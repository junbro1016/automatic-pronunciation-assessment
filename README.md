# Tell your words 🗣
## Automatic pronunciation assessment service for children

<div align="center">
  <img width="669" alt="스크린샷 2023-12-30 오후 5 49 04" src="https://github.com/JunBro1016/problem-solving/assets/82267460/a7b87f56-ad8c-4d9a-9d42-75d8b33e8e49">
</div>


This repository conatins codes and descriptions of industry-academic-cooperation project with **SKT NUGU** in Hanyang University's artificial intelligence and application class. **Tell your words** is a service that automatically evaluates children's English pronunciation using AI speakers. Below are the frameworks used for the project.

<div align="left">
   <img src = "https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=PyTorch&logoColor=white"/>
   <img src = "https://img.shields.io/badge/transformers-blue?style=flat-square"/>
   <img src = "https://img.shields.io/badge/ScikitLearn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white"/>
   <img src = "https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=NumPy&logoColor=white"/>
   <img src = "https://img.shields.io/badge/pandas-150458?style=flat-square&logo=pandas&logoColor=white"/>
   <img src = "https://img.shields.io/badge/GoogleColab-F9AB00?style=flat-square&logo=Google%20Colab&logoColor=white"/>
</div>

## Introduction 😁
### Q) Why are we doing this?
- We all know how the communication skill is important. Also, education for children will affect the next generation. After the pandemic, the alpha(α) generation is facing the problem of lack of language skills. They have learned language through passive digital media such as YouTube instead of direct interactions. For these children, adults have to support to improve their language skill enough, but double-income family is universal especially in Korea, which makes it difficult to count on individual family member to educate their child.

- Many families send children to academies for English education, but nonetheless, academies often focus on grammar and university enrollment exams rather than children's pronunciation and speaking skills.

### A) Speaking practice service for children with AI speaker NUGU
- There is a market gap for active 'speaking' education for the alpha generation.
- Due to the characteristics of AI speakers, it can be used for educational purposes even in households where smartphone usage is restricted.
- Measuring a child's pronunciation skills through simple quizzes: Using the NUGU AI Speaker, we provide some simple quizzes to encourage a child to speak. Then, we provide parents with an **analysis report of the child's pronunciation** compared to normal pronunciation through deep learning techniques. This service will help develop the child's language skills in an untact environment. In addition, it **tracks the child's language development**, giving parents a comprehensive understanding of the child's language skills. **(For a detailed description of the service, please refer to the `presentation.pdf` file in the `others` folder)**

## Data description 📁
To evaluate the speaker’s pronunciation fluency, we utilized publicly opened data from the [speech accent archive](http://accent.gmu.edu) (Weinberger, Steven., 2015. Speech Accent Archive. George Mason University). This dataset is dedicated to the study of accents of people from different language backgrounds and provides English speech data recorded by people of different countries, genders, and ages. Native and non-native English speakers read a given English paragraph, and their readings are carefully recorded. Here’s how the researchers collected their data.

They constructed an elicitation paragraph that read by each subject. This paragraph is written in common English words, but contains challenging English sound and sound sequences, encompassing practically all English phonetics. Each subject is recorded individually in a quiet room. Subjects sit at a table and are approximately 8-10 inches from the microphone. Subjects are then allowed to look at the elicitation paragraph for a minute or so, and they are permitted to ask about words that are unfamiliar. Subjects then read the paragraph once into a high-quality recording device. (Many of these recordings were done on a Sony TC-D5M using a Radio Shack 33-3001 unidirectional dynamic microphone, and on a Sony minidisk recorder. MDR-70, with a Sony ECM-MS907 stereo microphone) Every remote researcher must specify the type of recording device employed. Below is the recorded elicitation paragraph.

The elicitation paragraph:

> *Please call Stella. Ask her to bring these things with her from the store: Six spoons of fresh snow peas, five thick slabs of blue cheese, and maybe a snack for her brother Bob. We also need a small plastic snake and a big toy frog for the children. She can scoop these things into three red bags, and we will go meet her Wednesday at the train station.*

The elicitation paragraph contains most of the consonants, vowels, and clusters of standard American English.

## Code description 📝
### labeling-via-fewshot-learning.ipynb
<img src = "https://colab.research.google.com/assets/colab-badge.svg"/>
A dataset we wanted was that contains audio files of multiple people saying the same phrase, labeled with pronunciation scores, but this type of dataset was hard to find. So we decided to manually label the pronunciation scores ourselves. In the real service cases, we assume that the manual labeling is done by experts. However, it is too exhaustive and almost impossible to manually label all the audio data. Hence, we used a few-shot learning technique.

In this stage, we first change our wav files into tensors. And before few-shot learning, we manually labeled the sample data as 0,1,2 (higher means better pronunciation) for accuracy, completeness, fluency, and prosodic. We then used this data and few-shot learning technique to label pronunciation scores for the entire dataset. If you wonder what each evaluation metric means, please refer below.

- **accuracy**: The level at which the learner pronounces each word with an accurate utterance
- **completeness**: The percentage of the words that are actually pronounced
- **fluency**: Does the speaker pronounce smoothly and without unnecessary pauses?
- **prosodic**: Does the speaker pronounce in correct intonation, stable speaking speed and rhythm?

1. **Change wav to tensors and manually label samples**: Define a function to convert audio files to tensors using Wav2Vec2. Create a DataFrame to store file paths, vectors, and manual labels. Convert original audio files to tensors and store them in the DataFrame. Remove rows with NaN values and save the DataFrame as 'audio_reference.pkl'.
2. **Few shot learning**: Load the labeled data from 'audio_reference.pkl'. Define classes for audio encoding and few-shot learning. Split the data into training and testing sets. Set up the loss function (binary cross-entropy) and optimizer (Adam). Perform the training loop for data with the same and different classes.
3. **Labeling via few shot learned model**: Initialize test data and switch the model to evaluation mode. Compute similarity scores for each class and update the DataFrame with predicted labels.

-----

### audio-augmentation.ipynb
After labeling the pronunciation scores of the speech data, data augmentation is performed. There are many benefits of it, but here are some of the most important ones.

- **Improvement in Generalization Ability**: Augmentation helps the model to not overly rely on specific environments or conditions. This enables the model to maintain high performance in various real-world situations.
- **Prevention of Overfitting**: Augmentation aids in preventing overfitting when the training data is limited. Exposure to diverse forms and types of data enhances the generalization ability, preventing the model from fitting to closely too the training set.
- **Creation of Robust Models**: Augmentation helps in making model more robust and resilient. For example, it enhances the model’s ability to handle noise, environmental variations, and imperfect speech, contributing to its robustness in real-world scenarios.

The most important part of data augmentation is it can ensure the reliability of the model. Speech recorded by A.I. speaker is susceptible to ambient noise. However, by adding noise and other sound effects during the augmentation process, we can create a model that is robust to these situations. To augment wav files, we referred [“Data Augmenting Contrastive Learning of Speech Representations in the Time Domain” (Kharitonov et al., 2020)](https://paperswithcode.com/paper/data-augmenting-contrastive-learning-of) from paperswithcode, and used WavAugment library.

1. **Audio augmentation**: Augments audio data for machine learning by loading original audio information, creating paths for augmented files, and applying random modifications like pitch shifting and reverberation. The modified audio is then saved for later analysis.
2. **Create a new reference pickle file for later use**: Combines information from original and augmented audio files, creating a new reference file. The extended DataFrame includes paths and scores for both sets, ensuring augmented files have the same scores as their originals. This is crucial for diverse and effective machine learning model training.

-----

### pronunciation-scoring-via-fine-tuned-model.ipynb
Finally, this is a stage for scoring the children’s pronunciation, and visualize it as a graph. We take two different approaches to predict the children’s pronunciation, one based on the fine-tuned model prediction and the other based on similarity comparison. This is the first approach, predicting the child’s pronunciation score based on the fine-tuned model prediction. In this stage, we used the labeled data from the few-shot learning to fine-tune the Wav2Vec2 model. Since we have total four target variables (`accuracy`, `completeness`, `fluency` and `prosodic`), we executed four different versions of model training, and utilized each fine-tuned model. For this stage, we referred to the [official guidance of Hugging Face](https://huggingface.co/docs/transformers/tasks/audio_classification). 

1. **Load and preprocess dataset**: Loads the `audio_reference_final.pkl` dataset, splits it into train, validation, and test sets, and saves the test set for later evaluation. Then creates a label mapping dictionary and loads the Wav2Vec2 feature extractor for audio data. A preprocessing function is defined to convert audio files into the proper format for fine-tuning.
2. **Fine tuning**: Fine-tunes a pre-trained Wav2Vec2 model for four pronunciation aspects: `accuracy`, `completeness`, `fluency`, and `prosody`. For each aspect, the model is trained using specific hyperparameters, including learning rate and batch size. The `Trainer` class from the Hugging Face `transformers` library is utilized for the training process. The resulting models are pushed to the Hugging Face model hub for sharing.
3. **Inference**: After fine-tuning, the models are used for inference on a test audio file `test.wav`. The file is preprocessed, and each fine-tuned model predicts logits for the four pronunciation aspects. The predicted class with the highest probability is determined, converted to a label using the model's `id2label` mapping, and printed for each aspect.
4. **Graph visualization**: Using the `plotly` library, the code creates a radar chart to visually represent a child's pronunciation scores for the four aspects. The chart includes the child's scores and an average score for reference. This visualization provides a quick overview of the child's pronunciation performance in different aspects.

-----

### pronunciation-scoreing-via-similarity.ipynb
This is the second approach, predicting the child’s pronunciation score based on the similarity to the reference data. For the use of wav2vec 2.0 model, we refered to [“wav2vec 2.0: A Framework for Self-Supervised Learning of Speech Representations” (Baevski et al., 2020)](https://paperswithcode.com/paper/wav2vec-2-0-a-framework-for-self-supervised) from paperswithcode.

1. **Change wav files to tensors via pre-trained wav2vec 2.0 model**: After augmentation, we built our reference dataset by converting all the audio files into tensors using Wav2Vec 2.0 model.
2. **Convert new speech data into a tensor and find the n most similar tensors**: When a recorded child’s voice comes through the AI speaker, we convert it to a tensor and find the reference that is most similar to it. In this case, we used cosine similarity to calculate the similarity.
3. **Graph a child's pronunciation score**: Visualize the child’s predicted pronunciation scores for the four categories in a radar chart. To visualize the graph, we used the `plotly` library.

-----

### evaluation.ipynb
This is the very last stage of our pronunciation prediction. We wevaluate each model’s classification performance at this stage. Since we can’t say that our answer dataset is accurate, it’s wise to follow each process and make it as an opportunity to learn about the overall evaluation process. The evaluation process can be divided into two main steps.

1. **Predict on test dataset**: First load our fine-tuned models and make a prediction on our test dataset.
2. **Evaluation and graph visualization**: Compare the prediction with the original labels, and evaluate the model performance. Then visualize their prediction results as heatmap. To check various evaluation metrics results, we use `classification_report` from scikit learn.

## Demonstration 🔥
The demonstration video can be found from [here](https://youtu.be/m08JF9tZT98).



