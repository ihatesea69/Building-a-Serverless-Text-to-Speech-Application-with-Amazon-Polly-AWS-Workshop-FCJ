# Building a Serverless Text-to-Speech Application with Amazon Polly

[![Hugo](https://img.shields.io/badge/Built%20with-Hugo-ff4088?logo=hugo&logoColor=white)](https://gohugo.io/)
[![AWS](https://img.shields.io/badge/Platform-AWS-232F3E?logo=amazonwebservices&logoColor=white)](https://aws.amazon.com/)
[![Amazon Polly](https://img.shields.io/badge/Amazon-Polly-FF9900?logo=amazonaws&logoColor=white)](https://aws.amazon.com/polly/)
[![Serverless](https://img.shields.io/badge/Architecture-Serverless-FD5750?logo=serverless&logoColor=white)](https://aws.amazon.com/serverless/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/Deployed%20on-GitHub%20Pages-222222?logo=github)](https://ihatesea69.github.io/Building-a-Serverless-Text-to-Speech-Application-with-Amazon-Polly-AWS-Workshop-FCJ/)
[![Bilingual](https://img.shields.io/badge/Language-EN%20%7C%20VI-green)](https://ihatesea69.github.io/Building-a-Serverless-Text-to-Speech-Application-with-Amazon-Polly-AWS-Workshop-FCJ/)

A comprehensive hands-on workshop for building a serverless text-to-speech application using Amazon Polly and AWS services. This workshop demonstrates how to convert text content into high-quality audio files using a fully serverless architecture, eliminating the need for server management while ensuring high availability and scalability.

## Live Demo

**Workshop Site:** [https://ihatesea69.github.io/Building-a-Serverless-Text-to-Speech-Application-with-Amazon-Polly-AWS-Workshop-FCJ/](https://ihatesea69.github.io/Building-a-Serverless-Text-to-Speech-Application-with-Amazon-Polly-AWS-Workshop-FCJ/)

---

## Architecture Overview

![Architecture Diagram](content/Images/architecture.png)

The application provides a complete end-to-end solution for converting text to speech through a serverless pipeline. When a user submits text for conversion, the request flows through Amazon API Gateway to Lambda functions that orchestrate the conversion process using Amazon Polly, with results stored in S3 and metadata tracked in DynamoDB.

### How It Works: New Post Submission

When the application receives information about a new post to convert:

1. **API Gateway** receives the RESTful request from the static webpage hosted on Amazon S3.
2. **New Post Lambda** function initializes the MP3 generation process.
3. Post information is stored in **Amazon DynamoDB** for tracking.
4. **Amazon SNS** decouples the receiving process from audio conversion for asynchronous processing.
5. **Convert to Audio Lambda** is triggered by SNS when a new message appears.
6. **Amazon Polly** converts the text into an audio file in the specified language.
7. The MP3 file is saved to a dedicated **S3 bucket**.
8. DynamoDB is updated with the URL to the stored audio file.

### How It Works: Retrieving Posts

When the application retrieves information about posts:

1. **API Gateway** exposes the RESTful method for retrieving post information.
2. **Get Post Lambda** function handles the retrieval logic.
3. Post data including the S3 audio file reference is returned from **DynamoDB**.

---

## Application Demo

![Text-to-Speech Demo](content/Tasks/Images/ui5.gif)

The user interface accepts text input in multiple languages and converts it into playable audio files directly in the browser.

---

## AWS Services Used

| Service            | Purpose                                                                   |
| ------------------ | ------------------------------------------------------------------------- |
| Amazon Polly       | Text-to-speech synthesis with lifelike voices in 20+ languages            |
| Amazon API Gateway | RESTful API endpoint for text submission and retrieval                    |
| AWS Lambda         | Serverless compute for New Post, Convert to Audio, and Get Post functions |
| Amazon DynamoDB    | NoSQL database for storing post metadata and audio URLs                   |
| Amazon S3          | Storage for generated MP3 audio files and static website hosting          |
| Amazon SNS         | Message queue for decoupling post submission from audio conversion        |
| AWS CloudFormation | Infrastructure as code for automated deployment                           |
| AWS Step Functions | State machine orchestration (optional advanced usage)                     |

---

## Workshop Structure

This workshop takes approximately 90 minutes to complete and is divided into the following sections:

### Prerequisites and Environment Setup (15-20 min)

Prepare your AWS environment by launching a CloudFormation stack that provisions the necessary IAM roles, DynamoDB tables, and foundational resources.

### Task Breakdown

1. **Create a DynamoDB Table** - Set up the database for storing post information and audio file references
2. **Create an Amazon S3 Bucket** - Configure storage for generated MP3 files and static web hosting
3. **Create an SNS Topic** - Establish the messaging queue for asynchronous processing
4. **Create a New Post Lambda Function** - Build the function that initiates the conversion process
5. **Create a Convert to Audio Lambda Function** - Implement the Polly integration for text-to-speech conversion
6. **Test the Functions** - Validate the Lambda functions work correctly
7. **Create a Get Post Lambda Function** - Develop the retrieval endpoint for posts and audio links
8. **Expose the Lambda Function as a RESTful Web Service** - Configure API Gateway integration
9. **Create a Serverless User Interface** - Build the static web interface for user interaction

### Conclusion and Cleanup (10 min)

Review what you learned and properly clean up all deployed resources to avoid unexpected charges.

---

## Learning Objectives

After completing this workshop, you will be able to:

- Create and configure Amazon DynamoDB tables for data storage
- Build RESTful APIs using Amazon API Gateway
- Develop AWS Lambda functions triggered by API Gateway events
- Integrate AWS Lambda with Amazon Simple Notification Service for asynchronous processing
- Use Amazon Polly to synthesize speech in multiple languages and voices
- Deploy a complete serverless application using AWS CloudFormation

---

## Key Features of Amazon Polly

Amazon Polly overcomes common text-to-speech challenges including:

- **Homographs** - Words spelled identically but pronounced differently based on context
- **Text Normalization** - Properly interpreting abbreviations, acronyms, and units
- **Text-to-Phoneme Conversion** - Handling complex language mappings where similar spellings have different pronunciations
- **Foreign Words** - Processing terms like "deja vu," proper names, and international expressions

### Advantages

- **Rapid Response:** Supports real-time, interactive dialogue
- **Flexible Storage:** Allows caching and reuse of audio files
- **Unlimited Usage:** No additional charges for using converted speech
- **Easy Integration:** Simply send text to the Amazon Polly API

---

## Prerequisites

- AWS account with administrative access
- Basic understanding of AWS services (Lambda, API Gateway, S3, DynamoDB)
- Familiarity with RESTful APIs
- Web browser for accessing the workshop content

---

## Local Development

This workshop documentation is built with Hugo using the Learn theme.

```bash
# Clone the repository
git clone https://github.com/ihatesea69/Building-a-Serverless-Text-to-Speech-Application-with-Amazon-Polly-AWS-Workshop-FCJ.git
cd Building-a-Serverless-Text-to-Speech-Application-with-Amazon-Polly-AWS-Workshop-FCJ

# Initialize submodules (for theme)
git submodule update --init --recursive

# Run local development server
hugo server -D
```

Access the local site at `http://localhost:1313`

---

## Use Cases

While this workshop uses blog posts as an example, the application architecture can be applied to numerous scenarios:

- Converting website text into audio content for accessibility
- Reading recipes aloud while cooking
- Listening to news articles or books while driving or cycling
- Adding speech functionality to web and mobile applications
- Creating accessible content for visually impaired users
- Building voice-enabled customer service solutions

---

## References

- [Amazon Polly Documentation](https://docs.aws.amazon.com/polly/latest/dg/what-is.html)
- [Build Your Own Text-to-Speech Applications with Amazon Polly](https://aws.amazon.com/blogs/machine-learning/build-your-own-text-to-speech-applications-with-amazon-polly/)
- [What is Amazon API Gateway?](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
- [What is AWS Lambda?](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [Amazon DynamoDB Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
- [Amazon S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
- [AWS Serverless Application Model](https://aws.amazon.com/serverless/sam/)

---

## Contributing

For corrections, suggestions, or contributions, please contact: **hieunghiwork123@gmail.com**

---

## Community

[![AWS Study Group Blog](https://img.shields.io/badge/Blog-AWS%20Study%20Group-orange)](http://awsstudygroup.com)
[![Facebook Group](https://img.shields.io/badge/Facebook-AWS%20Study%20Group-1877F2?logo=facebook&logoColor=white)](https://www.facebook.com/groups/660548818043427/)
[![First Cloud Journey](https://img.shields.io/badge/Workshop-First%20Cloud%20Journey-blue)](https://000001.awsstudygroup.com/)

---

## License

This project is licensed under the MIT License.
