# ✈️ AI-Powered Travel Assistant & Recommendation Agent (Model Context Protocol - MCP & n8n)

> 🚀 **An enterprise-grade, decoupled AI architecture built using n8n and the Model Context Protocol (MCP)**, featuring an intelligent **Client Agent** equipped with conversation memory and LLM intelligence, interacting dynamically with an isolated **MCP Server** to fetch live external travel data (attractions, hotels, weather, dining, and currency rates).

---

## 🎯 Project Overview & Business Problem

Traditional travel chatbots rely on static data or lack the ability to cleanly separate tool execution from core reasoning logic, making them hard to scale or secure. 

This project solves these limitations by implementing a **Decoupled MCP Architecture**. The system is split into two distinct parts:
1. **The Client Workflow:** Houses the chat interface, **Groq Llama-3.3-70B AI Agent**, **Window Buffer Memory** for conversational context tracking, and an **MCP Client Tool** connection.
2. **The MCP Server Workflow:** Acts as a secure, dedicated microservice exposing specialized live tool endpoints (`Tourist Attraction`, `Hotel`, `Weather`, `Restaurant`, `Currency`) via OpenStreetMap Nominatim, wttr.in, and ExchangeRate APIs.

---

## 📊 Business Impact & Key Value Metrics

| 📈 Metric / Focus Area | 🛠️ Implementation Strategy | 💼 Business Value Delivered |
| :--- | :--- | :--- |
| **Decoupled Architecture** | Separation of Client Agent and MCP Server | Modular, secure, and easily maintainable tool scaling |
| **Contextual Personalization** | Window Buffer Memory Node | Remembers user budgets, hotel choices, and dietary preferences |
| **Real-Time Data Retrieval** | Live HTTP Request Tools via MCP Protocol | Eliminates outdated travel recommendations |
| **Advanced LLM Reasoning** | Groq Cloud `llama-3.3-70b-versatile` | Ultra-fast, context-aware travel itinerary generation |

---

## ⚙️ Workflow Architecture & Technical Flow

```text
┌────────────────────────────────────────────────────────────────────────┐
│ PART 1: AI TRAVEL CLIENT WORKFLOW                                      │
│                                                                        │
│  [Chat Trigger] ──► [AI Agent (Groq Llama-3.3)]                        │
│                           │         │              │                   │
│                           ▼         ▼              ▼                   │
│                     [Simple Memory] [Groq Model] [MCP Client Tool]     │
└─────────────────────────────────────┬──────────────────────────────────┘
                                      │ (MCP Protocol / SSE / Webhook)
                                      ▼
┌────────────────────────────────────────────────────────────────────────┐
│ PART 2: MCP SERVER WORKFLOW                                            │
│                                                                        │
│  [MCP Server Trigger] ──┬──► [Tourist Attraction Tool (OSM Nominatim)] │
│                         ├──► [Hotel Search Tool (OSM Nominatim)]       │
│                         ├──► [Weather Tool (wttr.in)]                  │
│                         ├──► [Restaurant Tool (OSM Nominatim)]         │
│                         └──► [Currency Conversion Tool (ExchangeRate)] │
└────────────────────────────────────────────────────────────────────────┘


🔍 Detailed Execution Steps & Processing Logic
1. 🤖 Part 1: The Client Intelligence Hub (Assignment 5 Client)
Chat Message Ingestion (When chat message received Node): Acts as the primary user entry point for queries (e.g., "Plan a trip to Cox's Bazar with a medium budget").

Contextual Memory (Simple Memory Node): Utilizes a Window Buffer Memory architecture to remember user preferences across sessions (Preferred Budget, Hotel Types, Transportation, Dietary Needs, and Activities).

LLM Core Engine (Groq Chat Model): Powered by llama-3.3-70b-versatile to process intent and formulate human-like responses.

MCP Client Bridge (MCP Client Node): Connects securely to the remote MCP server endpoint (https://salman00113.app.n8n.cloud/mcp/...) to discover and execute available tools dynamically.

2. 🔌 Part 2: The MCP Microservice Server (Assignment 5 Travel MCP server)
Server Trigger (MCP Server Trigger): Exposes a secure protocol entry point that listens to requests from the Client workflow.



Specialized Live Tools:

🏛️ Tourist Attraction Tool: Queries OpenStreetMap Nominatim to fetch landmarks, beaches, and sightseeing spots.

🏨 Hotel Tool: Retrieves nearby accommodation options and geographic coordinates.

⛅ Weather Tool: Pulls live meteorological conditions, temperature, and humidity via wttr.in.

🍽️ Restaurant Tool: Locates nearby dining options and local cuisine spots.

💱 Currency Tool: Fetches real-time exchange rate conversions using the ExchangeRate API.



🛠️ Tech Stack & Key Integrations
⚙️ Workflow Orchestrator: n8n (LangChain Agents, MCP Client/Server Nodes)

🤖 AI & LLM Infrastructure: Groq Cloud (llama-3.3-70b-versatile)

🌐 APIs & Data Providers: OpenStreetMap Nominatim, wttr.in, ExchangeRate API

🔄 Communication Protocol: Model Context Protocol (MCP)


💡 Consultant Mindset & Technical Edge
🧠 Why Choose a Decoupled MCP Architecture?

🔹 Enterprise Scalability: By keeping tools in a separate MCP server workflow, new data connectors can be added or modified without altering the core AI Agent client logic.

🔹 Persistent User Profiling: The integration of buffer memory allows the agent to build long-term user preference profiles, offering hyper-personalized travel itineraries over time.

🔹 Dynamic Tool Discovery: The MCP client-server standard enables the AI agent to query and invoke external tools on demand based strictly on user intent.