<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "355b12a5970c5c9e6db0bee970c751ba",
  "translation_date": "2025-07-13T15:43:19+00:00",
  "source_file": "01-CoreConcepts/README.md",
  "language_code": "es"
}
-->
# 📖 Conceptos Básicos de MCP: Dominando el Protocolo de Contexto de Modelo para la Integración de IA

El [Model Context Protocol (MCP)](https://github.com/modelcontextprotocol) es un marco estandarizado y potente que optimiza la comunicación entre Modelos de Lenguaje Extensos (LLMs) y herramientas externas, aplicaciones y fuentes de datos. Esta guía optimizada para SEO te llevará a través de los conceptos fundamentales de MCP, asegurando que comprendas su arquitectura cliente-servidor, componentes esenciales, mecánicas de comunicación y mejores prácticas de implementación.

## Visión General

Esta lección explora la arquitectura fundamental y los componentes que conforman el ecosistema del Model Context Protocol (MCP). Aprenderás sobre la arquitectura cliente-servidor, los componentes clave y los mecanismos de comunicación que impulsan las interacciones de MCP.

## 👩‍🎓 Objetivos Clave de Aprendizaje

Al finalizar esta lección, podrás:

- Entender la arquitectura cliente-servidor de MCP.
- Identificar los roles y responsabilidades de Hosts, Clientes y Servidores.
- Analizar las características principales que hacen de MCP una capa de integración flexible.
- Aprender cómo fluye la información dentro del ecosistema MCP.
- Obtener conocimientos prácticos a través de ejemplos de código en .NET, Java, Python y JavaScript.

## 🔎 Arquitectura MCP: Un Análisis Más Profundo

El ecosistema MCP se basa en un modelo cliente-servidor. Esta estructura modular permite que las aplicaciones de IA interactúen de manera eficiente con herramientas, bases de datos, APIs y recursos contextuales. Desglosemos esta arquitectura en sus componentes principales.

En esencia, MCP sigue una arquitectura cliente-servidor donde una aplicación host puede conectarse a múltiples servidores:

```mermaid
flowchart LR
    subgraph "Your Computer"
        Host["Host with MCP VScode, IDEs, Tools)"]
        S1["MCP Server A"]
        S2["MCP Server B"]
        S3["MCP Server C"]
        Host <-->|"MCP Protocol"| S1
        Host <-->|"MCP Protocol"| S2
        Host <-->|"MCP Protocol"| S3
        S1 <--> D1[("Local\Data Source A")]
        S2 <--> D2[("Local\Data Source B")]
    end
    subgraph "Internet"
        S3 <-->|"Web APIs"| D3[("Remote\Services")]
    end
```

- **Hosts MCP**: Programas como VSCode, Claude Desktop, IDEs o herramientas de IA que desean acceder a datos a través de MCP
- **Clientes MCP**: Clientes del protocolo que mantienen conexiones 1:1 con los servidores
- **Servidores MCP**: Programas ligeros que exponen capacidades específicas mediante el estándar Model Context Protocol
- **Fuentes de Datos Locales**: Archivos, bases de datos y servicios de tu computadora a los que los servidores MCP pueden acceder de forma segura
- **Servicios Remotos**: Sistemas externos disponibles por internet a los que los servidores MCP pueden conectarse mediante APIs.

El Protocolo MCP es un estándar en evolución; puedes ver las últimas actualizaciones en la [especificación del protocolo](https://modelcontextprotocol.io/specification/2025-06-18/)

### 1. Hosts

En el Model Context Protocol (MCP), los Hosts juegan un papel crucial como la interfaz principal a través de la cual los usuarios interactúan con el protocolo. Los Hosts son aplicaciones o entornos que inician conexiones con servidores MCP para acceder a datos, herramientas y prompts. Ejemplos de Hosts incluyen entornos de desarrollo integrados (IDEs) como Visual Studio Code, herramientas de IA como Claude Desktop o agentes personalizados diseñados para tareas específicas.

**Hosts** son aplicaciones LLM que inician conexiones. Ellos:

- Ejecutan o interactúan con modelos de IA para generar respuestas.
- Inician conexiones con servidores MCP.
- Gestionan el flujo de la conversación y la interfaz de usuario.
- Controlan permisos y restricciones de seguridad.
- Manejan el consentimiento del usuario para compartir datos y ejecutar herramientas.

### 2. Clientes

Los Clientes son componentes esenciales que facilitan la interacción entre Hosts y servidores MCP. Actúan como intermediarios, permitiendo que los Hosts accedan y utilicen las funcionalidades proporcionadas por los servidores MCP. Desempeñan un papel clave para asegurar una comunicación fluida y un intercambio eficiente de datos dentro de la arquitectura MCP.

**Clientes** son conectores dentro de la aplicación host. Ellos:

- Envían solicitudes a los servidores con prompts/instrucciones.
- Negocian capacidades con los servidores.
- Gestionan las solicitudes de ejecución de herramientas desde los modelos.
- Procesan y muestran las respuestas a los usuarios.

### 3. Servidores

Los Servidores son responsables de manejar las solicitudes de los clientes MCP y proporcionar respuestas adecuadas. Gestionan diversas operaciones como recuperación de datos, ejecución de herramientas y generación de prompts. Los servidores aseguran que la comunicación entre clientes y Hosts sea eficiente y confiable, manteniendo la integridad del proceso de interacción.

**Servidores** son servicios que proveen contexto y capacidades. Ellos:

- Registran las características disponibles (recursos, prompts, herramientas)
- Reciben y ejecutan llamadas a herramientas desde el cliente
- Proporcionan información contextual para mejorar las respuestas del modelo
- Devuelven los resultados al cliente
- Mantienen el estado a lo largo de las interacciones cuando es necesario

Los servidores pueden ser desarrollados por cualquiera para ampliar las capacidades del modelo con funcionalidades especializadas.

### 4. Características del Servidor

Los servidores en el Model Context Protocol (MCP) ofrecen bloques fundamentales que permiten interacciones enriquecidas entre clientes, hosts y modelos de lenguaje. Estas características están diseñadas para potenciar las capacidades de MCP ofreciendo contexto estructurado, herramientas y prompts.

Los servidores MCP pueden ofrecer cualquiera de las siguientes características:

#### 📑 Recursos

Los recursos en el Model Context Protocol (MCP) abarcan varios tipos de contexto y datos que pueden ser utilizados por usuarios o modelos de IA. Estos incluyen:

- **Datos Contextuales**: Información y contexto que los usuarios o modelos de IA pueden aprovechar para la toma de decisiones y ejecución de tareas.
- **Bases de Conocimiento y Repositorios de Documentos**: Colecciones de datos estructurados y no estructurados, como artículos, manuales y trabajos de investigación, que proporcionan información valiosa.
- **Archivos y Bases de Datos Locales**: Datos almacenados localmente en dispositivos o dentro de bases de datos, accesibles para procesamiento y análisis.
- **APIs y Servicios Web**: Interfaces y servicios externos que ofrecen datos y funcionalidades adicionales, permitiendo la integración con diversos recursos y herramientas en línea.

Un ejemplo de recurso puede ser un esquema de base de datos o un archivo que se puede acceder de la siguiente manera:

```text
file://log.txt
database://schema
```

### 🤖 Prompts

Los prompts en el Model Context Protocol (MCP) incluyen diversas plantillas predefinidas y patrones de interacción diseñados para optimizar los flujos de trabajo del usuario y mejorar la comunicación. Estos incluyen:

- **Mensajes y Flujos de Trabajo Plantilla**: Mensajes y procesos preestructurados que guían a los usuarios a través de tareas e interacciones específicas.
- **Patrones de Interacción Predefinidos**: Secuencias estandarizadas de acciones y respuestas que facilitan una comunicación consistente y eficiente.
- **Plantillas de Conversación Especializadas**: Plantillas personalizables adaptadas para tipos específicos de conversaciones, asegurando interacciones relevantes y contextualmente apropiadas.

Una plantilla de prompt puede verse así:

```markdown
Generate a product slogan based on the following {{product}} with the following {{keywords}}
```

#### ⛏️ Herramientas

Las herramientas en el Model Context Protocol (MCP) son funciones que el modelo de IA puede ejecutar para realizar tareas específicas. Estas herramientas están diseñadas para ampliar las capacidades del modelo de IA proporcionando operaciones estructuradas y confiables. Aspectos clave incluyen:

- **Funciones para que el modelo de IA ejecute**: Las herramientas son funciones ejecutables que el modelo puede invocar para llevar a cabo diversas tareas.
- **Nombre y Descripción Únicos**: Cada herramienta tiene un nombre distinto y una descripción detallada que explica su propósito y funcionalidad.
- **Parámetros y Resultados**: Las herramientas aceptan parámetros específicos y devuelven resultados estructurados, garantizando resultados consistentes y predecibles.
- **Funciones Discretas**: Las herramientas realizan funciones específicas como búsquedas web, cálculos y consultas a bases de datos.

Un ejemplo de herramienta podría verse así:

```typescript
server.tool(
  "GetProducts",
  {
    pageSize: z.string().optional(),
    pageCount: z.string().optional()
  }, () => {
    // return results from API
  }
)
```

## Características del Cliente

En el Model Context Protocol (MCP), los clientes ofrecen varias características clave a los servidores, mejorando la funcionalidad general y la interacción dentro del protocolo. Una de las características destacadas es el muestreo (Sampling).

### 👉 Muestreo (Sampling)

- **Comportamientos Agentes Iniciados por el Servidor**: Los clientes permiten que los servidores inicien acciones o comportamientos específicos de forma autónoma, mejorando las capacidades dinámicas del sistema.
- **Interacciones Recursivas con LLMs**: Esta característica permite interacciones recursivas con modelos de lenguaje extensos (LLMs), posibilitando un procesamiento más complejo e iterativo de tareas.
- **Solicitud de Completaciones Adicionales del Modelo**: Los servidores pueden solicitar completaciones adicionales del modelo, asegurando que las respuestas sean completas y contextualmente relevantes.

## Flujo de Información en MCP

El Model Context Protocol (MCP) define un flujo estructurado de información entre hosts, clientes, servidores y modelos. Comprender este flujo ayuda a clarificar cómo se procesan las solicitudes de los usuarios y cómo se integran herramientas externas y datos en las respuestas del modelo.

- **El Host Inicia la Conexión**  
  La aplicación host (como un IDE o interfaz de chat) establece una conexión con un servidor MCP, típicamente vía STDIO, WebSocket u otro transporte soportado.

- **Negociación de Capacidades**  
  El cliente (integrado en el host) y el servidor intercambian información sobre las características, herramientas, recursos y versiones del protocolo que soportan. Esto asegura que ambas partes entiendan qué capacidades están disponibles para la sesión.

- **Solicitud del Usuario**  
  El usuario interactúa con el host (por ejemplo, ingresando un prompt o comando). El host recopila esta entrada y la pasa al cliente para su procesamiento.

- **Uso de Recursos o Herramientas**  
  - El cliente puede solicitar contexto o recursos adicionales al servidor (como archivos, entradas de base de datos o artículos de bases de conocimiento) para enriquecer la comprensión del modelo.
  - Si el modelo determina que se necesita una herramienta (por ejemplo, para obtener datos, realizar un cálculo o llamar a una API), el cliente envía una solicitud de invocación de herramienta al servidor, especificando el nombre de la herramienta y los parámetros.

- **Ejecución en el Servidor**  
  El servidor recibe la solicitud de recurso o herramienta, ejecuta las operaciones necesarias (como correr una función, consultar una base de datos o recuperar un archivo) y devuelve los resultados al cliente en un formato estructurado.

- **Generación de la Respuesta**  
  El cliente integra las respuestas del servidor (datos de recursos, resultados de herramientas, etc.) en la interacción continua con el modelo. El modelo usa esta información para generar una respuesta completa y contextualmente relevante.

- **Presentación del Resultado**  
  El host recibe la salida final del cliente y la presenta al usuario, a menudo incluyendo tanto el texto generado por el modelo como cualquier resultado de la ejecución de herramientas o consultas a recursos.

Este flujo permite que MCP soporte aplicaciones de IA avanzadas, interactivas y conscientes del contexto, conectando sin problemas modelos con herramientas externas y fuentes de datos.

## Detalles del Protocolo

MCP (Model Context Protocol) se construye sobre [JSON-RPC 2.0](https://www.jsonrpc.org/), proporcionando un formato de mensajes estandarizado y agnóstico al lenguaje para la comunicación entre hosts, clientes y servidores. Esta base permite interacciones confiables, estructuradas y extensibles a través de diversas plataformas y lenguajes de programación.

### Características Clave del Protocolo

MCP extiende JSON-RPC 2.0 con convenciones adicionales para la invocación de herramientas, acceso a recursos y gestión de prompts. Soporta múltiples capas de transporte (STDIO, WebSocket, SSE) y habilita una comunicación segura, extensible y agnóstica al lenguaje entre componentes.

#### 🧢 Protocolo Base

- **Formato de Mensajes JSON-RPC**: Todas las solicitudes y respuestas usan la especificación JSON-RPC 2.0, asegurando una estructura consistente para llamadas a métodos, parámetros, resultados y manejo de errores.
- **Conexiones con Estado**: Las sesiones MCP mantienen estado a lo largo de múltiples solicitudes, soportando conversaciones continuas, acumulación de contexto y gestión de recursos.
- **Negociación de Capacidades**: Durante la configuración de la conexión, clientes y servidores intercambian información sobre características soportadas, versiones del protocolo, herramientas y recursos disponibles. Esto asegura que ambas partes comprendan las capacidades del otro y puedan adaptarse en consecuencia.

#### ➕ Utilidades Adicionales

A continuación, algunas utilidades y extensiones del protocolo que MCP ofrece para mejorar la experiencia del desarrollador y habilitar escenarios avanzados:

- **Opciones de Configuración**: MCP permite la configuración dinámica de parámetros de sesión, como permisos de herramientas, acceso a recursos y ajustes del modelo, adaptados a cada interacción.
- **Seguimiento de Progreso**: Operaciones de larga duración pueden reportar actualizaciones de progreso, permitiendo interfaces de usuario más receptivas y mejor experiencia durante tareas complejas.
- **Cancelación de Solicitudes**: Los clientes pueden cancelar solicitudes en curso, permitiendo a los usuarios interrumpir operaciones que ya no son necesarias o que tardan demasiado.
- **Reporte de Errores**: Mensajes y códigos de error estandarizados ayudan a diagnosticar problemas, manejar fallos de forma elegante y proporcionar retroalimentación útil a usuarios y desarrolladores.
- **Registro de Logs**: Tanto clientes como servidores pueden emitir logs estructurados para auditoría, depuración y monitoreo de interacciones del protocolo.

Aprovechando estas características, MCP garantiza una comunicación robusta, segura y flexible entre modelos de lenguaje y herramientas o fuentes de datos externas.

### 🔐 Consideraciones de Seguridad

Las implementaciones de MCP deben adherirse a varios principios clave de seguridad para asegurar interacciones seguras y confiables:

- **Consentimiento y Control del Usuario**: Los usuarios deben proporcionar consentimiento explícito antes de que se acceda a cualquier dato o se realicen operaciones. Deben tener control claro sobre qué datos se comparten y qué acciones están autorizadas, apoyados por interfaces intuitivas para revisar y aprobar actividades.

- **Privacidad de Datos**: Los datos del usuario solo deben exponerse con consentimiento explícito y deben estar protegidos mediante controles de acceso adecuados. Las implementaciones MCP deben proteger contra transmisiones no autorizadas y asegurar que la privacidad se mantenga en todas las interacciones.

- **Seguridad de las Herramientas**: Antes de invocar cualquier herramienta, se requiere consentimiento explícito del usuario. Los usuarios deben entender claramente la funcionalidad de cada herramienta, y se deben aplicar límites de seguridad robustos para evitar ejecuciones no intencionadas o inseguras.

Siguiendo estos principios, MCP garantiza que la confianza, privacidad y seguridad del usuario se mantengan en todas las interacciones del protocolo.

## Ejemplos de Código: Componentes Clave

A continuación, ejemplos de código en varios lenguajes populares que ilustran cómo implementar componentes clave de servidores MCP y herramientas.

### Ejemplo en .NET: Creando un Servidor MCP Simple con Herramientas

Aquí tienes un ejemplo práctico en .NET que demuestra cómo implementar un servidor MCP simple con herramientas personalizadas. Este ejemplo muestra cómo definir y registrar herramientas, manejar solicitudes y conectar el servidor usando el Model Context Protocol.

```csharp
using System;
using System.Threading.Tasks;
using ModelContextProtocol.Server;
using ModelContextProtocol.Server.Transport;
using ModelContextProtocol.Server.Tools;

public class WeatherServer
{
    public static async Task Main(string[] args)
    {
        // Create an MCP server
        var server = new McpServer(
            name: "Weather MCP Server",
            version: "1.0.0"
        );
        
        // Register our custom weather tool
        server.AddTool<string, WeatherData>("weatherTool", 
            description: "Gets current weather for a location",
            execute: async (location) => {
                // Call weather API (simplified)
                var weatherData = await GetWeatherDataAsync(location);
                return weatherData;
            });
        
        // Connect the server using stdio transport
        var transport = new StdioServerTransport();
        await server.ConnectAsync(transport);
        
        Console.WriteLine("Weather MCP Server started");
        
        // Keep the server running until process is terminated
        await Task.Delay(-1);
    }
    
    private static async Task<WeatherData> GetWeatherDataAsync(string location)
    {
        // This would normally call a weather API
        // Simplified for demonstration
        await Task.Delay(100); // Simulate API call
        return new WeatherData { 
            Temperature = 72.5,
            Conditions = "Sunny",
            Location = location
        };
    }
}

public class WeatherData
{
    public double Temperature { get; set; }
    public string Conditions { get; set; }
    public string Location { get; set; }
}
```

### Ejemplo en Java: Componentes de Servidor MCP

Este ejemplo demuestra el mismo servidor MCP y registro de herramientas que el ejemplo en .NET anterior, pero implementado en Java.

```java
import io.modelcontextprotocol.server.McpServer;
import io.modelcontextprotocol.server.McpToolDefinition;
import io.modelcontextprotocol.server.transport.StdioServerTransport;
import io.modelcontextprotocol.server.tool.ToolExecutionContext;
import io.modelcontextprotocol.server.tool.ToolResponse;

public class WeatherMcpServer {
    public static void main(String[] args) throws Exception {
        // Create an MCP server
        McpServer server = McpServer.builder()
            .name("Weather MCP Server")
            .version("1.0.0")
            .build();
            
        // Register a weather tool
        server.registerTool(McpToolDefinition.builder("weatherTool")
            .description("Gets current weather for a location")
            .parameter("location", String.class)
            .execute((ToolExecutionContext ctx) -> {
                String location = ctx.getParameter("location", String.class);
                
                // Get weather data (simplified)
                WeatherData data = getWeatherData(location);
                
                // Return formatted response
                return ToolResponse.content(
                    String.format("Temperature: %.1f°F, Conditions: %s, Location: %s", 
                    data.getTemperature(), 
                    data.getConditions(), 
                    data.getLocation())
                );
            })
            .build());
        
        // Connect the server using stdio transport
        try (StdioServerTransport transport = new StdioServerTransport()) {
            server.connect(transport);
            System.out.println("Weather MCP Server started");
            // Keep server running until process is terminated
            Thread.currentThread().join();
        }
    }
    
    private static WeatherData getWeatherData(String location) {
        // Implementation would call a weather API
        // Simplified for example purposes
        return new WeatherData(72.5, "Sunny", location);
    }
}

class WeatherData {
    private double temperature;
    private String conditions;
    private String location;
    
    public WeatherData(double temperature, String conditions, String location) {
        this.temperature = temperature;
        this.conditions = conditions;
        this.location = location;
    }
    
    public double getTemperature() {
        return temperature;
    }
    
    public String getConditions() {
        return conditions;
    }
    
    public String getLocation() {
        return location;
    }
}
```

### Ejemplo en Python: Construyendo un Servidor MCP

En este ejemplo mostramos cómo construir un servidor MCP en Python. También se muestran dos formas diferentes de crear herramientas.

```python
#!/usr/bin/env python3
import asyncio
from mcp.server.fastmcp import FastMCP
from mcp.server.transports.stdio import serve_stdio

# Create a FastMCP server
mcp = FastMCP(
    name="Weather MCP Server",
    version="1.0.0"
)

@mcp.tool()
def get_weather(location: str) -> dict:
    """Gets current weather for a location."""
    # This would normally call a weather API
    # Simplified for demonstration
    return {
        "temperature": 72.5,
        "conditions": "Sunny",
        "location": location
    }

# Alternative approach using a class
class WeatherTools:
    @mcp.tool()
    def forecast(self, location: str, days: int = 1) -> dict:
        """Gets weather forecast for a location for the specified number of days."""
        # This would normally call a weather API forecast endpoint
        # Simplified for demonstration
        return {
            "location": location,
            "forecast": [
                {"day": i+1, "temperature": 70 + i, "conditions": "Partly Cloudy"}
                for i in range(days)
            ]
        }

# Instantiate the class to register its tools
weather_tools = WeatherTools()

# Start the server using stdio transport
if __name__ == "__main__":
    asyncio.run(serve_stdio(mcp))
```

### Ejemplo en JavaScript: Creando un Servidor MCP

Este ejemplo muestra la creación de un servidor MCP en JavaScript y cómo registrar dos herramientas relacionadas con el clima.

```javascript
// Using the official Model Context Protocol SDK
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod"; // For parameter validation

// Create an MCP server
const server = new McpServer({
  name: "Weather MCP Server",
  version: "1.0.0"
});

// Define a weather tool
server.tool(
  "weatherTool",
  {
    location: z.string().describe("The location to get weather for")
  },
  async ({ location }) => {
    // This would normally call a weather API
    // Simplified for demonstration
    const weatherData = await getWeatherData(location);
    
    return {
      content: [
        { 
          type: "text", 
          text: `Temperature: ${weatherData.temperature}°F, Conditions: ${weatherData.conditions}, Location: ${weatherData.location}` 
        }
      ]
    };
  }
);

// Define a forecast tool
server.tool(
  "forecastTool",
  {
    location: z.string(),
    days: z.number().default(3).describe("Number of days for forecast")
  },
  async ({ location, days }) => {
    // This would normally call a weather API
    // Simplified for demonstration
    const forecast = await getForecastData(location, days);
    
    return {
      content: [
        { 
          type: "text", 
          text: `${days}-day forecast for ${location}: ${JSON.stringify(forecast)}` 
        }
      ]
    };
  }
);

// Helper functions
async function getWeatherData(location) {
  // Simulate API call
  return {
    temperature: 72.5,
    conditions: "Sunny",
    location: location
  };
}

async function getForecastData(location, days) {
  // Simulate API call
  return Array.from({ length: days }, (_, i) => ({
    day: i + 1,
    temperature: 70 + Math.floor(Math.random() * 10),
    conditions: i % 2 === 0 ? "Sunny" : "Partly Cloudy"
  }));
}

// Connect the server using stdio transport
const transport = new StdioServerTransport();
server.connect(transport).catch(console.error);

console.log("Weather MCP Server started");
```

Este ejemplo en JavaScript demuestra cómo crear un cliente MCP que se conecta a un servidor, envía un prompt y procesa la respuesta incluyendo cualquier llamada a herramientas que se haya realizado.

## Seguridad y Autorización
MCP incluye varios conceptos y mecanismos integrados para gestionar la seguridad y la autorización a lo largo del protocolo:

1. **Control de Permisos de Herramientas**:  
  Los clientes pueden especificar qué herramientas puede usar un modelo durante una sesión. Esto garantiza que solo las herramientas explícitamente autorizadas estén accesibles, reduciendo el riesgo de operaciones no deseadas o inseguras. Los permisos pueden configurarse dinámicamente según las preferencias del usuario, las políticas organizacionales o el contexto de la interacción.

2. **Autenticación**:  
  Los servidores pueden requerir autenticación antes de otorgar acceso a herramientas, recursos u operaciones sensibles. Esto puede implicar claves API, tokens OAuth u otros esquemas de autenticación. Una autenticación adecuada asegura que solo clientes y usuarios confiables puedan invocar capacidades del lado del servidor.

3. **Validación**:  
  Se aplica validación de parámetros para todas las invocaciones de herramientas. Cada herramienta define los tipos, formatos y restricciones esperados para sus parámetros, y el servidor valida las solicitudes entrantes en consecuencia. Esto evita que entradas malformadas o maliciosas lleguen a las implementaciones de las herramientas y ayuda a mantener la integridad de las operaciones.

4. **Limitación de Tasa**:  
  Para prevenir abusos y asegurar un uso justo de los recursos del servidor, los servidores MCP pueden implementar limitación de tasa para llamadas a herramientas y acceso a recursos. Los límites pueden aplicarse por usuario, por sesión o de forma global, y ayudan a proteger contra ataques de denegación de servicio o consumo excesivo de recursos.

Al combinar estos mecanismos, MCP ofrece una base segura para integrar modelos de lenguaje con herramientas externas y fuentes de datos, al mismo tiempo que brinda a usuarios y desarrolladores un control detallado sobre el acceso y uso.

## Mensajes del Protocolo

La comunicación MCP utiliza mensajes JSON estructurados para facilitar interacciones claras y confiables entre clientes, servidores y modelos. Los principales tipos de mensajes incluyen:

- **Solicitud del Cliente**  
  Enviada desde el cliente al servidor, este mensaje típicamente incluye:
  - El prompt o comando del usuario
  - Historial de la conversación para contexto
  - Configuración y permisos de herramientas
  - Cualquier metadato adicional o información de sesión

- **Respuesta del Modelo**  
  Devuelta por el modelo (a través del cliente), este mensaje contiene:
  - Texto generado o completado basado en el prompt y contexto
  - Instrucciones opcionales para llamar a una herramienta si el modelo determina que debe invocarse una
  - Referencias a recursos o contexto adicional según sea necesario

- **Solicitud de Herramienta**  
  Enviada desde el cliente al servidor cuando se necesita ejecutar una herramienta. Este mensaje incluye:
  - El nombre de la herramienta a invocar
  - Parámetros requeridos por la herramienta (validados contra el esquema de la herramienta)
  - Información contextual o identificadores para rastrear la solicitud

- **Respuesta de Herramienta**  
  Devuelta por el servidor tras ejecutar una herramienta. Este mensaje proporciona:
  - Los resultados de la ejecución de la herramienta (datos estructurados o contenido)
  - Cualquier error o información de estado si la llamada a la herramienta falló
  - Opcionalmente, metadatos adicionales o registros relacionados con la ejecución

Estos mensajes estructurados aseguran que cada paso en el flujo de trabajo MCP sea explícito, rastreable y extensible, apoyando escenarios avanzados como conversaciones multi-turno, encadenamiento de herramientas y manejo robusto de errores.

## Puntos Clave

- MCP usa una arquitectura cliente-servidor para conectar modelos con capacidades externas
- El ecosistema está compuesto por clientes, hosts, servidores, herramientas y fuentes de datos
- La comunicación puede realizarse mediante STDIO, SSE o WebSockets
- Las herramientas son las unidades fundamentales de funcionalidad expuestas a los modelos
- Los protocolos de comunicación estructurados garantizan interacciones consistentes

## Ejercicio

Diseña una herramienta MCP simple que sería útil en tu área. Define:
1. Cómo se llamaría la herramienta
2. Qué parámetros aceptaría
3. Qué salida devolvería
4. Cómo un modelo podría usar esta herramienta para resolver problemas de los usuarios


---

## Qué sigue

Siguiente: [Capítulo 2: Seguridad](../02-Security/README.md)

**Aviso legal**:  
Este documento ha sido traducido utilizando el servicio de traducción automática [Co-op Translator](https://github.com/Azure/co-op-translator). Aunque nos esforzamos por la precisión, tenga en cuenta que las traducciones automáticas pueden contener errores o inexactitudes. El documento original en su idioma nativo debe considerarse la fuente autorizada. Para información crítica, se recomienda la traducción profesional realizada por humanos. No nos hacemos responsables de malentendidos o interpretaciones erróneas derivadas del uso de esta traducción.