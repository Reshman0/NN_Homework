Generalization and Localization Based Style Imitation for Grayscale Images
This repository demonstrates the method proposed in the paper “Generalization and Localization Based Style Imitation for Grayscale Images”. The core idea is to learn a style transformation (e.g., an emboss filter) using:

Generalization (ANN): A feedforward neural network (FFANN) to map original (unfiltered) images to filtered images.
Localization (k-NN): A k-NN-based texture synthesis step to capture local textures and details that the ANN might miss.

Project Structure
.
├── filtered_imgs/         # Folder with filtered images (e.g., emboss) matching imgs/
├── filtered_imgs_ex/      # Older or unused filtered images (not part of the main workflow)
├── imgs/                  # Folder with original grayscale images
├── imgs_ex/               # Older or unused original images (not part of the main workflow)
├── oldimgs/               # Additional old images (also not used in the main workflow)
├── .gitattributes         # Git attributes file
├── ann_output_img1.png    # Example ANN output (from the trained model)
├── final_stylized_img1.png# Example final stylized image after k-NN texture synthesis
├── image_style_imitation.ipynb  # Main Jupyter Notebook containing all steps
├── model_weights.pth      # Saved model weights (FFANN)
└── README.md              # This file

imgs/: Contains your main unfiltered (original) grayscale images (e.g., img1.jpg, img2.jpg, ...).
filtered_imgs/: Contains the main filtered versions (e.g., img1_filtered.png) for style imitation (emboss, blur, etc.).
*_ex/ folders: These contain older or unused images and are not part of the primary pipeline.
oldimgs/: Also contains older or backup images not actively used.
ann_output_img1.png: An example output produced by the trained ANN on a test image.
final_stylized_img1.png: The final stylized image after combining the ANN output with k-NN-based texture synthesis.
image_style_imitation.ipynb: A single Jupyter Notebook that walks through data preparation, model training, inference, and k-NN texture synthesis.
model_weights.pth: The trained model’s weights (saved after training)

Usage
All the main steps are demonstrated inside image_style_imitation.ipynb:

Data Preparation

Load and resize images in imgs/ and filtered_imgs/ to a consistent size (e.g., 128×128).
Create a PyTorch Dataset of 3×3 patches (input) and the corresponding pixel intensity from the filtered images (target).
Model Definition and Training

A feedforward neural network (FFANN) is defined with 9 input neurons (for the 3×3 patch), several hidden layers, and 1 output neuron (predicted pixel intensity).
Train the network using MSE loss and SGD.
After training, the model weights are saved as model_weights.pth.
Inference (ANN Output)

Use the trained model to predict a filtered version of any new (or the same) grayscale image.
The notebook shows how to generate an ANN output image (e.g., ann_output_img1.png).
Texture Synthesis (k-NN Localization)

Calculate the difference map = (filtered image) - (ANN output).
Build a patch table (DiffPatchTable) from the difference map to capture local texture details.
For a new image, run the ANN to get its output, then use k-NN to find the best matching texture patches from the difference map.
Combine the ANN output with these local texture patches to produce the final stylized image (final_stylized_img1.png).
Result Visualization

Compare the original image, the ANN output, and the final stylized image side by side.

Example Workflow
Open image_style_imitation.ipynb in Jupyter or VS Code.
Run the notebook cells in order:
Data Preparation: Creates the patch-based dataset.
Model Training: Trains the FFANN.
ANN Inference: Generates an output for a test image.
k-NN Texture Synthesis: Applies the difference map patches to refine the ANN output.
Check outputs such as ann_output_img1.png (the ANN’s result) and final_stylized_img1.png (the refined final result).
Notes and Future Improvements
Advanced Techniques: The method can be enhanced using causal neighborhood search or iterative texture synthesis for more coherent textures.
Multiple Filters: You can train the ANN on various filters (emboss, blur, sharpen, etc.) and test its generalization.
Larger Patch Sizes: Using 5×5 or 7×7 for the k-NN texture patches can yield better details.
Color Images: Extend to color by using 3-channel inputs or a luminance-chrominance approach.

Acknowledgments
Inspired by the paper “Generalization and Localization Based Style Imitation for Grayscale Images”.
References to “Image Analogies” by Hertzmann et al. and texture synthesis methods by Wei & Levoy, Efros & Leung.
