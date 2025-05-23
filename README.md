# Project: Federated Learning for Clinical Report Generation
**Project Goal:** To develop a novel approach for automated clinical report generation from medical imaging data within a federated learning framework, addressing data privacy concerns (HIPAA) while enabling collaborative model training across multiple institutions. 

**Problem Statement:**
The integration of deep learning into the medical field is significantly hampered by stringent HIPAA laws, which restrict the use and distribution of sensitive patient information for research purposes.  This limitation creates a data bottleneck, preventing the training of robust models that require large and diverse datasets.  Furthermore, the current manual process of clinical report generation is prone to human error, potentially leading to inaccurate medical records and misdiagnoses. 




**Approach & Methodology:**
Our experiment aimed to overcome these challenges by implementing a federated learning architecture for clinical report generation. 
- Model Architecture: Each independent client model utilized an encoder-decoder network.  The encoder was a fine-tuned ResNet152 Convolutional Neural Network (CNN) for medical image processing, and the decoder was an LSTM-based Recurrent Neural Network (RNN) for text generation. 
- Federated Learning (FedAvg): The FedAvg architecture was implemented, where multiple client models (representing individual medical facilities) were trained independently on their respective subsets of data.  Their trained layer weights were then sent to a global model, averaged, and propagated back to each client, improving overall accuracy while preserving patient anonymity. 
- Dataset: The IU X-Ray dataset, consisting of Chest X-Rays and accompanying medical reports, was used.  Frontal X-ray images were exclusively used for simplification, resulting in 3691 examples. 

**Data Pre-processing:**
- Images were converted to torch tensors, pre-processed to fit the ResNet input, and normalized. 
- Reports were loaded into pandas dataframes. 
- A rudimentary text cleaning pipeline was developed, including lower-casing, removing non-ASCII characters and punctuation, separating conjoined words, and redacting sensitive patient information (replaced with "XXXX"). 
- A vocabulary of 1700 words was constructed using CountVectorizer, and word-to-index and index-to-word dictionaries were created. 
- Training Parameters: Models were trained for 10 epochs with a batch size of 64, using cross-entropy loss and the Adam optimizer with a learning rate of 3e-3. 

**Key Contributions & Results:**
- Successfully implemented a federated learning setup using the FedAvg architecture, demonstrating a methodology for training medical models while upholding HIPAA laws and protecting patient confidentiality. 
- Designed and trained an encoder-decoder model (ResNet encoder, LSTM decoder) capable of generating clinical reports from medical images. 
- The loss graph for individual model training showed a desirable decreasing trend. 

**Challenges & Limitations:**
- Over-fitting: The model exhibited severe over-fitting to the training data, often generating generic "normal" reports even when abnormalities were present in the test images.  This is likely due to an inherent data imbalance in clinical report datasets, where normal cases far outnumber abnormalities. 
- Limited Data: The IU-Xray dataset, with only several thousand data points, was smaller than other similar datasets (e.g., MIMIC-CXR with over 100,000 examples), contributing to over-fitting. 
Model Simplicity: The choice of an LSTM decoder over a Transformer architecture (due to time and resource constraints) likely limited the model's ability to create deep connections between words and handle complex context. 
- Image Processing: Excluding lateral X-ray images, while necessary for resource management, might have reduced the overall accuracy of the model by decreasing the data available for the encoder. 
- Federated Learning Integration: While the federated learning framework was established, the inherent over-fitting of the individual models meant that further testing in a multi-client federated setting was not fully pursued. 
Future Directions:
- Attention Mechanism Integration: Explore the implementation of attention mechanisms or Transformer-based decoders to improve the model's ability to create richer contextual connections and mitigate over-fitting to "normal" cases. 
- Dataset Expansion: Incorporate larger and more balanced medical imaging datasets to reduce over-fitting and improve generalization.
- Dynamic Image Input: Investigate methods for dynamically processing both frontal and lateral images if computational resources permit, to provide more comprehensive visual information to the encoder.
Detailed Error Analysis: Conduct more extensive testing and analysis to precisely diagnose the fundamental causes of over-fitting and to determine the optimal architecture for federated clinical report generation. 
