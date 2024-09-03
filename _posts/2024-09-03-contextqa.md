---
layout: post
title: "Introducing ContextQA: Your AI-powered assistant"
slug: introducing-contextqa
categories: llm
published: true
related_image: /images/contextqa.png
excerpt_separator: <!--more-->
---

<p align="center"><img src="../images/contextqa.png"/></p>
<br>
<!-- excerpt-start -->
Hey everyone! I’m excited to introduce you to **ContextQA**, a Python package I’ve been working on that’s designed to make your life easier when working with language models. **ContextQA** is ready to use right out of the box and integrates seamlessly with FastAPI and LangChain to offer a range of powerful features.
<!--more-->
With **ContextQA**, you can effortlessly handle tasks such as regular chat and conversational QA, complete with relevant sources and streaming responses. It also provides tools for managing your data sources, fine-tuning LLM settings (like the model and temperature), and adjusting vector DB settings to suit your needs.

In this blog post, I’ll dive into the following topics:

1. **Overview of ContextQA**: What it is, how it works, and what makes it stand out.
2. **Setting Up**: A step-by-step guide to getting started with **ContextQA**, from installation to initial configuration.
3. **Core Features**: A detailed look at the key functionalities, including chat capabilities, conversational QA, and data management.
4. **Customizing Settings**: How to adjust LLM and vector DB settings to optimize performance for your specific use cases.
5. **Wrap up**

I’ve put a lot of thought into making **ContextQA** as versatile and user-friendly as possible. I hope this post helps you get the most out of it and inspires you to explore its full potential. Stay tuned for a deep dive into each of these topics!

# What it is, how it works, and what makes it stand out

**ContextQA** is a tool that allows you to have a ready-to-use chatbot and QA assistant for chatting and interacting with your own data. It is built on top of
great and robust libraries such as [FastAPI](https://fastapi.tiangolo.com/), [LangChain](https://www.langchain.com/) and [HuggingFace](https://huggingface.co/).

It abstract all the complexity related to LLM communication, prompting, encoding, decoding, memory management, and other key features, making it easy to get started with a simple `pip install` command.

Custom configurations is what makes **ContextQA** so versatile and powerful. You can configure:

- LLM models
- Vector stores
- Memory management
- Embeddings

Regarding QA sessions, when **ContextQA** answers the user's question, it also provides the relevant sources of information that were used for creating the final answer.

#### Here are some examples of how you can use custom configurations to tailor ContextQA to your specific needs:

- You can use a specific LLM model that is best suited for your task
- You can use a specific vector store to store your data. For example, you could use [Pinecone](https://www.pinecone.io/) for fast vector search.
- You can use a specific memory management strategy to optimize the performance of **ContextQA**. For example, you could use an external Redis server
- You can configure the size of the chunks that will be encoded. For example, you could set a size of 2000 tokens/words to have a bigger context in each chunk of your data.

By customizing the configuration of **ContextQA**, you can create a tool that is perfectly suited for your specific needs.

# Setting Up

First, let's install **ContextQA**

```bash
pip install contextqa
```

After installing it, run the following command to start it

```bash
contextqa init
```

You'll see something like this

```bash
$ contextqa init

2024-08-28 01:00:39,586 - INFO - Using SQLite
2024-08-28 01:00:47,850 - INFO - Use pytorch device_name: cpu
2024-08-28 01:00:47,850 - INFO - Load pretrained SentenceTransformer: sentence-transformers/all-mpnet-base-v2
INFO:     Started server process [20658]
INFO:     Waiting for application startup.
2024-08-28 01:00:47,850 - INFO - Running initial migrations...
2024-08-28 01:00:47,853 - INFO - Context impl SQLiteImpl.
2024-08-28 01:00:47,855 - INFO - Will assume non-transactional DDL.
2024-08-28 01:00:47,860 - INFO - Running upgrade  -> 0bb7d192c063, Initial migration
2024-08-28 01:00:47,862 - INFO - Running upgrade 0bb7d192c063 -> b7d862d599fe, Support for store types and related indexes
2024-08-28 01:00:47,864 - INFO - Running upgrade b7d862d599fe -> 3058bf204a05, unique index name
INFO:     Application startup complete.
INFO:     Uvicorn running on http://localhost:8080 (Press CTRL+C to quit)
```

Now we can go where the tool is running and start with the initial configuration. Note that the tool runs on the port 8080 by default. You can change it by passing the port number using the `-p` option.

## Docker image

Optionally, you can run it using the official Docker image.

```bash
docker run --name [A CUSTOM NAME] -p 8080:8080 zaldivards/contextqa:2.0.5
```

### Initial configuration

When starting **ContextQA** for the first time, you'll see the welcome view, and when clicking the button at the bottom we will see the configuration stepper.

![Initial config](https://contextqa-assets.s3.amazonaws.com/init.png)

In the first step you need to set an LLM provider, model, access token(click the ? button to get help) and temperature. Click the save button and finally the next step button.

![Step 1](https://contextqa-assets.s3.amazonaws.com/settings/step-1.png)

Then, set up the vector store and some encoding parameters. Again, click the save button and finally the next step button.

![Step 2](https://contextqa-assets.s3.amazonaws.com/settings/step-2.png)

Finally, stablish other extra settings such as memory and database engine. Click the save button and the finalize button.

![Step 3](https://contextqa-assets.s3.amazonaws.com/settings/step-3.png)

# Core features

## CLI

When installing it, users are provided with a useful CLI for initializing the tool. As mentioned above, you can start **ContextQA** by running the following command:

```bash
contextqa init
```

However, users can also provide certain settings such as port number, and different custom paths. In order to get more information regarding the available options, run the following command:

```bash
$ contextqa init --help

Usage: contextqa init [OPTIONS]

ContextQA init command

╭─ Options ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ --port           -p      INTEGER    Port number to run the server on [default: 8080]                                                                                                                     │
│ --settings-json  -s      FILE       Path to the json file that will held the settings [default: /home/your-user/contextqa-data/settings.json]                                                             │
│ --media-home     -m      DIRECTORY  Path to the directory that will contain media files such as ingested PDFs [default: /home/your-user/contextqa-data/media]                                             │
│ --chroma-home    -c      DIRECTORY  Path to the directory that will be used by ChromaDB [default: /home/your-user/contextqa-data/vectordb-data]                                                           │
│ --help                              Show this message and exit.                                                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

Note that all of them have default values. By default, **ContextQA** creates the **contextqa-data** directory in your user's home directory. Additionally, it creates subdirectories and files for storing the tool's settings, media files and vector storage data.

You can provide custom paths for sure. However, data might be lost if you had been using **ContextQA** with the default parameters. So you will see a warning message when you provide either the `-s`, `-m` or `-c` parameters:

```bash
$ contextqa init -m ~/custom-dir

Be careful when using either of the following parameters for setting custom paths: -s, -m or -c. Data might be lost if you already have initialized contextqa. If this is the first time, proceed.

2024-08-29 13:51:14,251 - INFO - Using SQLite
2024-08-29 13:51:18,332 - INFO - Use pytorch device_name: cpu
2024-08-29 13:51:18,332 - INFO - Load pretrained SentenceTransformer: sentence-transformers/all-mpnet-base-v2
INFO:     Started server process [37387]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://localhost:8080 (Press CTRL+C to quit)
```

## Data management

Data management features live in the menu's _Sources_ section. Here, you can either ingest data sources or check the ones that have already been ingested.

### Data ingestion

**ContextQA** supports ingestion of txt, csv and pdf files. You can ingest up to 10 data sources per ingest process. Throughout this process, data sources are encoded and stored into the vector database.

![data ss1](https://contextqa-assets.s3.amazonaws.com/data-management/ss-1.png)
![data ss2](https://contextqa-assets.s3.amazonaws.com/data-management/ss-2.png)

Additionally, other metadata is stored in the relational database. Here, the database keeps track of each data source, its digest, and to which vector database and index it pertains. So for example, if you try to ingest a data source that has already been ingested and its content is the same since the last ingest, you won't be able to ingest it.
![data ss3](https://contextqa-assets.s3.amazonaws.com/data-management/ss-3.png)

### Check and manage existing data sources

Here, you can check and/or delete existing data sources.
![data ss4](https://contextqa-assets.s3.amazonaws.com/data-management/ss-4.png)
When you are in this section, you can just start typing and it will filter the matching data sources. For removing the filter, you can either click the "clear" button or press _esc_.
![data ss7](https://contextqa-assets.s3.amazonaws.com/data-management/ss-7.png)

For removing data sources, you can select one, more than one, or all checkboxes.
![data ss5](https://contextqa-assets.s3.amazonaws.com/data-management/ss-5.png)
![data ss6](https://contextqa-assets.s3.amazonaws.com/data-management/ss-6.png)

## Chatbot

**ContextQA**'s chatbot feature offers a user-friendly way to have conversations with the LLM you have set. It provides conversation memory, chips with question placeholders and the option to enable internet access so it can overcome knowledge limitations.

![data ss8](https://contextqa-assets.s3.amazonaws.com/data-management/ss-8.png)

<span style="color:#FFC300">Please keep in mind that the conversation memory is saved in the client state so changes between sections does not affect the UI. However, if you refresh your browser the state will be lost</span>.

### Memory

![cb ss1](https://contextqa-assets.s3.amazonaws.com/chatbot/ss-1.png)
![cb ss2](https://contextqa-assets.s3.amazonaws.com/chatbot/ss-2.png)

### Placeholders

You can use the chips to use pre-determined questions.

![cb ss3](https://contextqa-assets.s3.amazonaws.com/chatbot/ss-3.png)

### Expanded knowledge - Agent

As we all know, LLMs know nothing about real-time data and data in general because they are trained on a static dataset and do not have access to the internet or other external data sources. This means that they cannot access or process real-time data, such as news articles, social media posts, or financial data. Additionally, LLMs do not have the ability to store or retrieve data, so they cannot access or use data that is not included in their training dataset.

To overcome this, LLMs can be provided with context so they can use it for answering questions about topics they do not have knowledge about. **ContextQA** use an agentic approach to expand the LLM's knowledge.

#### Limited knowledge

![cb ss4](https://contextqa-assets.s3.amazonaws.com/chatbot/ss-4.png)

#### Expanded knowledge

![cb ss5](https://contextqa-assets.s3.amazonaws.com/chatbot/ss-5.png)

## QA

The QA feature is where you are able to query and/or chat about your data sources. Here, **ContextQA** answers are based on the ingested data sources.
Relevant information that is used for generating a user-friendly answer is available when the "Sources" button is clicked. Each supported format is shown in a specific way.

### Text files

The following answer is based on relevant data sources that mention "Hodor".

![qa ss1](https://contextqa-assets.s3.amazonaws.com/qa/ss-1.png)

Relevant nodes(chunks) that somehow match user's query or question.

![qa ss2](https://contextqa-assets.s3.amazonaws.com/qa/ss-2.png)

### PDF files

Here, the relevant data sources are displayed as entire PDF pages to enhance UX.

![qa ss3](https://contextqa-assets.s3.amazonaws.com/qa/ss-3.png)

Note that you can select a single page, zoom in or out, and rotate it if necessary.

![qa ss4](https://contextqa-assets.s3.amazonaws.com/qa/ss-4.png)

![qa ss5](https://contextqa-assets.s3.amazonaws.com/qa/ss-5.png)

### CSV files

For csv files, each row is an individual relevant chunk, hence that's how they are displayed in the relevant sources UI.

![qa ss6](https://contextqa-assets.s3.amazonaws.com/qa/ss-6.png)

![qa ss7](https://contextqa-assets.s3.amazonaws.com/qa/ss-7.png)

## Markup and code highlighting support

Both the Chatbot and the QA assistant support markup and syntax highlighting, making it user-friendly for providing code snippets and well-formatted responses

![hl-1](https://contextqa-assets.s3.amazonaws.com/hl-1.png)

![hl-2](https://contextqa-assets.s3.amazonaws.com/hl-2.png)

# Customizing settings

## Models

Currently, users can choose between OpenAI's and Google Gemini's models.

![cs ss1](https://contextqa-assets.s3.amazonaws.com/custom-settings/ss-1.png)

The temperature parameter is important for fine-tuning the model's answers. Greater values mean more random answers and possible hallucinations.

## Vector storage

Here, users can choose either ChromaDB or Pinecone as vector databases and sematic search engines. Additionally, users can configure advance settings such as chunk size and chunk overlap. These settings might enhance or decrease quality of QA answers, so make sure to set the appropriate values for your use case.

![cs ss2](https://contextqa-assets.s3.amazonaws.com/custom-settings/ss-2.png)

![cs ss4](https://contextqa-assets.s3.amazonaws.com/custom-settings/ss-4.png)

<span style="color:#FFC300">You might lose existing data if you change either the "Vector store home", "Collection name", or "Index"</span>.

## Extra settings

Here, you can change the media directory, LLM memory engine, and database. Points to consider:

- When updating the media directory, all content of the current directory will be moved to the new directory.
- Data is migrated when the database is changed.

![cs ss3](https://contextqa-assets.s3.amazonaws.com/custom-settings/ss-3.png)

## Status

You can check the status of **ContextQA**'s components. The color codes are as follows:

- **<span style="color: green">Green</span>**: Indicates a healthy component.
- **<span style="color: gray">Gray</span>**: Indicates a component that is not being used.
- **<span style="color: red">Red</span>**: Indicates that the component is not working properly.

![status ss1](https://contextqa-assets.s3.amazonaws.com/status/ss-1.png)

Components marked in gray or red will have a button in the top right corner. Click it to see the status message.

![status ss2](https://contextqa-assets.s3.amazonaws.com/status/ss-2.png)

![status ss3](https://contextqa-assets.s3.amazonaws.com/status/ss-3.png)


# Wrap Up

**ContextQA** offers an intuitive and valuable set of features that allows you to leverage both LLMs and your own data. It is designed for developers, students, and general users, making it a versatile tool for a wide range of applications.

Feel free to report any bugs or request new features.

![report](https://contextqa-assets.s3.amazonaws.com/report.png)

