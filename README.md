# Azure-AI-Foundry
Getting started with Azure AI Foundry is an exciting journey! Here’s a step-by-step guide to help you dive in:

# 1. Sign In: First, sign in with the Azure CLI using the same account that you use to access your AI Project:
   ```bash
   az login
   ```

# 2.  Install the Azure AI Projects Client Library: You’ll need to install the Azure AI Projects client library and Azure Identity:
   ```bash
   pip install azure-ai-projects azure-identity
   ```

# 3.  Create a Project Client in Code: Use the following code to create a project client. Make sure to replace `your_connection_string` with your actual project connection string:
   ```python
   from azure.identity import DefaultAzureCredential
   from azure.ai.projects import AIProjectClient

   project_connection_string = "your_connection_string"
   project = AIProjectClient.from_connection_string(conn_str=project_connection_string, credential=DefaultAzureCredential())
   ```

# 4.  Explore Azure OpenAI Service : The Azure OpenAI Service provides access to OpenAI's models, including GPT-4, DALLE-3, and more. You can install the OpenAI SDK and use it with your project client:
   ```bash
   pip install openai
   ```

# 5. Build and Deploy: 
Once you have your project set up, you can start building and deploying your AI applications. Azure AI Foundry offers various tools and services to help you evaluate, debug, and improve your applications.

Sure! Let's add some code snippets to the steps we discussed earlier.

Continuing from the previous points:

# 6. Utilize Pre-Built Models : Here’s an example of how to use a pre-built sentiment analysis model:

   ```python
   from azure.ai.textanalytics import TextAnalyticsClient
   from azure.core.credentials import AzureKeyCredential

   endpoint = "your_endpoint"
   key = "your_key"
   credential = AzureKeyCredential(key)
   text_analytics_client = TextAnalyticsClient(endpoint=endpoint, credential=credential)

   documents = ["I love programming with Azure AI!"]
   response = text_analytics_client.analyze_sentiment(documents=documents)

   for doc in response:
       print(f"Sentiment: {doc.sentiment}, Scores: {doc.confidence_scores}")
   ```

# 7. Customization and Fine-Tuning : Fine-tuning a model using your own data can be done with Azure Machine Learning. Here’s a sample code for training a custom model:

   ```python
   from azure.ai.ml import MLClient
   from azure.identity import DefaultAzureCredential
   from azure.ai.ml.entities import Data

   subscription_id = "your_subscription_id"
   resource_group = "your_resource_group"
   workspace = "your_workspace"

   ml_client = MLClient(DefaultAzureCredential(), subscription_id, resource_group, workspace)
   data_path = "path_to_your_data"

   # Load data
   data = Data(path=data_path)
   data = ml_client.data.create_or_update(data)

   # Train model
   job = ml_client.jobs.create_or_update(
       name="custom_model_training",
       display_name="Custom Model Training",
       description="Train a custom model",
       compute="your_compute_target",
       inputs={"data": data},
       experiment_name="custom_model_experiment"
   )

   ml_client.jobs.stream(job.name)
   ```

# 8. Monitoring and Management: Monitoring deployed models using Azure Monitor:

   ```python
   from azure.monitor.query import LogsQueryClient
   from azure.identity import DefaultAzureCredential

   client = LogsQueryClient(credential=DefaultAzureCredential())
   query = "AzureDiagnostics | where ResourceType == 'MODEL'"

   response = client.query_logs(
       "your_log_workspace_id",
       query,
       timespan="PT1H"
   )

   for result in response:
       print(result)
   ```

# 9. Security and Compliance : Example of setting up identity and access management:

   ```python
   from azure.identity import DefaultAzureCredential
   from azure.keyvault.secrets import SecretClient

   keyvault_url = "https://your-key-vault-name.vault.azure.net/"
   credential = DefaultAzureCredential()
   client = SecretClient(vault_url=keyvault_url, credential=credential)

   secret = client.set_secret("mySecret", "mySecretValue")
   print(f"Secret {secret.name} set to value {secret.value}")
   ```

# 10. Collaboration and Scaling: Using Azure DevOps for CI/CD:

    ```yaml
    trigger:
      branches:
        include:
          - main

    jobs:
    - job: Build
      pool:
        vmImage: 'ubuntu-latest'
      steps:
      - task: UsePythonVersion@0
        inputs:
          versionSpec: '3.x'
          addToPath: true
      - script: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
        displayName: 'Install dependencies'
      - script: python -m unittest discover
        displayName: 'Run tests'
    ```


