---
title: "3D Mesh Surface Reconstruction From Point Clouds"
excerpt: "<img src='/images/DeepView.jpg'><br/><br/>
**2nd Place of UBC DSCI Club x DarkVision Computer Vision Hackathon**
<br/>"
collection: portfolio
---

In this project, [Reyhan Pamungkas](https://github.com/adhgn) and I attempt to recreate the solutions of the [SMRVIS: Point cloud extraction from 3-D ultrasound for non-destructive testing Paper](https://www.researchgate.net/publication/371414251_SMRVIS_Point_cloud_extraction_from_3-D_ultrasound_for_non-destructive_testing) by Tang, L. T. W. for a challenge hosted by UBC Data Science Club in collaboration with DarkVision, a British Columbia-based company that specializes in industrial imaging technology. The code for this project can be found [here](https://github.com/ShawnGabriel/3D-Mesh-Reconstruction-From-Point-Clouds).

<br/><img src='/images/DarkVision.png'>

Introduction to The Challenge
=======
The techniques that this project used, was utilized in biomedical imaging such as CT and SPECT scans, but we repurpose it for non-destructive testing of industrial components, such as steel pipes. By detecting manufacturing defects in **steel pipes**, the framework has industrial applications in **quality assurance** and **safety**. The challenge didn't provide a definitive guide that told us to recreate the solutions of the SMRVIS Paper, not until 2 days after the challenge was published. Hence, the methodologies tested were 

Methodology
======
Brute Force Method
------
At first, we leveraged the AI models, ChatGPT 4o and Claude 3.5 Sonnet. However, after receiving their inputs and trying to run them, it was a catastrophe. It was super hard to debug, because the AI models lack so much context of the problem we're trying to solve. And ultimately, the problem itself was too sophisticated to be digest by a language model and come up with a definitive/instant solution.

Voxel2Mesh Paper
------
