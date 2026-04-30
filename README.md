# 🤖 RedQueen WhatsApp Bot

A production-ready WhatsApp automation bot with AI-powered responses, built with FastAPI, Evolution API, and React Dashboard.

## 📁 Project Structure

```
whatsapp-bot/
├── docker-compose.yml      # Main orchestration file
├── nginx.conf              # Reverse proxy config
├── .env.example            # Environment variables template
├── init.sql                # Database initialization
├── bot/                    # FastAPI Backend
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── main.py             # Main API & webhook handler
│   ├── database.py         # SQLAlchemy config
│   ├── models.py           # Database models
│   ├── config.py           # App settings
│   └── services/
│       ├── whatsapp.py     # Evolution API integration
│       ├── ai.py           # OpenAI GPT integration
│       └── scheduler.py    # Message scheduler
├── dashboard/              # React Admin Dashboard
│   ├── Dockerfile
│   ├── package.json
│   ├── public/
│   └── src/
│       ├── App.js
│       ├── index.js
│       ├── components/
│       │   └── Layout.js
│       └── pages/
│           ├── Dashboard.js
│           ├── Contacts.js
│           ├── Messages.js
│           ├── Broadcast.js
│           └── Settings.js
└── knowledge/              # Upload knowledge base files here
```

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose
- OpenAI API Key
- A server/VPS (Ubuntu recommended)
- Domain name (optional but recommended)

### 1. Clone & Setup

```bash
git clone <repo-url>
cd whatsapp-bot

# Copy environment file
cp .env.example .env

# Edit with your credentials
nano .env
```

### 2. Configure Environment Variables

Edit `.env`:
```env
OPENAI_API_KEY=sk-your-openai-api-key
ADMIN_NUMBER=5511999999999
SERVER_URL=https://yourdomain.com
WEBHOOK_SECRET=random-secret-string
```

### 3. Start Services

```bash
docker-compose up -d
```

This starts:
- **Evolution API** (port 8080) - WhatsApp connection
- **Bot Backend** (port 8000) - AI & logic
- **Dashboard** (port 3000) - Admin UI
- **PostgreSQL** (port 5432) - Database
- **Redis** (port 6379) - Cache & queues
- **Nginx** (port 80/443) - Reverse proxy

### 4. Connect WhatsApp

1. Open `http://your-server:8080`
2. Create an instance (name: `default`)
3. Scan the QR code with WhatsApp
4. Your bot is now connected!

### 5. Access Dashboard

Open `http://your-server:3000` to manage:
- View contacts & conversations
- Send manual messages
- Broadcast to multiple users
- Configure AI settings
- Upload knowledge base

## 🔧 Features

### Core Features
- ✅ **AI-Powered Replies** - GPT-4/3.5 responses
- ✅ **Conversation Memory** - Remembers context
- ✅ **Media Support** - Handles images, videos, audio, docs
- ✅ **Broadcast Messaging** - Send to multiple contacts
- ✅ **Scheduled Messages** - Set future deliveries
- ✅ **Contact Management** - Tags, notes, status
- ✅ **Real-time Chat** - Live message updates
- ✅ **Knowledge Base** - Upload docs for RAG

### Advanced Features
- ✅ **Sentiment Analysis** - Detects urgency & mood
- ✅ **Working Hours** - Auto-reply scheduling
- ✅ **Human Handover** - Escalate to admin
- ✅ **Analytics Dashboard** - Stats & insights
- ✅ **Webhook Security** - Signed requests
- ✅ **Docker Deploy** - One-command setup

## 📚 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Bot status |
| `/webhook/evolution` | POST | Receive WhatsApp events |
| `/api/v1/stats` | GET | Bot statistics |
| `/api/v1/contacts` | GET | List contacts |
| `/api/v1/contacts/{id}/messages` | GET | Contact messages |
| `/api/v1/send-message` | POST | Send manual message |
| `/api/v1/broadcast` | POST | Broadcast to multiple |
| `/api/v1/schedule-message` | POST | Schedule future message |
| `/api/v1/config` | GET/PUT | Bot configuration |
| `/api/v1/knowledge/upload` | POST | Upload knowledge file |

## 🧠 AI Configuration

### Custom System Prompt
Go to **Settings** → **Custom System Prompt** to override default behavior.

### Knowledge Base
Upload `.txt`, `.md`, or `.pdf` files to `/app/knowledge/` folder. The AI will use these for responses.

Example knowledge file:
```
Product: RedQueen Bot
Price: $99/month
Features: AI replies, scheduling, analytics
Support: support@redqueen.online
```

### Temperature Settings
- **0.1-0.3**: Factual, consistent responses
- **0.4-0.7**: Balanced (recommended)
- **0.8-1.0**: Creative, varied responses

## 🔒 Security

1. **Change default API keys** in docker-compose.yml
2. **Set strong webhook secret** in .env
3. **Use HTTPS** with SSL certificates
4. **Restrict Evolution API** to your server IP
5. **Enable firewall** (UFW):
```bash
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
```

## 🛠️ Troubleshooting

### Bot not responding?
```bash
# Check Evolution API status
curl http://localhost:8080/instance/connectionState/default

# Check logs
docker-compose logs -f evolution-api
docker-compose logs -f bot-backend
```

### Database issues?
```bash
# Reset database
docker-compose down -v
docker-compose up -d postgres
```

### QR Code not showing?
```bash
# Restart Evolution API
docker-compose restart evolution-api
```

## 📈 Scaling

For high-volume usage:
1. Use **Redis Cluster** for caching
2. Add **multiple Evolution API** instances
3. Use **PostgreSQL** with connection pooling
4. Deploy behind **load balancer**
5. Enable **CDN** for media files

## 💰 Costs

| Service | Cost |
|---------|------|
| VPS (2GB RAM) | $5-10/month |
| OpenAI API | ~$0.01-0.03 per message |
| Domain | $10-15/year |
| **Total** | **~$15-25/month** |

## 📄 License

MIT License - Free for personal and commercial use.

## 🆘 Support

- Issues: Open a GitHub issue
- Email: support@redqueen.online
- Discord: [Join our server]

---

Built with ❤️ by the RedQueen Team
