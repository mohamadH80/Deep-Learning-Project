# Deep-Learning-Project
final project of Deep Learning graduate course in Sharif University of Technology


## GANBERT

This is the code for the paper **"GAN-BERT: Generative Adversarial Learning for Robust Text Classification with a Bunch of Labeled Examples"** published in the **ACL 2020 - short paper** by *Danilo Croce* (Tor Vergata, University of Rome), *Giuseppe Castellucci* (Amazon) and *Roberto Basili* (Tor Vergata, University of Rome).

GAN-BERT is an extension of BERT which uses a Generative Adversarial setting to implement an effective semi-supervised learning schema. It allows training BERT with datasets composed of a limited amount of labeled examples and larger subsets of unlabeled material. 
GAN-BERT can be used in sequence classification tasks (also involving text pairs). 


## The Model

GAN-BERT is an extension of the BERT model within the Generative Adversarial Network (GAN) framework (Goodfellow et al, 2014). In particular, the Semi-Supervised GAN (Salimans et al, 2016) is used to make the BERT fine-tuning robust in such training scenarios where obtaining annotated material is problematic. When fine-tuned with very few labeled examples the BERT model is not able to provide sufficient performances. With GAN-BERT we extend the fine-tuning stage by introducing a Discriminator-Generator setting, where:

- the Generator G is devoted to producing "fake" vector representations of sentences;
- the Discriminator D is a BERT-based classifier over k+1 categories.

![GAN-BERT model](https://github.com/crux82/ganbert/raw/master/ganbert.jpg)

D has the role of classifying an example concerning the k categories of the task of interest, and it should recognize the examples that are generated by G (the k+1 category). 
G, instead, must produce representations as much similar as possible to the ones produced by the model for the "real" examples. G is penalized when D correctly classifies an example as fake.

In this context, the model is trained on both labeled and unlabeled examples. The labeled examples contribute to the computation of the loss function concerning the task k categories. The unlabeled examples contribute to the computation of the loss functions as they should not be incorrectly classified as belonging to the k+1 category (i.e., the fake category).

The resulting model is demonstrated to learn text classification tasks starting from very few labeled examples (50-60 examples) and to outperform the classical BERT fine-tuned models by a large margin in this setting.

## dataset

Large language models (LLMs) are becoming mainstream and easily accessible, ushering in an explosion of machine-generated content over various channels, such as news, social media, question-answering forums, educational, and even academic contexts. Recent LLMs, such as ChatGPT and GPT-4, generate remarkably fluent responses to a wide variety of user queries. The articulate nature of such generated texts makes LLMs attractive for replacing human labor in many scenarios. However, this has also resulted in concerns regarding their potential misuse, such as spreading misinformation and causing disruptions in the education system. Since humans perform only slightly better than chance when classifying machine-generated vs. human-written text, there is a need to develop automatic systems to identify machine-generated text with the goal of mitigating its potential misuse. 

- **Subtask B. Multi-Way Machine-Generated Text Classification:** Given a full text, determine who generated it. It can be human-written or generated by a specific language model.


| Task          | Google Drive Folder Link                                                                                           | File ID                                        |
|---------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| Whole dataset | [Google Drive Folder](https://drive.google.com/drive/folders/14DulzxuH5TDhXtviRVXsH5e2JTY2POLi)            | 14DulzxuH5TDhXtviRVXsH5e2JTY2POLi            |
| Subtask B     | [Google Drive Folder](https://drive.google.com/drive/folders/11YeloR2eTXcTzdwI04Z-M2QVvIeQAU6-)            | 11YeloR2eTXcTzdwI04Z-M2QVvIeQAU6-            |



### Statistics
| Subtask                     |  #Train |   #Dev  |
|:----------------------------|--------:|--------:|
| Subtask B                   |  71,027 |   3,000 |


#### Subtask B:
An object of the JSON has the following format:
```
{
  id -> identifier of the example,
  label -> label (human: 0, chatGPT: 1, cohere: 2, davinci: 3, bloomz: 4, dolly: 5),
  text -> text generated by machine or written by human,
  model -> model name that generated data,
  source -> source (Wikipedia, Wikihow, Peerread, Reddit, Arxiv) on English
}
```
