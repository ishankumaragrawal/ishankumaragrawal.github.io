---
layout: post
title: Skin Segmentation in Images
subtitle: This posts explains various ways through which you can segment out the color of the skin from the rest of the image.
gh-repo: 
gh-badge: [star, fork, follow]
cover-img: /assets/img/background.png
tags: [Computer Vision]
comments: true

---

Skin Segmentation can be a important aspect of pre-processing data for Deep Learning Models. It can be used whenever you are making a model which works on Hands, Faces etc. Unlike segmentation in other tasks (like [this](https://arxiv.org/abs/2005.05218) or [this](https://arxiv.org/abs/2001.04074) ) here it can be done without using a huge DL model.
Some of these methods work only for segmenting out the parts of skin from rest of the image, while rest can be used for segmenting foreground from background in general.

It cant be assumed that a model working better in my examples would also work better in your usecase, hence I would suggest to try all and also try by altering the thresholds a little to make it best for your use.

## 1. Using RGB Thresholding
Thresholding is the most simple and fast method of doing this. The way this method works is it assumes skin colors to be clustered near each other on the RGB model, and allows only values between those thresholds hence masking out the rest.

Here you can try and make the thresholds tighter or looser based on what works best for your usecase.

```python

def RGBMasking(img,bbox=None):
    """
    Segments the Hand from the Image, using RGB Rules
    Parameters
    ----------
    img: The image itself [H, W, 3/4]
    bbox: Bounding Box of the desired object format [x_min, x_max, y_min, y_max]
    """
    img = torch.tensor(img)
    r = img[:,:,0].clone()
    g = img[:,:,1].clone()
    b = img[:,:,2].clone()

    rule_rgb = (r > 0.3725).int()*(g > 0.156).int()*(b > 0.0784).int()*(r > g).int()*(r > b).int()*(abs(r - g) > 0.0588).int()
    
    rgb_ruled_img = img[:,:,:3] * rule_rgb.unsqueeze(2).repeat(1,1,3)
    
    #Removing everything detected outside bounding box if its provided
    if bbox is not None:
        bbox_mask = np.zeros((rgb_ruled_img.shape[0],rgb_ruled_img.shape[1],rgb_ruled_img.shape[2]))
        bbox_mask[bbox[0]:bbox[1],bbox[2]:bbox[3],:] = 1
        rgb_ruled_img *= bbox_mask
        
    return rgb_ruled_img


```

![RGB Results](../assets/img/rgb.png){: .mx-auto.d-block :}

## 2. Using HSV Thresholding

The HSV Color Model is another model to define the color spectrum similar to RGB Model.
Here the parameters are H(Hue), S(Saturation) and V(Value or Brightness) 

This color model is used more for skin segemntation, although it doesnt perform as well as RGB in this usecase of hands.

```python
def HSVMasking(img,bbox=None):
    """
    Segments the Hand from the Image, using HSV Rules
    Parameters
    ----------
    img: The image itself [H, W, 3/4]
    bbox: Bounding Box of the desired object format -[x_min, x_max, y_min, y_max]
    """
    img = torch.tensor(img)
    r = img[:,:,0].clone()
    g = img[:,:,1].clone()
    b = img[:,:,2].clone()

    #Converting RGB to HSV
    #cv2.cvtColor(self.image, cv2.COLOR_RGB2HSV) can also be used
    
    max_clr = torch.max(input=r,other=g)
    max_clr = torch.max(input=max_clr,other=b)

    min_clr = torch.min(input=r,other=g)
    min_clr = torch.min(input=min_clr,other=b)

    diff = max_clr - min_clr

    H = torch.ones_like(r)
    S = torch.ones_like(r)

    zero_t = torch.zeros_like(r)

    H = torch.where(max_clr == r, (60 * ((g - b) / diff) + 360) % 360, H)
    H = torch.where(max_clr == g, (60 * ((b - r) / diff) + 120) % 360, H)
    H = torch.where(max_clr == b, (60 * ((r - g) / diff) + 240) % 360, H)
    H = torch.where(max_clr == min_clr, zero_t, H)

    H = H/360
    S = torch.where(max_clr == 0, zero_t, diff/max_clr)
    V = max_clr
    
    #Thresholding    
    hsv_mask = (H < 0.1388).int() * (S < 0.68).int() * (S > 0.18).int()
        
    hsv_ruled_img = img[:,:,:3] * hsv_mask.unsqueeze(2).repeat(1,1,3)
    
    if bbox is not None:
        bbox_mask = np.zeros((hsv_ruled_img.shape[0],hsv_ruled_img.shape[1],hsv_ruled_img.shape[2]))
        bbox_mask[bbox[0]:bbox[1],bbox[2]:bbox[3],:] = 1
        hsv_ruled_img *= bbox_mask
        
    return hsv_ruled_img

```

![HSV Results](../assets/img/hsv_2.png){: .mx-auto.d-block :}

## 3. GrabCut
This is a algorithm introduced in the paper by Roth et. al. [[link to paper]](https://dl.acm.org/doi/10.1145/1186562.1015720) and does the task of seperating forground from background with minimum user interaction. 
Although this algorithm is fairly simple to use an gives exceptionally good results, it has to be kept in mind that it **can only be used when the skin (subject) is in the foreground**.

This algorithm also needs a **Bounding Box**. 
If you dataset doesnt give that, fret not as it work fairly well for a general loose bounding box which can be easily made if your subject is centered (which it should considering GrabCut works only for foreground seperation).

```python
def GrabCut(img, bbox=None):
    """
    Segments the Hand from the Image, using the GrabCut Algo
    Parameters
    ----------
    img: The image itself [H, W, 3/4]
    bbox: Bounding Box of the desired object format -[x_min, y_min, len_x, len_y]
    """
    #If the input is RGBA remove the A channel as CV2 requires RGB
    img = img[:,:,:3]
    #If you are inputting 
    img = cv2.cvtColor(img, cv2.COLOR_RGB2BGR)
    
    bgdModel = np.zeros((1,65),np.float64)
    fgdModel = np.zeros((1,65),np.float64)
    
    if bbox is None:
        bbox = (10,10,200,200)
    
    mask=np.zeros(img_rgb.shape[:2],np.uint8)
    cv2.grabCut(img, mask, bbox, bgdModel, fgdModel, 20, cv2.GC_INIT_WITH_RECT)
    
    mask2 = np.where((mask==2)|(mask==0),0,1).astype('uint8')
    
    img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    return img[:,:,:3]*mask2[:, :, np.newaxis].repeat(3,2)
```

![HSV Results](../assets/img/grabcut.png){: .mx-auto.d-block :}


Apart from these you can also try to **combine these methods**. For instance the mask param of GrabCut, can be replaced by the mask produced by RGB or HSV (sort of like a good initialisation). This would lead to the best accuracy.

For more depth check out these papers-
1. Shah et. al. Combinatorial Color Space Models for Skin Detection in Sub-continental Human Images [link](https://www.researchgate.net/publication/221365117_Combinatorial_Color_Space_Models_for_Skin_Detection_in_Sub-continental_Human_Images)

2. Kolkur et. al. Human Skin Detection Using RGB, HSV and YCbCr Color
Models [link](https://arxiv.org/pdf/1708.02694.pdf)

