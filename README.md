# Azure-AI-Foundry
Getting started with Azure AI Foundry is an exciting journey! Here’s a step-by-step guide to help you dive in:

1. # Sign In: First, sign in with the Azure CLI using the same account that you use to access your AI Project:
   ```bash
   az login
   ```

2. # Install the Azure AI Projects Client Library: You’ll need to install the Azure AI Projects client library and Azure Identity:
   ```bash
   pip install azure-ai-projects azure-identity
   ```

3. # Create a Project Client in Code: Use the following code to create a project client. Make sure to replace `your_connection_string` with your actual project connection string:
   ```python
   from azure.identity import DefaultAzureCredential
   from azure.ai.projects import AIProjectClient

   project_connection_string = "your_connection_string"
   project = AIProjectClient.from_connection_string(conn_str=project_connection_string, credential=DefaultAzureCredential())
   ```

4. # Explore Azure OpenAI Service : The Azure OpenAI Service provides access to OpenAI's models, including GPT-4, DALLE-3, and more. You can install the OpenAI SDK and use it with your project client:
   ```bash
   pip install openai
   ```

5. **Build and Deploy**: Once you have your project set up, you can start building and deploying your AI applications. Azure AI Foundry offers various tools and services to help you evaluate, debug, and improve your applications.

For more detailed instructions and examples, you can check out the [Azure AI Foundry documentation](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/develop/sdk-overview).

Happy coding! If you have any specific questions or need further assistance, feel free to ask.
