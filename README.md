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
* Customize and deploy this Sitecore Powershell Module in your Sitecore instance by following the steps described in the next section
* Publish all content items that are necessary for the Chatbot to populate the Azure Cognitive Search Index
* Validate the chat experience within the Azure AI Studio
* Deploy the chat experience as a new Web App or Power Virtual Agent bot from the Chat section
* Embed the chat experience within your website

## To extend or customize this module for project-specific needs:
* Clone this Github repository
* Migrate the config & serialized items into your repository
* Sync the items with Sitecore
* Populate the Azure OpenAI and Cognitive Search settings under _/sitecore/system/Modules/PowerShell/Script Library/AI Chatbot_
* Update the script to include content from all fields that are needed for the Chatbot
* Validate and promote your changes to production!

## Considerations/Limitations:
* Azure OpenAI is available in multiple regions. However, certain models/features are available only in specific locations. Choose the closest location which has the model/features that you are looking for. Review the [Azure OpenAI Models Guide](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models) for more information/status.
* The maximum length of input text for embedding models is 2048 tokens (equivalent to around 2-3 pages of text)
* Consider fine-tuning the responses to match your brand guidelines
* Consider supplying more context about the person, his/her interests, historical information, etc., to OpenAI from your orchestrating application for a personalized chat experience
* Implement Azure Security Best Practices for OpenAI like using Private Endpoints, using Azure AD Identity, etc.
* Apply Content Filters and consider using Azure AI Content Safety Studio for filtering harmful content if needed
