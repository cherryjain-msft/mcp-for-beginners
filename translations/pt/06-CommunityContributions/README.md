<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7b4b9bfacd2926725e6f1cda82bc8ff5",
  "translation_date": "2025-07-16T21:52:19+00:00",
  "source_file": "06-CommunityContributions/README.md",
  "language_code": "pt"
}
-->
# Comunidade e Contribuições

## Visão Geral

Esta lição foca-se em como envolver-se com a comunidade MCP, contribuir para o ecossistema MCP e seguir as melhores práticas para desenvolvimento colaborativo. Compreender como participar em projetos MCP open-source é essencial para quem pretende moldar o futuro desta tecnologia.

## Objetivos de Aprendizagem

No final desta lição, será capaz de:
- Compreender a estrutura da comunidade e do ecossistema MCP
- Participar eficazmente em fóruns e discussões da comunidade MCP
- Contribuir para repositórios open-source MCP
- Criar e partilhar ferramentas e servidores MCP personalizados
- Seguir as melhores práticas para desenvolvimento e colaboração MCP
- Descobrir recursos e frameworks comunitários para desenvolvimento MCP

## O Ecossistema da Comunidade MCP

O ecossistema MCP é composto por vários componentes e participantes que trabalham em conjunto para avançar o protocolo.

### Componentes Principais da Comunidade

1. **Mantenedores do Protocolo Core**: A organização oficial [Model Context Protocol GitHub](https://github.com/modelcontextprotocol) mantém as especificações core do MCP e as implementações de referência
2. **Desenvolvedores de Ferramentas**: Indivíduos e equipas que criam ferramentas e servidores MCP
3. **Fornecedores de Integração**: Empresas que integram o MCP nos seus produtos e serviços
4. **Utilizadores Finais**: Desenvolvedores e organizações que utilizam MCP nas suas aplicações
5. **Contribuidores**: Membros da comunidade que contribuem com código, documentação ou outros recursos

### Recursos da Comunidade

#### Canais Oficiais

- [Organização MCP no GitHub](https://github.com/modelcontextprotocol)
- [Documentação MCP](https://modelcontextprotocol.io/)
- [Especificação MCP](https://modelcontextprotocol.io/docs/specification)
- [Discussões no GitHub](https://github.com/orgs/modelcontextprotocol/discussions)
- [Repositório de Exemplos & Servidores MCP](https://github.com/modelcontextprotocol/servers)

#### Recursos Geridos pela Comunidade

- [Clientes MCP](https://modelcontextprotocol.io/clients) - Lista de clientes que suportam integrações MCP
- [Servidores MCP da Comunidade](https://github.com/modelcontextprotocol/servers?tab=readme-ov-file#-community-servers) - Lista crescente de servidores MCP desenvolvidos pela comunidade
- [Awesome MCP Servers](https://github.com/wong2/awesome-mcp-servers) - Lista selecionada de servidores MCP
- [PulseMCP](https://www.pulsemcp.com/) - Centro comunitário e newsletter para descobrir recursos MCP
- [Servidor Discord](https://discord.gg/jHEGxQu2a5) - Liga-te com desenvolvedores MCP
- Implementações SDK específicas por linguagem
- Publicações em blogs e tutoriais

## Contribuir para o MCP

### Tipos de Contribuições

O ecossistema MCP acolhe vários tipos de contribuições:

1. **Contribuições de Código**:
   - Melhorias no protocolo core
   - Correção de bugs
   - Implementações de ferramentas e servidores
   - Bibliotecas cliente/servidor em diferentes linguagens

2. **Documentação**:
   - Melhorar a documentação existente
   - Criar tutoriais e guias
   - Traduzir documentação
   - Criar exemplos e aplicações de demonstração

3. **Suporte à Comunidade**:
   - Responder a perguntas em fóruns e discussões
   - Testar e reportar problemas
   - Organizar eventos comunitários
   - Orientar novos contribuidores

### Processo de Contribuição: Protocolo Core

Para contribuir para o protocolo core MCP ou implementações oficiais, siga estes princípios das [diretrizes oficiais de contribuição](https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/CONTRIBUTING.md):

1. **Simplicidade e Minimalismo**: A especificação MCP mantém um padrão elevado para adicionar novos conceitos. É mais fácil adicionar coisas a uma especificação do que removê-las.

2. **Abordagem Concreta**: As alterações na especificação devem basear-se em desafios de implementação específicos, não em ideias especulativas.

3. **Fases de uma Proposta**:
   - Definir: Explorar o problema, validar que outros utilizadores MCP enfrentam o mesmo problema
   - Prototipar: Construir uma solução de exemplo e demonstrar a sua aplicação prática
   - Escrever: Com base no protótipo, redigir uma proposta de especificação

### Configuração do Ambiente de Desenvolvimento

```bash
# Fork the repository
git clone https://github.com/YOUR-USERNAME/modelcontextprotocol.git
cd modelcontextprotocol

# Install dependencies
npm install

# For schema changes, validate and generate schema.json:
npm run check:schema:ts
npm run generate:schema

# For documentation changes
npm run check:docs
npm run format

# Preview documentation locally (optional):
npm run serve:docs
```

### Exemplo: Contribuir com uma Correção de Bug

```javascript
// Original code with bug in the typescript-sdk
export function validateResource(resource: unknown): resource is MCPResource {
  if (!resource || typeof resource !== 'object') {
    return false;
  }
  
  // Bug: Missing property validation
  // Current implementation:
  const hasName = 'name' in resource;
  const hasSchema = 'schema' in resource;
  
  return hasName && hasSchema;
}

// Fixed implementation in a contribution
export function validateResource(resource: unknown): resource is MCPResource {
  if (!resource || typeof resource !== 'object') {
    return false;
  }
  
  // Improved validation
  const hasName = 'name' in resource && typeof (resource as MCPResource).name === 'string';
  const hasSchema = 'schema' in resource && typeof (resource as MCPResource).schema === 'object';
  const hasDescription = !('description' in resource) || typeof (resource as MCPResource).description === 'string';
  
  return hasName && hasSchema && hasDescription;
}
```

### Exemplo: Contribuir com uma Nova Ferramenta para a Biblioteca Standard

```python
# Example contribution: A CSV data processing tool for the MCP standard library

from mcp_tools import Tool, ToolRequest, ToolResponse, ToolExecutionException
import pandas as pd
import io
import json
from typing import Dict, Any, List, Optional

class CsvProcessingTool(Tool):
    """
    Tool for processing and analyzing CSV data.
    
    This tool allows models to extract information from CSV files,
    run basic analysis, and convert data between formats.
    """
    
    def get_name(self):
        return "csvProcessor"
        
    def get_description(self):
        return "Processes and analyzes CSV data"
    
    def get_schema(self):
        return {
            "type": "object",
            "properties": {
                "csvData": {
                    "type": "string", 
                    "description": "CSV data as a string"
                },
                "csvUrl": {
                    "type": "string",
                    "description": "URL to a CSV file (alternative to csvData)"
                },
                "operation": {
                    "type": "string",
                    "enum": ["summary", "filter", "transform", "convert"],
                    "description": "Operation to perform on the CSV data"
                },
                "filterColumn": {
                    "type": "string",
                    "description": "Column to filter by (for filter operation)"
                },
                "filterValue": {
                    "type": "string",
                    "description": "Value to filter for (for filter operation)"
                },
                "outputFormat": {
                    "type": "string",
                    "enum": ["json", "csv", "markdown"],
                    "default": "json",
                    "description": "Output format for the processed data"
                }
            },
            "oneOf": [
                {"required": ["csvData", "operation"]},
                {"required": ["csvUrl", "operation"]}
            ]
        }
    
    async def execute_async(self, request: ToolRequest) -> ToolResponse:
        try:
            # Extract parameters
            operation = request.parameters.get("operation")
            output_format = request.parameters.get("outputFormat", "json")
            
            # Get CSV data from either direct data or URL
            df = await self._get_dataframe(request)
            
            # Process based on requested operation
            result = {}
            
            if operation == "summary":
                result = self._generate_summary(df)
            elif operation == "filter":
                column = request.parameters.get("filterColumn")
                value = request.parameters.get("filterValue")
                if not column:
                    raise ToolExecutionException("filterColumn is required for filter operation")
                result = self._filter_data(df, column, value)
            elif operation == "transform":
                result = self._transform_data(df, request.parameters)
            elif operation == "convert":
                result = self._convert_format(df, output_format)
            else:
                raise ToolExecutionException(f"Unknown operation: {operation}")
            
            return ToolResponse(result=result)
        
        except Exception as e:
            raise ToolExecutionException(f"CSV processing failed: {str(e)}")
    
    async def _get_dataframe(self, request: ToolRequest) -> pd.DataFrame:
        """Gets a pandas DataFrame from either CSV data or URL"""
        if "csvData" in request.parameters:
            csv_data = request.parameters.get("csvData")
            return pd.read_csv(io.StringIO(csv_data))
        elif "csvUrl" in request.parameters:
            csv_url = request.parameters.get("csvUrl")
            return pd.read_csv(csv_url)
        else:
            raise ToolExecutionException("Either csvData or csvUrl must be provided")
    
    def _generate_summary(self, df: pd.DataFrame) -> Dict[str, Any]:
        """Generates a summary of the CSV data"""
        return {
            "columns": df.columns.tolist(),
            "rowCount": len(df),
            "columnCount": len(df.columns),
            "numericColumns": df.select_dtypes(include=['number']).columns.tolist(),
            "categoricalColumns": df.select_dtypes(include=['object']).columns.tolist(),
            "sampleRows": json.loads(df.head(5).to_json(orient="records")),
            "statistics": json.loads(df.describe().to_json())
        }
    
    def _filter_data(self, df: pd.DataFrame, column: str, value: str) -> Dict[str, Any]:
        """Filters the DataFrame by a column value"""
        if column not in df.columns:
            raise ToolExecutionException(f"Column '{column}' not found")
            
        filtered_df = df[df[column].astype(str).str.contains(value)]
        
        return {
            "originalRowCount": len(df),
            "filteredRowCount": len(filtered_df),
            "data": json.loads(filtered_df.to_json(orient="records"))
        }
    
    def _transform_data(self, df: pd.DataFrame, params: Dict[str, Any]) -> Dict[str, Any]:
        """Transforms the data based on parameters"""
        # Implementation would include various transformations
        return {
            "status": "success",
            "message": "Transformation applied"
        }
    
    def _convert_format(self, df: pd.DataFrame, format: str) -> Dict[str, Any]:
        """Converts the DataFrame to different formats"""
        if format == "json":
            return {
                "data": json.loads(df.to_json(orient="records")),
                "format": "json"
            }
        elif format == "csv":
            return {
                "data": df.to_csv(index=False),
                "format": "csv"
            }
        elif format == "markdown":
            return {
                "data": df.to_markdown(),
                "format": "markdown"
            }
        else:
            raise ToolExecutionException(f"Unsupported output format: {format}")
```

### Diretrizes para Contribuição

Para fazer uma contribuição bem-sucedida em projetos MCP:

1. **Comece Pequeno**: Inicie com documentação, correções de bugs ou pequenas melhorias
2. **Siga o Guia de Estilo**: Respeite o estilo de código e as convenções do projeto
3. **Escreva Testes**: Inclua testes unitários para as suas contribuições de código
4. **Documente o Seu Trabalho**: Adicione documentação clara para novas funcionalidades ou alterações
5. **Submeta PRs Focados**: Mantenha os pull requests focados numa única questão ou funcionalidade
6. **Interaja com o Feedback**: Seja receptivo ao feedback sobre as suas contribuições

### Exemplo de Fluxo de Trabalho para Contribuição

```bash
# Clone the repository
git clone https://github.com/modelcontextprotocol/typescript-sdk.git
cd typescript-sdk

# Create a new branch for your contribution
git checkout -b feature/my-contribution

# Make your changes
# ...

# Run tests to ensure your changes don't break existing functionality
npm test

# Commit your changes with a descriptive message
git commit -am "Fix validation in resource handler"

# Push your branch to your fork
git push origin feature/my-contribution

# Create a pull request from your branch to the main repository
# Then engage with feedback and iterate on your PR as needed
```

## Criar e Partilhar Servidores MCP

Uma das formas mais valiosas de contribuir para o ecossistema MCP é criar e partilhar servidores MCP personalizados. A comunidade já desenvolveu centenas de servidores para vários serviços e casos de uso.

### Frameworks para Desenvolvimento de Servidores MCP

Existem vários frameworks disponíveis para simplificar o desenvolvimento de servidores MCP:

1. **SDKs Oficiais**:
   - [TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)
   - [Python SDK](https://github.com/modelcontextprotocol/python-sdk)
   - [C# SDK](https://github.com/modelcontextprotocol/csharp-sdk)
   - [Go SDK](https://github.com/modelcontextprotocol/go-sdk)
   - [Java SDK](https://github.com/modelcontextprotocol/java-sdk)
   - [Kotlin SDK](https://github.com/modelcontextprotocol/kotlin-sdk)

2. **Frameworks da Comunidade**:
   - [MCP-Framework](https://mcp-framework.com/) - Construa servidores MCP com elegância e rapidez em TypeScript
   - [MCP Declarative Java SDK](https://github.com/codeboyzhou/mcp-declarative-java-sdk) - Servidores MCP orientados por anotações em Java
   - [Quarkus MCP Server SDK](https://github.com/quarkiverse/quarkus-mcp-server) - Framework Java para servidores MCP
   - [Next.js MCP Server Template](https://github.com/vercel-labs/mcp-for-next.js) - Projeto inicial Next.js para servidores MCP

### Desenvolvimento de Ferramentas Partilháveis

#### Exemplo .NET: Criar um Pacote de Ferramentas Partilhável

```csharp
// Create a new .NET library project
// dotnet new classlib -n McpFinanceTools

using Microsoft.Mcp.Tools;
using System.Threading.Tasks;
using System.Net.Http;
using System.Text.Json;

namespace McpFinanceTools
{
    // Stock quote tool
    public class StockQuoteTool : IMcpTool
    {
        private readonly HttpClient _httpClient;
        
        public StockQuoteTool(HttpClient httpClient = null)
        {
            _httpClient = httpClient ?? new HttpClient();
        }
        
        public string Name => "stockQuote";
        public string Description => "Gets current stock quotes for specified symbols";
        
        public object GetSchema()
        {
            return new {
                type = "object",
                properties = new {
                    symbol = new { 
                        type = "string",
                        description = "Stock symbol (e.g., MSFT, AAPL)" 
                    },
                    includeHistory = new { 
                        type = "boolean",
                        description = "Whether to include historical data",
                        default = false
                    }
                },
                required = new[] { "symbol" }
            };
        }
        
        public async Task<ToolResponse> ExecuteAsync(ToolRequest request)
        {
            // Extract parameters
            string symbol = request.Parameters.GetProperty("symbol").GetString();
            bool includeHistory = false;
            
            if (request.Parameters.TryGetProperty("includeHistory", out var historyProp))
            {
                includeHistory = historyProp.GetBoolean();
            }
            
            // Call external API (example)
            var quoteResult = await GetStockQuoteAsync(symbol);
            
            // Add historical data if requested
            if (includeHistory)
            {
                var historyData = await GetStockHistoryAsync(symbol);
                quoteResult.Add("history", historyData);
            }
            
            // Return formatted result
            return new ToolResponse {
                Result = JsonSerializer.SerializeToElement(quoteResult)
            };
        }
        
        private async Task<Dictionary<string, object>> GetStockQuoteAsync(string symbol)
        {
            // Implementation would call a real stock API
            // This is a simplified example
            return new Dictionary<string, object>
            {
                ["symbol"] = symbol,
                ["price"] = 123.45,
                ["change"] = 2.5,
                ["percentChange"] = 1.2,
                ["lastUpdated"] = DateTime.UtcNow
            };
        }
        
        private async Task<object> GetStockHistoryAsync(string symbol)
        {
            // Implementation would get historical data
            // Simplified example
            return new[]
            {
                new { date = DateTime.Now.AddDays(-7).Date, price = 120.25 },
                new { date = DateTime.Now.AddDays(-6).Date, price = 122.50 },
                new { date = DateTime.Now.AddDays(-5).Date, price = 121.75 }
                // More historical data...
            };
        }
    }
}

// Create package and publish to NuGet
// dotnet pack -c Release
// dotnet nuget push bin/Release/McpFinanceTools.1.0.0.nupkg -s https://api.nuget.org/v3/index.json -k YOUR_API_KEY
```

#### Exemplo Java: Criar um Pacote Maven para Ferramentas

```java
// pom.xml configuration for a shareable MCP tool package
<!-- 
<project>
    <groupId>com.example</groupId>
    <artifactId>mcp-weather-tools</artifactId>
    <version>1.0.0</version>
    
    <dependencies>
        <dependency>
            <groupId>com.mcp</groupId>
            <artifactId>mcp-server</artifactId>
            <version>1.0.0</version>
        </dependency>
    </dependencies>
    
    <distributionManagement>
        <repository>
            <id>github</id>
            <name>GitHub Packages</name>
            <url>https://maven.pkg.github.com/username/mcp-weather-tools</url>
        </repository>
    </distributionManagement>
</project>
-->

package com.example.mcp.weather;

import com.mcp.tools.Tool;
import com.mcp.tools.ToolRequest;
import com.mcp.tools.ToolResponse;
import com.mcp.tools.ToolExecutionException;

import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.URI;
import java.util.HashMap;
import java.util.Map;

public class WeatherForecastTool implements Tool {
    private final HttpClient httpClient;
    private final String apiKey;
    
    public WeatherForecastTool(String apiKey) {
        this.httpClient = HttpClient.newHttpClient();
        this.apiKey = apiKey;
    }
    
    @Override
    public String getName() {
        return "weatherForecast";
    }
    
    @Override
    public String getDescription() {
        return "Gets weather forecast for a specified location";
    }
    
    @Override
    public Object getSchema() {
        Map<String, Object> schema = new HashMap<>();
        // Schema definition...
        return schema;
    }
    
    @Override
    public ToolResponse execute(ToolRequest request) {
        try {
            String location = request.getParameters().get("location").asText();
            int days = request.getParameters().has("days") ? 
                request.getParameters().get("days").asInt() : 3;
            
            // Call weather API
            Map<String, Object> forecast = getForecast(location, days);
            
            // Build response
            return new ToolResponse.Builder()
                .setResult(forecast)
                .build();
        } catch (Exception ex) {
            throw new ToolExecutionException("Weather forecast failed: " + ex.getMessage(), ex);
        }
    }
    
    private Map<String, Object> getForecast(String location, int days) {
        // Implementation would call weather API
        // Simplified example
        Map<String, Object> result = new HashMap<>();
        // Add forecast data...
        return result;
    }
}

// Build and publish using Maven
// mvn clean package
// mvn deploy
```

#### Exemplo Python: Publicar um Pacote PyPI

```python
# Directory structure for a PyPI package:
# mcp_nlp_tools/
# ├── LICENSE
# ├── README.md
# ├── setup.py
# ├── mcp_nlp_tools/
# │   ├── __init__.py
# │   ├── sentiment_tool.py
# │   └── translation_tool.py

# Example setup.py
"""
from setuptools import setup, find_packages

setup(
    name="mcp_nlp_tools",
    version="0.1.0",
    packages=find_packages(),
    install_requires=[
        "mcp_server>=1.0.0",
        "transformers>=4.0.0",
        "torch>=1.8.0"
    ],
    author="Your Name",
    author_email="your.email@example.com",
    description="MCP tools for natural language processing tasks",
    long_description=open("README.md").read(),
    long_description_content_type="text/markdown",
    url="https://github.com/username/mcp_nlp_tools",
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
        "Operating System :: OS Independent",
    ],
    python_requires=">=3.8",
)
"""

# Example NLP tool implementation (sentiment_tool.py)
from mcp_tools import Tool, ToolRequest, ToolResponse, ToolExecutionException
from transformers import pipeline
import torch

class SentimentAnalysisTool(Tool):
    """MCP tool for sentiment analysis of text"""
    
    def __init__(self, model_name="distilbert-base-uncased-finetuned-sst-2-english"):
        # Load the sentiment analysis model
        self.sentiment_analyzer = pipeline("sentiment-analysis", model=model_name)
    
    def get_name(self):
        return "sentimentAnalysis"
        
    def get_description(self):
        return "Analyzes the sentiment of text, classifying it as positive or negative"
    
    def get_schema(self):
        return {
            "type": "object",
            "properties": {
                "text": {
                    "type": "string", 
                    "description": "The text to analyze for sentiment"
                },
                "includeScore": {
                    "type": "boolean",
                    "description": "Whether to include confidence scores",
                    "default": True
                }
            },
            "required": ["text"]
        }
    
    async def execute_async(self, request: ToolRequest) -> ToolResponse:
        try:
            # Extract parameters
            text = request.parameters.get("text")
            include_score = request.parameters.get("includeScore", True)
            
            # Analyze sentiment
            sentiment_result = self.sentiment_analyzer(text)[0]
            
            # Format result
            result = {
                "sentiment": sentiment_result["label"],
                "text": text
            }
            
            if include_score:
                result["score"] = sentiment_result["score"]
            
            # Return result
            return ToolResponse(result=result)
            
        except Exception as e:
            raise ToolExecutionException(f"Sentiment analysis failed: {str(e)}")

# To publish:
# python setup.py sdist bdist_wheel
# python -m twine upload dist/*
```

### Partilha de Boas Práticas

Ao partilhar ferramentas MCP com a comunidade:

1. **Documentação Completa**:
   - Documentar o propósito, uso e exemplos
   - Explicar parâmetros e valores de retorno
   - Documentar quaisquer dependências externas

2. **Gestão de Erros**:
   - Implementar tratamento robusto de erros
   - Fornecer mensagens de erro úteis
   - Tratar casos limite de forma adequada

3. **Considerações de Performance**:
   - Otimizar para velocidade e uso de recursos
   - Implementar caching quando apropriado
   - Considerar escalabilidade

4. **Segurança**:
   - Usar chaves API e autenticação seguras
   - Validar e sanitizar entradas
   - Implementar limitação de taxa para chamadas a APIs externas

5. **Testes**:
   - Incluir cobertura de testes abrangente
   - Testar com diferentes tipos de entrada e casos limite
   - Documentar procedimentos de teste

## Colaboração Comunitária e Melhores Práticas

A colaboração eficaz é fundamental para um ecossistema MCP próspero.

### Canais de Comunicação

- Issues e Discussões no GitHub
- Microsoft Tech Community
- Canais Discord e Slack
- Stack Overflow (tags: `model-context-protocol` ou `mcp`)

### Revisões de Código

Ao rever contribuições MCP:

1. **Clareza**: O código é claro e bem documentado?
2. **Correcção**: Funciona como esperado?
3. **Consistência**: Segue as convenções do projeto?
4. **Completude**: Inclui testes e documentação?
5. **Segurança**: Existem preocupações de segurança?

### Compatibilidade de Versões

Ao desenvolver para MCP:

1. **Versionamento do Protocolo**: Respeitar a versão do protocolo MCP que a sua ferramenta suporta
2. **Compatibilidade com Clientes**: Considerar compatibilidade retroativa
3. **Compatibilidade com Servidores**: Seguir as diretrizes de implementação de servidores
4. **Alterações Incompatíveis**: Documentar claramente quaisquer alterações incompatíveis

## Exemplo de Projeto Comunitário: Registo de Ferramentas MCP

Uma contribuição importante para a comunidade pode ser o desenvolvimento de um registo público para ferramentas MCP.

```python
# Example schema for a community tool registry API

from fastapi import FastAPI, HTTPException, Depends
from pydantic import BaseModel, Field, HttpUrl
from typing import List, Optional
import datetime
import uuid

# Models for the tool registry
class ToolSchema(BaseModel):
    """JSON Schema for a tool"""
    type: str
    properties: dict
    required: List[str] = []

class ToolRegistration(BaseModel):
    """Information for registering a tool"""
    name: str = Field(..., description="Unique name for the tool")
    description: str = Field(..., description="Description of what the tool does")
    version: str = Field(..., description="Semantic version of the tool")
    schema: ToolSchema = Field(..., description="JSON Schema for tool parameters")
    author: str = Field(..., description="Author of the tool")
    repository: Optional[HttpUrl] = Field(None, description="Repository URL")
    documentation: Optional[HttpUrl] = Field(None, description="Documentation URL")
    package: Optional[HttpUrl] = Field(None, description="Package URL")
    tags: List[str] = Field(default_factory=list, description="Tags for categorization")
    examples: List[dict] = Field(default_factory=list, description="Example usage")

class Tool(ToolRegistration):
    """Tool with registry metadata"""
    id: uuid.UUID = Field(default_factory=uuid.uuid4)
    created_at: datetime.datetime = Field(default_factory=datetime.datetime.now)
    updated_at: datetime.datetime = Field(default_factory=datetime.datetime.now)
    downloads: int = Field(default=0)
    rating: float = Field(default=0.0)
    ratings_count: int = Field(default=0)

# FastAPI application for the registry
app = FastAPI(title="MCP Tool Registry")

# In-memory database for this example
tools_db = {}

@app.post("/tools", response_model=Tool)
async def register_tool(tool: ToolRegistration):
    """Register a new tool in the registry"""
    if tool.name in tools_db:
        raise HTTPException(status_code=400, detail=f"Tool '{tool.name}' already exists")
    
    new_tool = Tool(**tool.dict())
    tools_db[tool.name] = new_tool
    return new_tool

@app.get("/tools", response_model=List[Tool])
async def list_tools(tag: Optional[str] = None):
    """List all registered tools, optionally filtered by tag"""
    if tag:
        return [tool for tool in tools_db.values() if tag in tool.tags]
    return list(tools_db.values())

@app.get("/tools/{tool_name}", response_model=Tool)
async def get_tool(tool_name: str):
    """Get information about a specific tool"""
    if tool_name not in tools_db:
        raise HTTPException(status_code=404, detail=f"Tool '{tool_name}' not found")
    return tools_db[tool_name]

@app.delete("/tools/{tool_name}")
async def delete_tool(tool_name: str):
    """Delete a tool from the registry"""
    if tool_name not in tools_db:
        raise HTTPException(status_code=404, detail=f"Tool '{tool_name}' not found")
    del tools_db[tool_name]
    return {"message": f"Tool '{tool_name}' deleted"}
```

## Principais Conclusões

- A comunidade MCP é diversa e acolhe vários tipos de contribuições
- Contribuir para MCP pode ir desde melhorias no protocolo core até ferramentas personalizadas
- Seguir as diretrizes de contribuição aumenta as hipóteses de aceitação do seu PR
- Criar e partilhar ferramentas MCP é uma forma valiosa de enriquecer o ecossistema
- A colaboração comunitária é essencial para o crescimento e melhoria do MCP

## Exercício

1. Identifique uma área no ecossistema MCP onde possa contribuir com base nas suas competências e interesses
2. Faça fork do repositório MCP e configure um ambiente de desenvolvimento local
3. Crie uma pequena melhoria, correção de bug ou ferramenta que beneficie a comunidade
4. Documente a sua contribuição com testes e documentação adequados
5. Submeta um pull request para o repositório apropriado

## Recursos Adicionais

- [Projetos da Comunidade MCP](https://github.com/topics/model-context-protocol)


---

Próximo: [Lições da Adoção Inicial](../07-LessonsfromEarlyAdoption/README.md)

**Aviso Legal**:  
Este documento foi traduzido utilizando o serviço de tradução automática [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos esforcemos pela precisão, por favor tenha em conta que traduções automáticas podem conter erros ou imprecisões. O documento original na sua língua nativa deve ser considerado a fonte autorizada. Para informações críticas, recomenda-se tradução profissional humana. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações incorretas decorrentes da utilização desta tradução.