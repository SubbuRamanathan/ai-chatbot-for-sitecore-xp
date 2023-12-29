# AI-Powered Chatbot for Sitecore XP
This repository contains the Sitecore Powershell Module needed for connecting XP websites with Azure OpenAI & Cognitive Search to create an AI-powered chatbot.

## Prerequisites
* Active Azure Subscription
* As of today(17-Oct-2023), Azure OpenAI Service is in public preview and only available to customers based on request. Please ensure to submit the request via this form: https://aka.ms/oai/access. The approval process typically takes about 2-10 business days.

## Setup & Configuration
* Create Azure OpenAI Service from Azure Portal
* Launch [Azure AI Studio](https://oai.azure.com/)
* Create a new deployment selecting your preferred model(typically gpt-35-turbo-16k or gpt-4-32k). More details about models can be found [here](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models).
* Create a new deployment for embeddings by selecting the model as text-embedding-ada-002, which will be used later for generating embeddings
* Navigate to Chat, and select 'Add a data source'
* Choose Azure Blob Storage(if you will need to index files as well) or Azure Cognitive Search(if it will be only content) as data source
* Create the necessary elements prompted by the tool like Azure Blob Storage, Azure Cognitive Search, Search Index, etc., and complete the setup. Ensure to review the created Azure Resources and configure them based on Azure Security Best Practices
* Register an app in Azure Active Directory(now Entra ID) and obtain Tenant ID, Client ID & Client Secret, as you will need them in the upcoming steps
* Add appropriate role assignments to the app for Azure OpenAI(Cognitive Services OpenAI Contributor) and Cognitive Search(Search Service Contributor/Search Index Data Contributor) resources from their respective IAM sections.
* Customize and deploy this Sitecore Powershell Module in your Sitecore instance by following the steps described in the next section
* Implement Security Best Practices like Private Endpoints, Role-based Access Control, etc.
* Publish all content items necessary for the Chatbot to populate the Azure Cognitive Search Index. You could publish the respective individual item or the parent item along with subitems for indexing.
* Validate the chat experience within the Azure AI Studio
* Deploy the chat experience as a new Web App or Power Virtual Agent bot from the Chat section
* Embed the chat experience within your website. Below is a quick demo of the same, and detailed walk-through of the solution can be found here: [Building an Intelligent Chat Experience powered by Real time Business Content/Data with Azure OpenAI](https://youtu.be/IoavMH3akis?si=zRJjq-sP1z-yQabZ&t=1537),
[![AI Chatbot for Sitecore](https://i3.ytimg.com/vi/1UY0iFHJFgU/maxresdefault.jpg)](https://www.youtube.com/watch?v=1UY0iFHJFgU)

## To deploy, extend, or customize this module for project-specific needs:
* Clone this Github repository
* Migrate the config & serialized items into your repository
* Sync the items with Sitecore
* Populate the General Settings(Templates & Fields to be included), Azure OAuth, OpenAI, and Cognitive Search Settings in _/sitecore/system/Modules/PowerShell/Script Library/AI Chatbot/Settings_. For production deployments, you may need to optimize the _Index-Content_ & _Generate-Embeddings_ functions to retrieve the secrets from Azure Key Vault and/or any existing solution you may be following for storing/handling secrets.
* Validate and promote your changes to production!

## Considerations/Limitations:
* Azure OpenAI is available in multiple regions. However, certain models/features are available only in specific locations. Choose the closest location which has the model/features that you are looking for. Review the [Azure OpenAI Models Guide](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models) for more information/status.
* The maximum length of input text for embedding models is 2048 tokens (equivalent to around 2-3 pages of text)
* Consider fine-tuning the model to match your brand guidelines if needed. Please note that fine-tuning is expensive; you may review the [OpenAI pricing page](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/openai-service/) for more details. In most cases, you may also be able to achieve your goals via Prompt Engineering.
* Consider supplying more context about the person, his/her interests, historical information, etc., to OpenAI from your orchestrating application for a personalized chat experience
* Set up log monitoring and alerting to track any indexing failures and address issues proactively. This module logs the failures within SPE.log files.
* You may need to customize the solution, including module, chat web app, etc., for supporting multiple languages, multiple publishing targets, etc.
* Apply Content Filters and consider using Azure AI Content Safety Studio for filtering harmful content if needed
