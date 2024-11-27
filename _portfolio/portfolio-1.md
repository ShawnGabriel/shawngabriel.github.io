---
title: "3D Mesh Surface Reconstruction From Point Clouds (Nov 2024)"
excerpt: "<img src='/images/DeepView.jpg'><br/><br/>
**2nd Place of UBC DSCI x DarkVision Computer Vision Hackathon**
<br/>"
collection: portfolio
---

In this project, [Reyhan Pamungkas](https://github.com/adhgn) and I attempt to recreate the solutions of the [SMRVIS: Point cloud extraction from 3-D ultrasound for non-destructive testing Paper](https://www.researchgate.net/publication/371414251_SMRVIS_Point_cloud_extraction_from_3-D_ultrasound_for_non-destructive_testing) by Tang, L. T. W. for a challenge hosted by UBC Data Science Club in collaboration with DarkVision, a British Columbia-based company that specializes in industrial imaging technology. The code for this project can be found [here](https://github.com/ShawnGabriel/3D-Mesh-Reconstruction-From-Point-Clouds).

<br/><img src='/images/DarkVision.png'>

Introduction to The Challenge
=======
The techniques that this project used, was utilized in biomedical imaging such as CT and SPECT scans, but we repurpose it for non-destructive testing of industrial components, such as steel pipes. By detecting manufacturing defects in **steel pipes**, the framework has industrial applications in **quality assurance** and **safety**. The challenge didn't provide a definitive guide that told us to recreate the solutions of the SMRVIS Paper, not until 2 days after the challenge was published. Hence, the methodologies tested can be seen as an experimentation phase, as we weren't given clear instructions on how to approach the problem.

Methodology
======
We explored a total of 3 methodologies, where each one played a crucial role in the development of our overall understanding of the challenge and the expected output to be yield by any model we decided to choose. Each methodology shined a light on how we viewed the overarching problem and what needs to be done immediately after each successes to keep a constant momentum, given that we only had **5 days** to work on the challenge during the reading break.

Brute Force Method
------
<div style="text-align: justify;">
At first, we leveraged the AI models, ChatGPT 4o and Claude 3.5 Sonnet. However, after receiving their inputs and trying to run them, it was a catastrophe. It was super hard to debug, because the AI models lack so much context of the problem we're trying to solve. And ultimately, the problem itself was too sophisticated to be digest by a language model and come up with a definitive/instant solution.
</div>

Voxel2Mesh Paper
------
<div style="text-align: justify;">
Then, we moved on to a research paper published in 2019 called <a href = "https://arxiv.org/abs/1912.03681">Voxel2Mesh: 3D Mesh Model Generation from Volumetric Data</a> by Wickramasinghe et al. where we tried approaching the code and figuring out how to recreate our own model. Unfortuantely, we then realized that it required both the volumes and meshes files to be in the same format which was an npy file. We then try modify the code to different file formats which in the end still didnt work. This was a pivotal moment for us, as we decided to exit out of implementing this paper. To our knowledge and intuition of the orchestration of the repository, we figured that altering the preprocessing file would lead numerous problems related to other files. 
</div>
<br/>
<br/>
<img src='/images/Attempt.png'>
<br/>
<br/>
<div align="center">
**Above is our attempt in modifying the preprocessing section of the repository.**
</div>

Reconstruction From Point Clouds
------
<div style="text-align: justify;">
So when started out, we tried to generate the results using the author's model. We thought we succeeded at first (more on this later), so, we then attempted to make our own model.  The repository had three **4 files** in order to build a desired model, as shown below:
</div>
- **c0.py** contains all of the distinctive parameters for the model itself, ranging from the number of recurrent layers to the number of epochs.
- **c1args.py** is where we preprocess the training data, both the ultrasound scans and the corresponding meshes.
- **c2load.py** is the core of the model. It requires all preceding files to be fully runnable in order to be executed.
- **test.py** is where the model is fed with the testing data and aims to reconstruct a surface mesh from given 3D volumetric data.

Model Architecture
------
**Why did we choose the R2 U-Net model?**
<br/>
In all honesty, the R2 U-Net was one of the best performing models according to the paper, hence our decision. Additionally, this architecture was one of the three architectures that had most of the parameters defined from the authors comments within each separate file. Now let's get technical. As we know, residual layers allows us leverage skip connections, giving we have a deep layer; we wouldn't want the model to be unable to learn, countering the vanishing gradient problem. Other than that, recurrent layers are used so each convolution block would be able to learn from their past mistakes, feeding into the same convolution block for **n amount of times**.


Results & Evaluation
======
By using the model we saved earlier, we are inputting some of the steelpipe data, and then comparing it to the reference mesh by using 5 metrics:
- F1 Score: ,
- Chamfer Distance: ,
- Hausdorff Distance: ,
- Mean Surface Distance (MSD): ,
- Residual Mean Square Distance (RMSD): 

For direct Hausdorff Distance values, we failed to calculate them because it took a very long time to run it. This is due to us having very limited time and resources, we decided to not include the values here. Along with us not able to calculate the Hausdorff Distance, we also see that the value for each metrics are not ideal for a functioning and viable model. We suspect that these problems are resulted due to the resulting npz file having so many points compared to the reference mesh. Here it says that the npz file contains 83 million points inside the array, compared to the mesh file which only has 40,000 points. This makes each metric produce a unreasonable value.

Challeges & Solutions
======





