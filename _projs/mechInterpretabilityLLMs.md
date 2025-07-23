---
layout: work
title: "Mechanistic Interpretability of LLMs"
description : Leveraging Sparse Autoencoders to understand the learning process of an LLM
caption: Leveraging Sparse Autoencoders to understand the learning process of an LLM
tags: ["Explanability", "LLMs", "Sparse-autoencoders"]

thumbnail-img: 
share-img: 
comments: true
gh-repo: memesoo99/LLM_interpretability
gh-badge: [follow]
dated: 2025-02-01
category: new
---
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    <p>
      <strong>LLM Interpretability with Sparse Autoencoders</strong> explores how to reverse-engineer large language models (LLMs) to better understand their internal representations. 
      Traditional neuron-based analysis falls short due to <em>polysemanticity</em> — where single neurons encode multiple unrelated concepts. 
      To address this, we adopt <strong>Sparse Autoencoders (SAEs)</strong> to extract <em>monosemantic</em> features that more cleanly correspond to human-understandable concepts.
    </p>
    <p>
      Inspired by recent work from Anthropic, we train Top-K autoencoders across multiple LLMs and evaluate the quality of learned features using visualizations, feature steering, and interpretability metrics.
      We also propose techniques like <strong>Ghost Grads</strong> and a novel <strong>kScheduler</strong> to address dead latent issues in sparse training.
      Applications include insight into safety-related behaviors (e.g., bias, deception) and the ability to steer generation with targeted features instead of model finetuning.
    </p>
    <p><strong>Sample Results</strong></p>
    <p><strong>Example: Steering Vector Influence on Generation</strong></p>
    <table class="table table-bordered">
      <thead>
        <tr>
          <th>Steering Vector</th>
          <th>Generated Poem</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Unsteered</td>
          <td>
            The sun, oh glorious sun,<br>
            Bringing warmth to everyone,<br>
            Never to fade away.<br>
            Its rays, so bright and bold,<br>
            Painting the sky with gold,<br>
            Waking up the earth,<br>
            Making all things unfold.
          </td>
        </tr>
        <tr>
          <td>Donald Trump</td>
          <td>
            NYC is the city that never sleeps,<br>
            Where dreams come true and secrets keep.<br>
            A place where people from all walks of life,<br>
            Gather to make their own unique strife.<br>
            From Wall Street to Times
          </td>
        </tr>
        <tr>
          <td>Taj Mahal</td>
          <td>
            India, you beautiful country.<br>
            A land of history and culture so rich.<br>
            Your cities are magnificent, your people so kind.<br>
            I'm in love with you, oh India!<br>
            From the Himalayas to the Bay of Bengal,
          </td>
        </tr>
        <tr>
          <td>Adolf Hitler</td>
          <td>
            I am a cog in the great machine,<br>
            Wound up tight in the gears of industry.<br>
            My hands move with precision and speed,<br>
            As I churn out product after product
          </td>
        </tr>
      </tbody>
    </table>
    <p>
      This example illustrates how activating specific features (via steering vectors) influences the style, theme, and content of generated outputs — demonstrating the interpretability and controllability of internal representations.
    </p>
    <p>
      We also developed a real-time web-based feature activation visualizer and demonstrated feature-level alignment with real-world concepts like <em>gender bias, COT reasoning, and landmarks</em>. 
      These methods pave the way for more interpretable and steerable LLMs.
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
    <a href="https://docs.google.com/presentation/d/1VfSVlCjON-ypxgxc76mzgpa3l15qYOTrWChKYaZLTig/edit?usp=sharing" class="btn btn-secondary" target="_blank">
      View Slides (PPT)
    </a>
  </div>
</div>

