# 🤖 AI Snowflake Telegram Bot

> Ask questions in plain English. Get Snowflake query results — instantly, in Telegram.

[![n8n](https://img.shields.io/badge/Built%20with-n8n-orange?style=flat-square)](https://n8n.io)
[![Snowflake](https://img.shields.io/badge/Database-Snowflake-29B5E8?style=flat-square)](https://snowflake.com)
[![Telegram](https://img.shields.io/badge/Interface-Telegram-2CA5E0?style=flat-square)](https://telegram.org)
[![LLM](https://img.shields.io/badge/LLM-Kimi%20K2.5%20via%20OpenRouter-purple?style=flat-square)](https://openrouter.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)

---

## 💡 What It Does

Send a natural language message to your Telegram bot — it converts it into a Snowflake SQL query, executes it, and sends back the results with a plain-English explanation. No SQL knowledge required.

**Example:**

> **You:** What is the average account balance?
>
> **Bot:** The average account balance is **$4,231.00**
>
> *This query calculates the mean value of `C_ACCTBAL` across all customers in the CUSTOMER table.*

---

## 🏗️ Architecture

```
Telegram Message
      ↓
  n8n Workflow
      ↓
  AI Agent (Kimi K2.5 via OpenRouter)
      ↓
  SQL Generation + Validation
      ↓
  Snowflake Query Execution
      ↓
  Telegram Response (Results + Explanation)
```

---

## ✨ Features

- 🗣️ **Natural language to SQL** — no query writing needed
- ⚡ **Automatic execution** — queries run instantly against Snowflake
- 🔒 **Read-only safety** — only `SELECT`, `SHOW`, and `DESCRIBE` are permitted
- 💬 **Human-readable responses** — results come with plain-English explanations
- 📱 **Telegram interface** — accessible from any device
- 🔧 **Built on n8n** — fully visual, low-code workflow

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Automation | [n8n](https://n8n.io) |
| Database | [Snowflake](https://snowflake.com) |
| LLM | Moonshot Kimi K2.5 (via [OpenRouter](https://openrouter.ai)) |
| Interface | Telegram Bot API |
| Logic | JavaScript (n8n Code Node) |

---

## 🚀 Getting Started

### Prerequisites

- [n8n](https://n8n.io) (self-hosted or cloud)
- A [Snowflake](https://snowflake.com) account
- A [Telegram Bot Token](https://core.telegram.org/bots#botfather) (from @BotFather)
- An [OpenRouter](https://openrouter.ai) API key

---

### 1. Install n8n

**Via npm:**
```bash
npm install n8n -g
n8n start
```

**Via Docker:**
```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

---

### 2. Import the Workflow

1. Open your n8n instance at `http://localhost:5678`
2. Go to **Workflows → Import from File**
3. Select `workflow/n8n-snowflake-ai-bot.json`

---

### 3. Configure Credentials

In n8n, set up the following credentials:

| Credential | Where to Get It |
|-----------|----------------|
| **Telegram Bot Token** | [@BotFather](https://t.me/BotFather) on Telegram |
| **Snowflake** | Your Snowflake account settings |
| **OpenRouter API Key** | [openrouter.ai/keys](https://openrouter.ai/keys) |

---

### 4. Activate the Workflow

Toggle the workflow to **Active** and send a message to your Telegram bot to test it.

---

## 🔄 Workflow Steps

| Step | Node | Description |
|------|------|-------------|
| 1 | **Telegram Trigger** | Listens for incoming messages |
| 2 | **AI Agent** | Generates SQL from natural language using an LLM |
| 3 | **Code Node** | Parses the AI's JSON output — extracts SQL query and explanation template |
| 4 | **Snowflake Node** | Executes the generated SQL query |
| 5 | **Telegram Response** | Sends results and explanation back to the user |

---

## 🔐 Security

The AI agent is strictly restricted to **read-only** SQL operations.

| ✅ Allowed | ❌ Blocked |
|-----------|----------|
| `SELECT` | `INSERT` |
| `SHOW` | `UPDATE` |
| `DESCRIBE` | `DELETE` |
| | `DROP` |
| | `ALTER` |
| | `MERGE` |

Any request that attempts to generate a mutating query will be rejected before execution.

---

## 💬 Example Queries

```
What is the average account balance?
How many customers are in the database?
Describe the CUSTOMER table
Show me 5 sample rows from CUSTOMER
What are the distinct market segments?
Which customers have the highest account balance?
```

---

## 🗂️ Project Structure

```
ai-snowflake-telegram-bot/
├── workflow/
│   └── n8n-snowflake-ai-bot.json    # n8n workflow export
├── README.md
└── LICENSE
```

---

## 🔭 Roadmap

- [ ] Multi-table join query support
- [ ] Query validation layer before execution
- [ ] Chart/visualization responses (via image generation)
- [ ] Slack and WhatsApp integration
- [ ] Query history per user
- [ ] Role-based access control

---

## 🤝 Contributing

Contributions are welcome! Please open an issue first to discuss what you'd like to change.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -m 'Add my feature'`)
4. Push to the branch (`git push origin feature/my-feature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgements

- [n8n](https://n8n.io) for the automation backbone
- [Moonshot AI](https://www.moonshot.cn) for Kimi K2.5
- [OpenRouter](https://openrouter.ai) for unified LLM access
- [Snowflake](https://snowflake.com) for the data warehouse layer
