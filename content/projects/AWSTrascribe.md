---
title: "Researching the Impact of Multiple Factors in Speech Transcription Using Amazon Transcribe Service"
date: 2021-05-15T23:15:00+07:00
slug: AWS, ANOVA
category: projects
summary:
description:
cover:
  image: "covers/AWSTranscribe.jpg"
  alt:
  caption:
  relative: true
showtoc: true
draft: false
author: ["Ruize Hou", "Angel Song", "Sirui Hu", "Aoran Wang", "Julin Ye"]
---

# Topic: Researching the Impact of Multiple Factors in Speech Transcription Using Amazon Transcribe Service

## Introduction
Audio is a popular source of content expression, ranging from music, podcast, to zoom classes. Audio not only enhances multimedia applications by serving as an extra channel of information but also adds a sense of realism by conveying emotion, time period, and geographical location of the speaker. During the Covid-19 pandemic in which social distancing is required, audio has become an increasingly important channel for people to conduct their businesses and connect with each other. For example, many companies adopted audio calls as a method to replace traditional meetings and schools delivered online lectures to avoid gatherings. Audio transcription, as a complementary service for audio, converts speech in an audio file into written text. It has a wide range of applications, such as extracting information from interviews, analyzing patterns in academic research and even adding subtitles to lecture recording. Thus, the accuracy of audio transcription becomes critical to whether or not the users can correctly and efficiently understand the audio and apply the results to their work field. Traditionally, users had to rely on transcription providers to manually listen and transcribe the audio into text, which was costly, inefficient and in poor accuracy. Thanks to the rapid development of artificial intelligence and machine learning technology, now we can use a lot of online transcription services to help us achieve our goals.

In this report, we are going to examine two factors speech speed, and accent, that could potentially affect the accuracy of audio transcription by measuring the word error rate(WER). We adopt [method] to generate 55 different texts by altering speech speed, and accent, and transcribe them to texts using Amazon Transcribe Service. We then calculate the corresponding word error rate for each speed and accent and analyze the results using a wide range of python statistics tools. Our assumption before data analysis is that first, when the speech speed increases, the accuracy will decrease holding other factors fixed, second, the accuracy of US accent will be higher than others. Based on the results, both accents and speed influence on Amazon transcribe accuracy, while accent poses a stronger effect than speed.

## Method Overview
The core method in our project is [Amazon Transcribe](https://aws.amazon.com/transcribe/) Services, which uses automatic speech recognition(ASR), a deep learning process, to convert speech to text quickly with high accuracy. The method enjoys four main benefits. First, it creates easily readable transcriptions by adding speaker diarization, punctuation and formatting. Second, it ensures customers privacy by identifying and redacting sensitive personally identifiable information and allowing contact centers to easily review and share the transcripts for the purpose of customer experience insight and agent training based on the PII. Third, it increases accuracy with customized transcriptions by allowing users to add new words to base vocabulary, such as product names, technical terminology, etc. or train the language model. Fourth, it filters specific words by enabling the user to mask or remove words that are unwanted.

## Research Design

![image1](/images/AWS/architecture_diagram.png)

We initially input SSML scripts to a Google text to audio converting service named Google TTS Audio Service, from which we generated two groups of audio files: ones with same speeds and different accents and ones with same accents and different speeds. To proceed, we uploaded them into two separate Amazon S3 buckets, and utilized Amazon Transcribe service to convert them to our source text files. Afterwards, we used the Jiwer speech evaluation recognition package to build the WER (world error rate) dataframe, where we compare the target original input SSML scripts and source text files we generated using Amazon Transcribe service. Finally, we input the WER dataframe to ANOVA analysis to testify whether our results are statistically significant. 

## Data Preparation

We generated raw audio files using an online voice-generator which applies the Google TTS Audio Service. Although Amazon has its own text-to-audio service named Amazon Polly, it has only four different accents available, which does not provide us enough sample data for the research. On the contrary Google TTS provides a variety of  The content includes five different texts as followed, ranging from novels and website contents to news articles:

As the research aims to analyze the effect of accents and speed on the accuracy of text generated by Amazon Transcribe. The raw audios cover six different accents including French, Spanish, Japanese, Korean, UK, and US. The audio files were also generated at five different speeds including 0.5,0.8,1.0,1.2, and 1.5 in the US accent. 

## Transcribe Model Running

After downloading audio files from s3 bucket, we run the transcribe model using our generated audio file. We divided our audio files into two parts. In the first part, we choose files based on six different accents with five different versions of text. In the second parts, we choose files based on five different accents with five different versions of texts. We use five different versions of texts in order to avoid the bias caused by one certain type of text.  We use  loops to run the transcribe and extract data from the Transcribe model. The results are saved into the text lists which contain all converted versions of text after running the  Transcribe model.

## Word Error Rate Calculation

In order to evaluate the accuracy of transcribed text generated by Amazon Transcribe, we introduce a metric called Word Error Rate (WER). This method is recommended by the US National Institute of Standards and Technology for the evaluation of ASR systems.
WER is defined as the normalized Levenshtein edit distance. Levenshtein edit distance calculates the distance between the reference and the hypothesis.:

The formula is

![image1](/images/AWS/wer_formula.png)

WER is the percentage of transcription errors produced by the ASR method compared to the number of words actually spoken. In other words, it’s the minimum number of words that need to be corrected to change the hypothesis transcript into the reference transcript, divided by the number of words that the speaker originally said. 
According to this formula, we know that the lower the WER, the more accurate the transcribed text is, with 0 error rate the best. WER can go beyond 1 if there are too many insertion errors.

The usage of WER is simple. This algorithm is contained in the jiwer package. First we should install it using the pip function.
![image1](/images/AWS/install_jiwer.png)
Then we import the wer function from the jiwer package
![image1](/images/AWS/import_jiwer.png)
After we prepared the reference text and hypothesis text we wanted to test on, we can call the wer() function to get the result (origin refers to reference text, test refer to hypothesis text),
![image1](/images/AWS/wer_function.png)
Calculating WER for all the transcribed text files we collected, we make our WER table and can move on to the statistical analysis part.
Below is a glimpse of the WER dataframe.
![image1](/images/AWS/all_wer_sample.png)


## Data Visualization And Analysis

According to our OLS Regression and data visualization, accents and speed do affect the accuracy of Amazon Transcribe. Amazon Transcribe results in accuracies for different accents which rank from the highest to lowest as US, UK, Spanish, French, Korean, and Japanese. Meanwhile, based on the regression, the positive coefficient of scripts generated from Japanese and Korean accents and WER suggest the error rate for these two accents tends to be higher compared to other accents, whereas the negative coefficient of scripts generated from UK, Spanish, and US accents and WER suggests a more accurate transcription.

As for the speed, the WER values of different speeds do not show a significant difference given a large p-value. From boxplot visualization, we can find that the average value of WER in the five different speeds falls in the range around 0.15. We also find that the difference between speed 0.8 which has the largest WER and speed 1.0 which has lowest WER are not significant, which corresponds to our main finding. Based on regression model analysis, the coefficients are all negative for the categorical speeds. If treating speed as a numerical variable, for every unit increase in speed, the WER value will decrease.
