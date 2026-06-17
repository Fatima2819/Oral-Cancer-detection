🦷** Oral Cancer Detection using Hybrid Parallel Deep Learning**
A hybrid parallel deep learning framework combining MTUNet++, Vision Transformer (ViT), and MeDSAN Attention Module for early detection of Oral Squamous Cell Carcinoma (OSCC) from histopathological images.

 Authors

Name                Email
Fatima Tul Zahra   Su92-bsdsm-f22-017@superior.edu.pk
Syeda Mashael      Su92-bsdsm-f22-014@superior.edu.pk

Supervisor: Hafiz Muhammad Shahzad (Lecturer)
Department: Software Engineering — The Superior University, Lahore

📌 Problem Statement
Oral cancer is among the most dangerous yet most late-diagnosed cancers — especially in Pakistan where 91.5% of OSCC cases are detected at late stage (Naseer et al., 2016). Traditional diagnosis through visual examination and biopsy is:
❌ Invasive and painful for patients
❌ Time-consuming (days to weeks for results)
❌ Heavily dependent on specialist pathologists
❌ Prone to inter-observer variability
This project proposes an automated AI-based early detection system that classifies histopathological images as Normal or OSCC within seconds.

🏗️ Model Architecture

The proposed Fusion Model uses a hybrid parallel design. The input image (224×224 RGB) is simultaneously passed through two parallel branches — MTUNet++ which extracts local spatial features like cell nuclei shapes and tissue boundaries, and a Vision Transformer (ViT) (vit_tiny_patch16_224) which captures the global tissue structure through self-attention. Both branches produce 192-dimensional feature vectors. The ViT output is then refined by the MeDSAN attention module, which re-weights features to highlight clinically relevant malignant regions and suppress background noise. The CNN and Transformer features are then concatenated into a 384-dimensional vector and passed through a 4-stage classifier with BatchNorm and Dropout layers to produce the final prediction — Normal or OSCC.

📊 Dataset

The model was trained and evaluated on the Oral Disease Dataset from Kaggle, containing 10,002 histopathological images across two perfectly balanced classes — 5,002 images of healthy oral tissue (oral_normal) and 5,000 images of cancerous tissue (oral_scc). All images are RGB format and were resized to 224×224 pixels. The dataset was split into 80% training (8,001 images), 10% validation (1,000 images), and 10% test (1,001 images). Training data was augmented with horizontal flipping, random rotation, and color jitter to improve generalization. Validation and test sets were kept clean with only resizing and normalization applied.

⚙️ Training Configuration

The model was trained using the AdamW optimizer with a learning rate of 1e-4 and weight decay of 0.01 for better regularization. CrossEntropyLoss was used as the loss function with a batch size of 32. A ReduceLROnPlateau scheduler (patience=3) was used to automatically reduce the learning rate when validation loss plateaued. To prevent overfitting, Early Stopping with patience=5 was applied along with Dropout layers (0.1 to 0.3) throughout the classifier. Training was done on Google Colab using an NVIDIA GPU, with the model and data stored on Google Drive.

📈 Results

The model achieved a final test accuracy of 98.50% on 1,001 unseen images. The AUC-ROC score was 0.9989, indicating near-perfect discrimination between normal and cancerous tissue. Precision, Recall, and F1-Score all stood at 0.9850. Sensitivity (cancer detection rate) was 0.9860 and Specificity (normal detection rate) was 0.9840. Training stopped at epoch 10 out of a maximum of 30 due to early stopping, with a best validation accuracy of 98.00%. The close alignment between train accuracy (98.25%), validation accuracy (98.00%), and test accuracy (98.50%) confirms that the model generalized well and did not overfit.
🔬 Key Contributions

This work proposes a novel hybrid parallel architecture where MTUNet++ and ViT run simultaneously — not sequentially — capturing both local cellular features and global tissue structure at the same time. The integration of the MeDSAN attention module reduces false positives by directing the model's focus toward clinically relevant malignant regions. The project is specifically motivated by the late-diagnosis crisis in Pakistan and is designed with low-resource clinical settings in mind where specialist pathologists are scarce.


⚠️ Limitations

The current model performs binary classification only (Normal vs OSCC) and does not support multi-stage cancer grading. It has been tested on a single Kaggle dataset and external hospital validation is still needed. Explainable AI (XAI) has not been integrated yet, and the model requires GPU compute due to the ViT branch.


🔮 Future Work

Future directions include multi-stage cancer grading (Stage I–IV), integration of Grad-CAM or SHAP for model explainability, development of a lightweight model for mobile or edge deployment, validation on local Pakistani hospital datasets, and a multi-modal approach combining clinical metadata with imaging data.


🙏 Acknowledgements

This project is dedicated to the memory of Mashael's aunt, who showed immeasurable strength in her battle with oral cancer. Her journey inspired us to work toward better and earlier detection for patients in Pakistan. We thank our supervisor Sir Hafiz Muhammad Shahzad for his continuous guidance throughout this research.


📄 License

This project is submitted as a Final Year Project at The Superior University, Lahore. For academic use only.
