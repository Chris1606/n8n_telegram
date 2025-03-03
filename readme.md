# Telegram Bot Automation with n8n 🤖

Create an AI-powered Telegram bot using n8n workflow automation. This guide walks through setting up n8n with Docker, exposing it via Ngrok, and connecting it to Telegram with AI capabilities.

## 🌟 Features
- Automated Telegram message processing
- Integration with AI models (cloud-based or local via Ollama)
- RAG capabilities using Pinecone vector database
- Memory buffer for conversation context

## 📋 Prerequisites
- [Docker](https://www.docker.com/) installed
- [Ngrok account](https://ngrok.com/)
- Telegram account
- [Pinecone account](https://www.pinecone.io/) (for RAG)
- [Ollama](https://ollama.ai/) installed (optional, for local AI)

## 🚀 Quick Setup

### 1. Expose Local Server with Ngrok
```bash
ngrok http 5678
```
Save the generated HTTPS URL (looks like https://abc123.ngrok.io)

---

### 2. Launch n8n with Docker
- Create persistent volume
```
docker volume create n8n_data
```
- Run container
```
docker run -it --name n8n \ -p 5678:5678 \ -v n8n_data:/home/node/.n8n \ -e WEBHOOK_URL="YOUR_NGROK_URL" \ docker.n8n.io/n8nio/n8n
```
- Access n8n UI at: http://localhost:5678
- 👉 Pro Tip: Create an account when prompted for unlimited workflows!
---
### 3. Create Telegram Bot
- Open Telegram and search for @BotFather

- Send /newbot and follow prompts

- Save your bot token (looks like 123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11)

---
# 🤖 Workflow Configuration
### 1. Telegram Node Setup 
- Add Telegram Trigger node

- Configure credentials with your bot token

- Select "Message" trigger type
### 2. AI Agent Configuration
- **System Prompt**: Define your bot's personality/role
- **AI Model**:
  - Cloud: Select from OpenAI, Anthropic, etc.
  - Local: Use Ollama endpoint `http://[YOUR_LOCAL_IP]:11434`
- **Memory**: Add conversation buffer
- **RAG Tools**:
  1. Pinecone DB connection (needs API key)
  2. Embedding model matching Pinecone dimensions
### 3. Output Configuration
- Add **Telegram Send Message** node connected to AI output
--- 
# 🔍 Testing & Validation
### 1. Activate workflow in n8n
### 2. Send message to your Telegram bot
### 3. Verify AI response in Telegram
--- 
# 🛠️ Troubleshooting Tips
### - Ensure Ngrok is running while testing

### - Check Docker logs: docker logs n8n

### - Verify API keys are correctly entered

### - Confirm Ollama is running for local models (ollama serve)
--- 
# How to Update n8n
```
  # Pull latest (stable) version
  docker pull docker.n8n.io/n8nio/n8n

  # Pull specific version
  docker pull docker.n8n.io/n8nio/n8n:1.81.0

  # Pull next (unstable) version
  docker pull docker.n8n.io/n8nio/n8n:next
```
After pulling the updated image, stop your n8n container and start it again. You can also use the command line. Replace <container_id> in the commands below with the container ID you find in the first command:
```
  # Find your container ID
  docker ps -a

  # Stop the container with the `<container_id>`
  docker stop <container_id>

  # Remove the container with the `<container_id>`
  docker rm <container_id>

  # Start the container
  docker run --name=<container_name> [options] -d docker.n8n.io/n8nio/n8n
```
If you run n8n using a Docker Compose file, follow these steps to update n8n:
```
  # Pull latest version
  docker compose pull

  # Stop and remove older version
  docker compose down

  # Start the container
  docker compose up -d
```
---
# 📚 Resources
- [n8n Documentation](https://docs.n8n.io/)
- [Pinecone Setup Guide](https://docs.pinecone.io/docs/quickstart)
- [Ollama Model Library](https://ollama.ai/library)