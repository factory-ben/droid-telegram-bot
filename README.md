# Droid Telegram Bot

A Telegram bot that interfaces with [Factory's Droid CLI](https://factory.ai), allowing you to interact with Droid via Telegram messages.

## Features

- 💬 **Chat with Droid** - Send messages and get AI-powered responses
- ⚡ **Live Streaming** - Watch tool calls in real-time as Droid works
- 📂 **Session Management** - Persistent sessions with working directory context
- 🔐 **Access Control** - Restrict bot access to specific Telegram users
- 🔧 **Git Integration** - Quick `/git` commands for common operations

## Prerequisites

- Python 3.10+
- A [Factory](https://factory.ai) account and API key
- [Droid CLI](https://docs.factory.ai) installed
- Telegram bot token (from [@BotFather](https://t.me/botfather))
- Your Telegram user ID (from [@userinfobot](https://t.me/userinfobot))

## Quick Start

### 1. Install Droid CLI

```bash
# Install the Droid CLI
curl -fsSL https://factory.ai/install.sh | sh

# Verify installation
droid --version
```

### 2. Get a Factory API Key

1. Sign up at [factory.ai](https://factory.ai)
2. Go to Settings → API Keys
3. Create a new API key and copy it

### 3. Clone and Install

```bash
git clone https://github.com/factory-ben/droid-telegram-bot.git
cd droid-telegram-bot
pip install -r requirements.txt
```

### 4. Configure Environment

```bash
cp .env.example .env
# Edit .env with your values
```

Required environment variables:
- `FACTORY_API_KEY` - Your Factory API key (from step 2)
- `TELEGRAM_BOT_TOKEN` - Your bot token from BotFather
- `TELEGRAM_ALLOWED_USER_IDS` - Comma-separated Telegram user IDs

### 5. Run

```bash
# Direct
python bot.py

# Or with environment variables inline
TELEGRAM_BOT_TOKEN=your-token TELEGRAM_ALLOWED_USER_IDS=123456 python bot.py
```

## Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `FACTORY_API_KEY` | ✅ | - | Your Factory API key ([get one here](https://factory.ai)) |
| `TELEGRAM_BOT_TOKEN` | ✅ | - | Telegram bot token from @BotFather |
| `TELEGRAM_ALLOWED_USER_IDS` | ✅ | - | Comma-separated Telegram user IDs |
| `DROID_PATH` | ❌ | `droid` | Path to Droid CLI |
| `DROID_DEFAULT_CWD` | ❌ | `~` | Default working directory |
| `DROID_LOG_FILE` | ❌ | `/var/log/droid-telegram/bot.log` | Log file path |
| `DROID_SESSIONS_FILE` | ❌ | `/var/lib/droid-telegram/sessions.json` | Sessions file |

## Commands

| Command | Description |
|---------|-------------|
| `/start` | Welcome message and quick help |
| `/help` | Detailed help |
| `/new [path]` | Start new session (optionally in directory) |
| `/session` | List recent sessions |
| `/session <id>` | Switch to a session |
| `/cwd` | Show current working directory |
| `/stream` | Toggle live tool updates on/off |
| `/status` | Bot and Droid status |
| `/git [args]` | Run git commands in current directory |

## Usage Tips

- **Reply to continue** - Reply to any bot message to continue that session
- **Working directories** - Use `/new ~/projects/myapp` to set context
- **Live updates** - Watch Droid's progress with streaming enabled (default)
- **Permission prompts** - Bot shows Allow/Deny buttons for elevated permissions

## Production Deployment

### systemd Service

```bash
# Copy service file
sudo cp droid-telegram.service /etc/systemd/system/

# Edit with your environment variables
sudo systemctl edit droid-telegram

# Enable and start
sudo systemctl enable droid-telegram
sudo systemctl start droid-telegram
```

### Docker (coming soon)

```bash
docker run -e TELEGRAM_BOT_TOKEN=xxx -e TELEGRAM_ALLOWED_USER_IDS=123 droid-telegram
```

## Security Notes

- **Never commit tokens** - Use environment variables or `.env` files
- **Restrict access** - Always set `TELEGRAM_ALLOWED_USER_IDS`
- **Review permissions** - The bot can execute commands via Droid

## License

MIT License - see [LICENSE](LICENSE)

## Contributing

Contributions welcome! Please open an issue or PR.
