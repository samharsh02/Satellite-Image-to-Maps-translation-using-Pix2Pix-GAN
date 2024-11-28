# Note: 
If the codeblock does not render on college internet for some reason, try using mobile data, it will open - happened with me a few times.

# Satellite-Image-to-Maps-translation-using-Pix2Pix-GAN

# Introduction:
This repository has the ipynb notebook for the mentioned project. The dataset link has been provided within the code, you can copy the kagglehub command and run it on your own machine. However it is suggested to use an environment that has GPU support. 

We have implemented Pix2Pix GAN for the task of image translation from satellite image to map image. Pix2Pix is a type of cGAN which trains on paired images and then the generator can be used to translate images from one form to another.

# Generator architecture:
The U-Net generator used here is a CNN with a 7-layer encoder and a 7-layer decoder connected via skip connections. The encoder uses downscaling with Conv2D, LeakyReLU, and Batch Normalization to extract features, while the decoder employs upscaling with Conv2DTranspose, Batch Normalization, and ReLU to reconstruct the image. Skip connections concatenate encoder features with corresponding decoder layers, preserving spatial details.

# Discriminator architecture:
The Discriminator is a Patch -GAN (CNN) with 4 downscaling layers that processes concatenated real/target and generated images. Each downscale layer applies Conv2D, LeakyReLU, and Batch Normalization. The final layers include a Conv2D with stride 1 and Batch Normalization followed by another Conv2D to output a single-channel feature map representing the likelihood of patches being real or fake. It uses PatchGAN architecture to classify overlapping image patches, promoting local realism.

# Setup:

Loss functions:  
   - The generator uses adversarial loss (binary cross-entropy) combined with L1 loss (mean absolute error) to improve both realism and similarity to the target image.  
   - The discriminator uses binary cross-entropy loss to distinguish real images from generated ones.

Generator training:  
   - The generator aims to minimize the adversarial loss while reducing the pixel-wise difference from the target image using L1 loss.  
   - This helps the generator create realistic outputs that align closely with the target.

Discriminator training:  
   - The discriminator learns to classify real images as 1 and generated images as 0, improving its ability to differentiate between real and fake.

Gradient calculations:  
   - Gradients for generator and discriminator losses are computed separately using TensorFlow's `GradientTape`.

# Evaluation:

Structural similarity Index(SSIM) :      0.9241
Fréchet Inception Distance (FID) :       866.28
Inception Score (IS) :       1.00 ± 0.00

Visualizations are present in the notebook.


