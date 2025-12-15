# Qwen GradCAM Evaluation - Panel-Level
Attribution on the MusciClaims Scientific Figure
Dataset

## Abstract
The MuSciClaims benchmark evaluates scientific claim verification using information-rich, multi-panel figures, but although it reveals that vision–language models (VLMs) often fail to localize evidence or interpret figure components, it does not explain how these models actually search for visual support. To address this gap, we investigate the visual grounding behavior of Qwen 2.5 VL (7B) across four baselines designed to probe where the model looks when verifying claims. Our experiments range from unguided panel prediction with Grad-CAM attribution, to claim-processed variants, to fully guided prompting where the model receives the correct panel and must identify the relevant evidence region. This structured analysis exposes how different inputs shape the model’s attention and grounding behavior. Notably, in the guided setting, Qwen achieves 87.81% accuracy in verifying the support claims, demonstrating strong latent grounding capabilities despite known limitations in claim verification performance. Our findings provide the first systematic, panel-level attribution study on MuSciClaims, offering clearer insight into how VLMs interpret scientific figures.

## 📋 Prerequisites

* **Google Account** (to access Google Colab and Google Drive).
* **GPU Runtime**: These notebooks require a GPU. The code is optimized for CUDA execution (T4 or A100 recommended).
* **Data Files**:
    * **Test Dataset**: The notebook downloads the claims and labels remotely from hugging face.
    * **Image Dataset**: A collection of scientific figure images referenced in the dataset. [Link to Image Dataset][https://drive.google.com/file/d/1_24AXdQvJ8S98WjYdFZ4-bqhBJB72HvF/view?usp=share_link]

## 🚀 Setup Instructions

### 1. Google Drive Configuration
The code expects a specific folder structure in your Google Drive to locate the images.

1.  Open your [Google Drive](https://drive.google.com/).
2.  Create a new folder named `VLM`.
3.  Inside the `VLM` folder, create a subfolder named `paper_figures`.
4.  **Upload Images**:
    * Download the full image dataset (if provided as a ZIP).
    * Unzip the images and upload **all individual image files** directly into the `paper_figures` folder on Drive.
    * *Note*: The notebook will search for images at `/content/drive/MyDrive/VLM/paper_figures/[image_name]`.

### 2. Running the Baselines

1.  **Choose a Baseline**: Select the notebook you wish to run (e.g., `Baseline0.ipynb`, `evaluation_musciclaims_vlm_project_baseline3.py`, etc.) and upload it to [Google Colab](https://colab.research.google.com/).
2.  **Set Runtime Type**:
    * Go to **Runtime** > **Change runtime type**.
    * Select **A100 GPU with High RAM** under Hardware accelerator.
    * Click **Save**.
3.  **Mount Drive**:
    * Run the initial cells in the notebook. You will be prompted to permit the notebook to access your Google Drive. Click **Connect to Google Drive**.
    * This is required to access the images stored in `VLM/paper_figures/`.
4.  **Install Dependencies**:
    * The setup cells will automatically install necessary libraries (e.g., `transformers`, `accelerate`, `qwen-vl-utils`).
5.  **Load Dataset**:
    * **For Baseline 3 (and similar files):** The script automatically downloads the `test` split of the MuSciClaims dataset from the Hugging Face hub. No local file upload is needed for the claims/labels.
    * *(If running other Baselines that require local files, you may need to manually upload a `test_set.jsonl` file.)*

### 3. Usage

* **Configuration**: Each baseline uses a `get_config()` function to set model IDs and paths. Ensure the `image_root_dir` (default: `/content/drive/MyDrive/VLM/paper_figures/`) is correct.
* **Execution**: Run the cells sequentially. The scripts will:
    1.  Load the specific model (e.g., Qwen2.5-VL) and its processor.
    2.  Download the dataset and preprocess the claims.
    3.  Iterate through the data, loading the required image from Drive.
    4.  Generate verification verdicts (SUPPORT/NON_SUPPORT) and, for Baseline 3, Grad-CAM visualizations.
* **Output**: Results, logs, and Grad-CAM image overlays will be stored, likely in a path similar to `/content/drive/MyDrive/VLM/Baseline3/overlay`.

## ⚠️ Common Issues

* **Image Not Found**: If you see `Skipping: Image not found`, ensure your images are in `My Drive/VLM/paper_figures/` and that the filenames match the dataset references.
* **CUDA/Memory Errors**: If the runtime crashes, try restarting the session or ensuring no other heavy GPU sessions are running.

## 📁 File Structure Summary

```text
Google Drive/
└── My Drive/
    └── VLM/
        └── paper_figures/
            ├── figure_1.jpg
            ├── figure_2.jpg
            └── ... (all extracted images)
