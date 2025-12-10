# Qwen GradCAM Evaluation - Panel-Level
Attribution on the MusciClaims Scientific Figure
Dataset

## Abstract
The MuSciClaims benchmark evaluates scientific claim verification using information-rich, multi-panel figures, but although it reveals that vision–language models (VLMs) often fail to localize evidence or interpret figure components, it does not explain how these models actually search for visual support. To address this gap, we investigate the visual grounding behavior of Qwen 2.5 VL (7B) across four baselines designed to probe where the model looks when verifying claims. Our experiments range from unguided panel prediction with Grad-CAM attribution, to claim-processed variants, to fully guided prompting where the model receives the correct panel and must identify the relevant evidence region. This structured analysis exposes how different inputs shape the model’s attention and grounding behavior. Notably, in the guided setting, Qwen achieves 87.81% accuracy in verifying the support claims, demonstrating strong latent grounding capabilities despite known limitations in claim verification performance. Our findings provide the first systematic, panel-level attribution study on MuSciClaims, offering clearer insight into how VLMs interpret scientific figures.

