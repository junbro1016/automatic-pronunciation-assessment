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
To evaluate the speaker’s pronunciation fluency, we utilized publicly opened data from the **“speech accent archive”** (Weinberger, Steven., 2015. Speech Accent Archive. George Mason University. Retrieved from http://accent.gmu.edu). This dataset is dedicated to the study of accents of people from different language backgrounds and provides English speech data recorded by people of different countries, genders, and ages. Native and non-native English speakers read a given English paragraph, and their readings are carefully recorded. Here’s how the researchers collected their data.

They constructed an elicitation paragraph that read by each subject. This paragraph is written in common English words, but contains challenging English sound and sound sequences, encompassing practically all English phonetics. Each subject is recorded individually in a quiet room. Subjects sit at a table and are approximately 8-10 inches from the microphone. Subjects are then allowed to look at the elicitation paragraph for a minute or so, and they are permitted to ask about words that are unfamiliar. Subjects then read the paragraph once into a high-quality recording device. (Many of these recordings were done on a Sony TC-D5M using a Radio Shack 33-3001 unidirectional dynamic microphone, and on a Sony minidisk recorder. MDR-70, with a Sony ECM-MS907 stereo microphone) Every remote researcher must specify the type of recording device employed. Below is the recorded elicitation paragraph.

The elicitation paragraph:

> *Please call Stella. Ask her to bring these things with her from the store: Six spoons of fresh snow peas, five thick slabs of blue cheese, and maybe a snack for her brother Bob. We also need a small plastic snake and a big toy frog for the children. She can scoop these things into three red bags, and we will go meet her Wednesday at the train station.*

The elicitation paragraph contains most of the consonants, vowels, and clusters of standard American English.

## Code description 📝

