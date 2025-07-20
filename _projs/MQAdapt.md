---
layout: work
title: "MQA Adapt - Adapting MQA for efficient Inference"
description : Layerwise Adaptive Multi-Query Attention for efficient inference
caption: An insight into applying MQA at inference time on a layerwise level to improve inference time without dropping accuracy significantly.
tags: ["inference-time-speedup", "MQA", "research"]

thumbnail-img: 
share-img: 
comments: true
# gh-repo: Ishan-Kumar2/Molecular_VAE_Pytorch
gh-badge: [follow]
dated: 2024-12-01
category: new
---

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    <p>
      <strong>MQAdapt</strong> explores whether <em>Multi-Query Attention (MQA)</em> can be adaptively applied at inference time to reduce compute and memory usage in transformer models, with minimal performance drop. 
      Motivated by the success of inference-time optimizations like GQA and PTQ, we investigate three research questions: 
      <strong>RQ1</strong>: Does MQA reduce inference latency? 
      <strong>RQ2</strong>: Are some transformer layers more sensitive to MQA than others? 
      <strong>RQ3</strong>: How can we best select layers for MQA under a given budget?
    </p>
    <p>
      Our experiments show a linear improvement in compute and memory efficiency with increasing MQA layers. 
      However, layer sensitivity varies significantly — lower layers are more critical to overall performance, while alternating layers helps preserve accuracy. 
      Greedy strategies that apply MQA to consecutive layers lead to steep accuracy drops, while <em>alternating layer sampling</em> stabilizes performance, enabling up to 5 layers to use MQA with negligible loss. 
      MQAdapt offers a practical path to inference-time efficiency gains without retraining, especially promising for long-context generation tasks.
    </p>
  </div>
</div>


<div class="row mt-5">
  <div class="col-sm-6 text-center">
    <a href="https://drive.google.com/file/d/1D7_c-u_7fiNS_NdLD66xg1ItM7YH1leT/view?usp=sharing" class="btn btn-primary" target="_blank">
      View Full Report (PDF)
    </a>
  </div>
  <div class="col-sm-6 text-center">
    <a href="https://docs.google.com/presentation/d/1VQvTXy5RRU54HSbQNngFosrOZzrRyJ4IyrDfKLhgZ84/edit?usp=sharing" class="btn btn-secondary" target="_blank">
      View Slides (PPT)
    </a>
  </div>
</div>