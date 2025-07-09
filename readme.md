# 🧠 MCP Twitter Bot

An example project demonstrating how to build a **Model Context Protocol (MCP) server and client** that uses **Google Gemini** to post tweets (formerly on Twitter, now X) and run dynamic tools.

🚀 Built with:

* @modelcontextprotocol/sdk
* @google/genai
* twitter-api-v2
* Node.js, Express, dotenv

---

## ✨ Features

* Interactive CLI chat that uses Google Gemini to understand user prompts.
* MCP tools dynamically listed and called via Gemini.
* Posts tweets using Twitter API.
* Real-time communication with the server via Server-Sent Events (SSE).
* Easy to extend: add your own tools quickly.

---

## 📂 Project Structure

```
.
├── client
│ ├── node_modules/
│ ├── .env
│ ├── index.js
│ ├── package-lock.json
│ └── package.json
│
├── server
│ ├── node_modules/
│ ├── .env
│ ├── index.js
│ ├── mcp.tool.js
│ ├── package-lock.json
│ └── package.json
│

```

---

## 🛠 Installation

1. Clone the repository:

```
https://github.com/Zaki-Mohd/mcp-x-poster.git
cd mcp-x-poster
```

2. Install dependencies:

```
npm install
```

3. Configure environment variables:
   Create a `.env` file in the root folder and add:

```
GEMINI_API_KEY=your_google_gemini_api_key

TWITTER_API_KEY=your_twitter_api_key
TWITTER_API_SECRET=your_twitter_api_secret
TWITTER_ACCESS_TOKEN=your_twitter_access_token
TWITTER_ACCESS_TOKEN_SECRET=your_twitter_access_token_secret
```

⚠️ Make sure not to commit `.env` to version control.

---

## 🚀 Running the project

1️⃣ Start the MCP server:

```
npx nodemon index.js
```

2️⃣ Start the MCP client (in a separate terminal):

```
node index.js
```

The client will prompt for your message; Google Gemini decides whether to answer directly or call a tool like `createPost`.

---

## ⚙️ How it works

* The MCP server exposes tools:

  * `createPost`: posts a tweet
  * `addTwoNumbers`: simple math tool for testing
* The MCP client:

  * Lists tools from the server
  * Sends chat history and tool list to Google Gemini
  * If Gemini returns a `functionCall`, the client calls the tool on the server and includes the result in the next request

This loop creates a dynamic, AI-assisted workflow.

---

## 🧩 Adding your own tools

In `index.js`, add a new tool like this:

```js
server.tool(
  "toolName",
  "Tool description",
  {
    param1: z.string(), // validate parameters with zod
    param2: z.number()
  },
  async (args) => {
    // Your logic here
    return {
      content: [
        { type: "text", text: "Result text" }
      ]
    }
  }
)
```

The client will automatically discover it via `listTools()`.

---

## 📦 Requirements

* Node.js v18 or newer
* Twitter Developer credentials (API keys & tokens)
* Google Gemini API key

---



## ❤️ Contributing

PRs and suggestions are welcome!

