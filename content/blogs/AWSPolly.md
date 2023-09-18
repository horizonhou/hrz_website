---
title: "Tutorial for Using Amazon Polly"
date: 2021-12-01T23:15:00+07:00
slug: 
category: AWS
summary:
description: 
cover:
  image: "covers/AWSPolly.jpg"
  alt: 
  caption: 
  relative: true
showtoc: true
draft: false
---

## Amazon Polly
We are going to use Amazon Polly which is a machine learning tool for converting text to lifelike speech. For more information, please visit the documentation.

## Set up an IAM role
We need to update our permission in order to use Amazon Polly API. First, let's find the Amazon SageMaker in the console and click on Notebook on the left side, select Notebook instances, then we click the link under Permissions and encryption.

![image1](/images/AWSPolly/sagemaker.png)

When we get into the new webpage, select Permissions and then add AmazonS3FullAccess and AmazonPollyFullAccess by clicking the Attach policies button to allow access to these Amazon services.

![image1](/images/AWSPolly/IAM.png)

## Getting started using Python SDK
In this guide we are going to use the function synthesize_speech which can take up to 3000 letters and transform it into real time speech with chosen voice. This process leads to relatively small latency in most cases.

First, let's import boto3 package which is used for managing AWS services.

![image1](/images/AWSPolly/step1.png)

Next, create an instance client of the client object in the boto3 package for polly. This will allow us to use and make requests to Amazon Polly service via Python.

![image1](/images/AWSPolly/step2.png)

Create the text we want convert to real time speach. Today we will only use simple text as and example. In this part, we can also get files from the Amazon S3 bucket, then convert it to string type to be processed.

![image1](/images/AWSPolly/step3.png)

Using our client, apply the dot notation to access the method synthesize_size in Polly. For values in the method, set Text to the variable my_text we created above, set OutputFormat to "mp3", and set VoiceId to "Joanna". The last value refers to the type of voices you want to hear. For more types of voices, please look at documentation.

![image1](/images/AWSPolly/step4.png)

Check the type of response.

![image1](/images/AWSPolly/step5.png)

We get a Python dictionary, so let's investigate the keys.

![image1](/images/AWSPolly/step6.png)

Check the value AudioStream.

![image1](/images/AWSPolly/step7.png)

We can output our received audio file to a local mp3 file. We send the value in AudioStream to stream, then write to a local file with address saved in the variable output.

![image1](/images/AWSPolly/step8.png)

We can also send our audio file to our S3 bucket, or directly use it somewhere else as needed.

## More Applications using Polly

Amazon Polly has way more stronger functions including converting longer text (beyond 3000 letters), please check documentation for more information.

The function of converting text to real time audio is useful in various of areas. For example, real time translation. It can also cooperate with machine visual to read text directly in real world scenarios. I would like to use a text file of French literature, first use some method (Amazon Translate would help) to translate the text file into English, then use the Amazon Polly to convert into real time audio and see the quality of it. Undoubtedly, this machine learning method will make our life more convenient in the future.