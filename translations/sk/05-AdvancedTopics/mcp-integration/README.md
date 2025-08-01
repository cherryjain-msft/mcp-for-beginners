<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "73240f845b99df9401fffd21c09a5f7b",
  "translation_date": "2025-07-17T10:58:52+00:00",
  "source_file": "05-AdvancedTopics/mcp-integration/README.md",
  "language_code": "sk"
}
-->
# Podniková integrácia

Pri budovaní MCP serverov v podnikateľskom prostredí často potrebujete integrovať existujúce AI platformy a služby. Táto sekcia popisuje, ako integrovať MCP s podnikateľskými systémami ako Azure OpenAI a Microsoft AI Foundry, čím umožníte pokročilé AI funkcie a orchestráciu nástrojov.

## Úvod

V tejto lekcii sa naučíte, ako integrovať Model Context Protocol (MCP) s podnikateľskými AI systémami, so zameraním na Azure OpenAI a Microsoft AI Foundry. Tieto integrácie vám umožnia využiť výkonné AI modely a nástroje pri zachovaní flexibility a rozšíriteľnosti MCP.

## Ciele učenia

Na konci tejto lekcie budete schopní:

- Integrovať MCP s Azure OpenAI a využiť jeho AI schopnosti.
- Implementovať orchestráciu nástrojov MCP s Azure OpenAI.
- Kombinovať MCP s Microsoft AI Foundry pre pokročilé schopnosti AI agentov.
- Využiť Azure Machine Learning (ML) na spúšťanie ML pipeline a registráciu modelov ako MCP nástrojov.

## Integrácia Azure OpenAI

Azure OpenAI poskytuje prístup k výkonným AI modelom ako GPT-4 a ďalším. Integrácia MCP s Azure OpenAI vám umožní využiť tieto modely pri zachovaní flexibility orchestrácie nástrojov MCP.

### Implementácia v C#

V tomto ukážkovom kóde demonštrujeme, ako integrovať MCP s Azure OpenAI pomocou Azure OpenAI SDK.

```csharp
// .NET Azure OpenAI Integration
using Microsoft.Mcp.Client;
using Azure.AI.OpenAI;
using Microsoft.Extensions.Configuration;
using System.Threading.Tasks;

namespace EnterpriseIntegration
{
    public class AzureOpenAiMcpClient
    {
        private readonly string _endpoint;
        private readonly string _apiKey;
        private readonly string _deploymentName;
        
        public AzureOpenAiMcpClient(IConfiguration config)
        {
            _endpoint = config["AzureOpenAI:Endpoint"];
            _apiKey = config["AzureOpenAI:ApiKey"];
            _deploymentName = config["AzureOpenAI:DeploymentName"];
        }
        
        public async Task<string> GetCompletionWithToolsAsync(string prompt, params string[] allowedTools)
        {
            // Create OpenAI client
            var client = new OpenAIClient(new Uri(_endpoint), new AzureKeyCredential(_apiKey));
            
            // Create completion options with tools
            var completionOptions = new ChatCompletionsOptions
            {
                DeploymentName = _deploymentName,
                Messages = { new ChatMessage(ChatRole.User, prompt) },
                Temperature = 0.7f,
                MaxTokens = 800
            };
            
            // Add tool definitions
            foreach (var tool in allowedTools)
            {
                completionOptions.Tools.Add(new ChatCompletionsFunctionToolDefinition
                {
                    Name = tool,
                    // In a real implementation, you'd add the tool schema here
                });
            }
            
            // Get completion response
            var response = await client.GetChatCompletionsAsync(completionOptions);
            
            // Handle tool calls in the response
            foreach (var toolCall in response.Value.Choices[0].Message.ToolCalls)
            {
                // Implementation to handle Azure OpenAI tool calls with MCP
                // ...
            }
            
            return response.Value.Choices[0].Message.Content;
        }
    }
}
```

V predchádzajúcom kóde sme:

- Nakonfigurovali klienta Azure OpenAI s endpointom, názvom nasadenia a API kľúčom.
- Vytvorili metódu `GetCompletionWithToolsAsync` na získavanie dokončení s podporou nástrojov.
- Spracovali volania nástrojov v odpovedi.

Odporúčame implementovať skutočnú logiku spracovania nástrojov podľa vášho konkrétneho nastavenia MCP servera.

## Integrácia Microsoft AI Foundry

Azure AI Foundry poskytuje platformu na tvorbu a nasadzovanie AI agentov. Integrácia MCP s AI Foundry vám umožní využiť jeho schopnosti pri zachovaní flexibility MCP.

V nasledujúcom kóde vyvíjame integráciu agenta, ktorý spracováva požiadavky a spracováva volania nástrojov pomocou MCP.

### Implementácia v Jave

```java
// Java AI Foundry Agent Integration
package com.example.mcp.enterprise;

import com.microsoft.aifoundry.AgentClient;
import com.microsoft.aifoundry.AgentToolResponse;
import com.microsoft.aifoundry.models.AgentRequest;
import com.microsoft.aifoundry.models.AgentResponse;
import com.mcp.client.McpClient;
import com.mcp.tools.ToolRequest;
import com.mcp.tools.ToolResponse;

public class AIFoundryMcpBridge {
    private final AgentClient agentClient;
    private final McpClient mcpClient;
    
    public AIFoundryMcpBridge(String aiFoundryEndpoint, String mcpServerUrl) {
        this.agentClient = new AgentClient(aiFoundryEndpoint);
        this.mcpClient = new McpClient.Builder()
            .setServerUrl(mcpServerUrl)
            .build();
    }
    
    public AgentResponse processAgentRequest(AgentRequest request) {
        // Process the AI Foundry Agent request
        AgentResponse initialResponse = agentClient.processRequest(request);
        
        // Check if the agent requested to use tools
        if (initialResponse.getToolCalls() != null && !initialResponse.getToolCalls().isEmpty()) {
            // For each tool call, route it to the appropriate MCP tool
            for (AgentToolCall toolCall : initialResponse.getToolCalls()) {
                String toolName = toolCall.getName();
                Map<String, Object> parameters = toolCall.getArguments();
                
                // Execute the tool using MCP
                ToolResponse mcpResponse = mcpClient.executeTool(toolName, parameters);
                
                // Create tool response for AI Foundry
                AgentToolResponse toolResponse = new AgentToolResponse(
                    toolCall.getId(),
                    mcpResponse.getResult()
                );
                
                // Submit tool response back to the agent
                initialResponse = agentClient.submitToolResponse(
                    request.getConversationId(), 
                    toolResponse
                );
            }
        }
        
        return initialResponse;
    }
}
```

V predchádzajúcom kóde sme:

- Vytvorili triedu `AIFoundryMcpBridge`, ktorá integruje AI Foundry a MCP.
- Implementovali metódu `processAgentRequest`, ktorá spracováva požiadavky AI Foundry agenta.
- Spracovali volania nástrojov vykonaním cez MCP klienta a odoslaním výsledkov späť AI Foundry agentovi.

## Integrácia MCP s Azure ML

Integrácia MCP s Azure Machine Learning (ML) vám umožní využiť výkonné ML schopnosti Azure pri zachovaní flexibility MCP. Táto integrácia sa dá použiť na spúšťanie ML pipeline, registráciu modelov ako nástrojov a správu výpočtových zdrojov.

### Implementácia v Pythone

```python
# Python Azure AI Integration
from mcp_client import McpClient
from azure.ai.ml import MLClient
from azure.identity import DefaultAzureCredential
from azure.ai.ml.entities import Environment, AmlCompute
import os
import asyncio

class EnterpriseAiIntegration:
    def __init__(self, mcp_server_url, subscription_id, resource_group, workspace_name):
        # Set up MCP client
        self.mcp_client = McpClient(server_url=mcp_server_url)
        
        # Set up Azure ML client
        self.credential = DefaultAzureCredential()
        self.ml_client = MLClient(
            self.credential,
            subscription_id,
            resource_group,
            workspace_name
        )
    
    async def execute_ml_pipeline(self, pipeline_name, input_data):
        """Executes an ML pipeline in Azure ML"""
        # First process the input data using MCP tools
        processed_data = await self.mcp_client.execute_tool(
            "dataPreprocessor",
            {
                "data": input_data,
                "operations": ["normalize", "clean", "transform"]
            }
        )
        
        # Submit the pipeline to Azure ML
        pipeline_job = self.ml_client.jobs.create_or_update(
            entity={
                "name": pipeline_name,
                "display_name": f"MCP-triggered {pipeline_name}",
                "experiment_name": "mcp-integration",
                "inputs": {
                    "processed_data": processed_data.result
                }
            }
        )
        
        # Return job information
        return {
            "job_id": pipeline_job.id,
            "status": pipeline_job.status,
            "creation_time": pipeline_job.creation_context.created_at
        }
    
    async def register_ml_model_as_tool(self, model_name, model_version="latest"):
        """Registers an Azure ML model as an MCP tool"""
        # Get model details
        if model_version == "latest":
            model = self.ml_client.models.get(name=model_name, label="latest")
        else:
            model = self.ml_client.models.get(name=model_name, version=model_version)
        
        # Create deployment environment
        env = Environment(
            name="mcp-model-env",
            conda_file="./environments/inference-env.yml"
        )
        
        # Set up compute
        compute = self.ml_client.compute.get("mcp-inference")
        
        # Deploy model as online endpoint
        deployment = self.ml_client.online_deployments.create_or_update(
            endpoint_name=f"mcp-{model_name}",
            deployment={
                "name": f"mcp-{model_name}-deployment",
                "model": model.id,
                "environment": env,
                "compute": compute,
                "scale_settings": {
                    "scale_type": "auto",
                    "min_instances": 1,
                    "max_instances": 3
                }
            }
        )
        
        # Create MCP tool schema based on model schema
        tool_schema = {
            "type": "object",
            "properties": {},
            "required": []
        }
        
        # Add input properties based on model schema
        for input_name, input_spec in model.signature.inputs.items():
            tool_schema["properties"][input_name] = {
                "type": self._map_ml_type_to_json_type(input_spec.type)
            }
            tool_schema["required"].append(input_name)
        
        # Register as MCP tool
        # In a real implementation, you would create a tool that calls the endpoint
        return {
            "model_name": model_name,
            "model_version": model.version,
            "endpoint": deployment.endpoint_uri,
            "tool_schema": tool_schema
        }
    
    def _map_ml_type_to_json_type(self, ml_type):
        """Maps ML data types to JSON schema types"""
        mapping = {
            "float": "number",
            "int": "integer",
            "bool": "boolean",
            "str": "string",
            "object": "object",
            "array": "array"
        }
        return mapping.get(ml_type, "string")
```

V predchádzajúcom kóde sme:

- Vytvorili triedu `EnterpriseAiIntegration`, ktorá integruje MCP s Azure ML.
- Implementovali metódu `execute_ml_pipeline`, ktorá spracováva vstupné dáta pomocou MCP nástrojov a spúšťa ML pipeline v Azure ML.
- Implementovali metódu `register_ml_model_as_tool`, ktorá registruje Azure ML model ako MCP nástroj, vrátane vytvorenia potrebného nasadenia a výpočtových zdrojov.
- Namapovali dátové typy Azure ML na JSON schému pre registráciu nástrojov.
- Použili asynchrónne programovanie na spracovanie potenciálne dlhých operácií, ako je spúšťanie ML pipeline a registrácia modelov.

## Čo ďalej

- [5.2 Multi modality](../mcp-multi-modality/README.md)

**Vyhlásenie o zodpovednosti**:  
Tento dokument bol preložený pomocou AI prekladateľskej služby [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, prosím, majte na pamäti, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Pôvodný dokument v jeho rodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.