# Deltecho Bot Setup Guide

Deltecho Bot is an AI-powered DeltaChat bot that integrates Claude AI with secure, decentralized messaging.

## Features

- 🔐 End-to-end encrypted messaging via DeltaChat
- 🤖 Claude AI-powered responses with bash command execution
- 💬 Context-aware conversations (maintains conversation history per chat)
- 🛠️ Coding assistant capabilities with tool use
- 📧 Works over email infrastructure (no additional server needed)

## Prerequisites

- Node.js version 18 or higher
- A valid email account for the bot
- Anthropic API key

## Installation

1. Clone the repository and install dependencies:
```bash
npm install
```

2. Build the project:
```bash
npm run build
```

## Configuration

You need to set up two things:

### 1. Anthropic API Key

Set your Anthropic API key as an environment variable:
```bash
export ANTHROPIC_KEY=your_anthropic_api_key_here
```

### 2. DeltaChat Email Credentials

You have two options:

#### Option A: Regular Email Account
```bash
export ADDR=your-bot-email@example.com
export MAIL_PW=your_email_password
```

#### Option B: Chatmail (Recommended for Testing)

[Chatmail](https://github.com/deltachat/chatmail) is a server configuration optimized for Delta Chat with fast setup:

```bash
export CHATMAIL_QR=dcaccount:https://nine.testrun.org/new
```

## Running the Bot

Start the bot with:
```bash
npm run start:deltecho
```

Or directly:
```bash
node dist/deltecho-bot.js
```

On the first run, you'll need to provide credentials:
```bash
ANTHROPIC_KEY=sk-xxx ADDR=bot@example.com MAIL_PW=password npm run start:deltecho
```

Or with Chatmail:
```bash
ANTHROPIC_KEY=sk-xxx CHATMAIL_QR=dcaccount:https://nine.testrun.org/new npm run start:deltecho
```

## Usage

1. After starting the bot, it will display:
   - The bot's email address
   - A verification QR code

2. In your Delta Chat app:
   - Add the bot's email as a contact
   - Scan the verification QR code (especially important for Chatmail)
   - Start sending messages!

3. The bot will:
   - Respond to your messages using Claude AI
   - Execute bash commands when needed for coding tasks
   - Maintain conversation context within each chat

## Example Conversations

```
You: Can you help me create a Python script to list files?
Bot: [Provides code and can execute it to show results]

You: What files are in the current directory?
Bot: [Executes ls command and shows results]

You: Can you explain how async/await works in JavaScript?
Bot: [Provides explanation]
```

## Data Storage

The bot stores its data in the `deltachat-data` directory, which includes:
- Account configuration
- Message database
- Encryption keys

**Important**: Keep this directory secure and backed up!

## Security Notes

- Messages are end-to-end encrypted between you and the bot
- The bot operator (you) can see all messages
- Bash commands are executed with the bot's user permissions
- Be cautious about what commands you ask the bot to run

## Troubleshooting

### Bot doesn't respond
- Check that ANTHROPIC_KEY is set correctly
- Verify email credentials are correct
- Check the console for error messages

### Can't connect on Chatmail
- Make sure to scan the verification QR code
- Both you and the bot need to be on compatible instances

### Build errors
- Ensure Node.js version is 18 or higher
- Delete `node_modules` and `package-lock.json`, then run `npm install` again

## Architecture

The bot integrates two main components:

1. **DeltaChat Interface**: Handles secure messaging over email
   - Uses JSON-RPC API for communication
   - Manages encryption and message routing
   - Stores conversation data locally

2. **Claude AI Agent**: Provides intelligent responses
   - Maintains conversation history per chat
   - Can execute bash commands via tool use
   - Handles errors gracefully

## Development

To modify the bot:

1. Edit `src/deltecho-bot.ts`
2. Rebuild with `npm run build`
3. Test your changes

## Credits

Based on:
- [deltachat-bot/echo](https://github.com/deltachat-bot/echo) - Echo bot example
- [DeltaChat](https://delta.chat/) - Secure messaging platform
- The original mini-agent in this repository

## License

Same as the parent repository.
