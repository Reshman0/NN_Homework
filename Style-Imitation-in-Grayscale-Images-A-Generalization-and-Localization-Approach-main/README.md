

---

This project implements the method described in the paper "Generalization and Localization Based Style Imitation for Grayscale Images." In essence, we train a simple feedforward neural network to transform an original grayscale image into one that mimics an emboss effect. The network takes a small 3×3 patch of pixels as input and predicts the intensity of the center pixel, learning a general mapping between the unfiltered and filtered images. Since the network struggles with reproducing fine local textures (like subtle brush strokes), we complement it with a k-NN based texture synthesis step. This additional process calculates the difference between the network's output and the true filtered image, and then uses a patch-based nearest neighbor search to restore local texture details that the network could not capture.

All steps—from data preparation (resizing and patch extraction) to model training, inference, and texture refinement—are demonstrated in a single Jupyter Notebook included in the repository. Simply install the required Python libraries (numpy, OpenCV, PyTorch, scikit-learn, and matplotlib), and run the notebook to see the entire pipeline in action. The project is modular and easily extendable, so you can experiment with different filters, patch sizes, and improvements to further enhance the final stylized results.

---
