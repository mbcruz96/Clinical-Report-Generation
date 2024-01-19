**Clinical Report Generator using Federated Learning**
- ![Federated learning diagram](assets/Img/fed learning.png)
- Designed a Transformer model with the following architecture: a multimodal CNN encoder and a generative LSTM decoder to generate clinical reports based off individual patient diagnostic information.
- After training multiple models, the model weights were averaged using Federated Learning to create a global model and propagated the weights back to each individual model.
- By utilizing a federated learning, the model could be upscaled so that hospitals could use the model to generate clinical reports without sharing private patient information across hospitals.
- **Goal:** To implement a model that would allow medical data to be used in deep learning models without breaching constraints imposed by HIPPA
