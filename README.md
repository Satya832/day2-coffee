# ☕ Day 2 – Coffee Shop Barista Voice Agent

[![LiveKit](https://img.shields.io/badge/LiveKit-Agents-blue)](https://livekit.io/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-green)](https://openai.com/)
[![AssemblyAI](https://img.shields.io/badge/AssemblyAI-STT-orange)](https://www.assemblyai.com/)
[![Cartesia](https://img.shields.io/badge/Cartesia-TTS-purple)](https://cartesia.ai/)

This project is part of the **Murf AI + LiveKit "10 Days of Voice Agents" Challenge**.

A voice-driven coffee shop barista agent that takes customer orders through natural conversation. Built with LiveKit Agents, OpenAI, AssemblyAI, and Cartesia TTS, the agent acts as a friendly barista who collects drink preferences and saves orders to a local JSON file.

---

## 🎯 Overview

The Nebula Coffee barista agent engages customers in natural voice conversations to collect their coffee orders. It intelligently tracks order state, asks clarifying questions when needed, and saves completed orders locally.

### Key Capabilities

- **Natural Voice Interaction**: Speak your order naturally - no rigid commands needed
- **Smart Order Tracking**: Maintains order state and remembers all details
- **Intelligent Clarification**: Asks only necessary follow-up questions
- **Persistent Storage**: Saves all orders to JSONL format
- **Friendly Persona**: Behaves like a real barista from "Nebula Coffee"

---

## ✨ Features

### 🎤 Voice-Based Conversation
Users speak their orders naturally, and the agent responds with a friendly, conversational barista voice.

### 📊 Order State Tracking
The agent maintains a structured order object:

```json
{
  "drinkType": "string",
  "size": "string",
  "milk": "string",
  "extras": ["string"],
  "name": "string"
}
```

### 💬 Smart Clarifying Questions
The agent intelligently asks follow-up questions only for missing information, making the conversation feel natural and efficient.

### 💾 Automatic Order Saving
Every completed order is automatically saved to:
```
backend/orders_day2.jsonl
```

### 🎭 Authentic Barista Persona
The assistant embodies a polite, helpful barista from "Nebula Coffee" with a warm, welcoming personality.

---

## 🏗 Project Structure

```
day2-coffee/
│
├── backend/
│   ├── src/
│   │   ├── agent.py          # Main Barista Agent with LiveKit setup
│   │   ├── order_state.py    # Order data model and state management
│   │   └── tools.py          # Custom tools (update_order, save_order)
│   ├── .env.local            # Backend environment variables
│   ├── pyproject.toml        # Python dependencies
│   └── orders_day2.jsonl     # Stored orders (generated)
│
├── frontend/
│   ├── components/
│   │   └── CallInterface.tsx # LiveKit voice interface
│   ├── pages/
│   │   └── index.tsx         # Main page
│   ├── .env.local            # Frontend environment variables
│   ├── package.json          # Frontend dependencies
│   └── pnpm-lock.yaml
│
├── start_app.sh              # One-command startup script
├── README.md                 # This file
└── .gitignore
```

---

## 🛠 Tech Stack

### Backend
- **[LiveKit Agents](https://docs.livekit.io/agents/)** - Real-time voice agent framework
- **[AssemblyAI](https://www.assemblyai.com/)** - Speech-to-text transcription
- **[OpenAI GPT-4o-mini](https://openai.com/)** - Language model for conversation
- **[Cartesia Sonic-3](https://cartesia.ai/)** - Text-to-speech synthesis
- **Custom Tools** - Order management functions

### Frontend
- **[Next.js](https://nextjs.org/)** - React framework
- **[LiveKit Components](https://docs.livekit.io/reference/components/react/)** - Voice interface
- **[pnpm](https://pnpm.io/)** - Fast package manager
- **React UI** - Clean, modern interface

---

## 🚀 Quick Start

### Prerequisites

- **Node.js** 18+ and **pnpm** installed
- **Python** 3.11+ installed
- **uv** package manager for Python ([install](https://github.com/astral-sh/uv))
- API keys for:
  - LiveKit
  - OpenAI
  - Cartesia
  - AssemblyAI

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/Satya832/day2-coffee.git
cd day2-coffee
```

### 2️⃣ Backend Setup

```bash
cd backend

# Install dependencies
uv sync

# Create environment file
cp .env.example .env.local
```

**Edit `backend/.env.local` with your API keys:**

```env
LIVEKIT_URL=ws://localhost:7880
LIVEKIT_API_KEY=your_livekit_api_key
LIVEKIT_API_SECRET=your_livekit_api_secret
OPENAI_API_KEY=your_openai_api_key
CARTESIA_API_KEY=your_cartesia_api_key
ASSEMBLYAI_API_KEY=your_assemblyai_api_key
```

**Download required model files:**

```bash
uv run python src/agent.py download-files
```

### 3️⃣ Frontend Setup

```bash
cd ../frontend

# Install dependencies
pnpm install

# Create environment file
cp .env.example .env.local
```

**Edit `frontend/.env.local`:**

```env
NEXT_PUBLIC_LIVEKIT_URL=ws://localhost:7880
LIVEKIT_API_KEY=your_livekit_api_key
LIVEKIT_API_SECRET=your_livekit_api_secret
```

### 4️⃣ Run Everything

**Option A: One-Command Start (Recommended)**

Make the startup script executable and run it:

```bash
chmod +x start_app.sh
./start_app.sh
```

This will:
1. Start LiveKit server
2. Launch backend agent
3. Start frontend development server
4. Auto-open browser at `http://localhost:3000`

**Option B: Manual Start**

Open three separate terminal windows:

**Terminal 1 - LiveKit Server:**
```bash
livekit-server --dev
```

**Terminal 2 - Backend Agent:**
```bash
cd backend
uv run python src/agent.py dev
```

**Terminal 3 - Frontend:**
```bash
cd frontend
pnpm dev
```

Then open `http://localhost:3000` in your browser.

---

## 🎮 Usage

1. **Open the Application**: Navigate to `http://localhost:3000`
2. **Join the Call**: Click "Join Call" to connect to the voice agent
3. **Place Your Order**: Speak naturally - for example:
   - "Hi, I'd like a large cappuccino"
   - "Can I get an oat milk latte?"
   - "Medium americano with an extra shot, please"
4. **Answer Questions**: The agent will ask for any missing details
5. **Confirm**: Once complete, your order is saved automatically

### Example Conversation

**Customer**: "Hi, I'd like a latte"  
**Barista**: "Great choice! What size would you like - small, medium, or large?"  
**Customer**: "Medium please"  
**Barista**: "Perfect! What type of milk would you prefer?"  
**Customer**: "Oat milk, and can you add vanilla syrup?"  
**Barista**: "Of course! One medium oat milk latte with vanilla syrup. Can I get your name for the order?"  
**Customer**: "It's Sarah"  
**Barista**: "Wonderful! Your order is ready, Sarah. We'll have that medium oat milk latte with vanilla syrup ready shortly!"

---

## 📦 Order Data Format

Orders are saved in `backend/orders_day2.jsonl` with the following structure:

```json
{
  "timestamp": "2025-11-22T16:10:34Z",
  "drinkType": "latte",
  "size": "medium",
  "milk": "oat",
  "extras": ["vanilla syrup"],
  "name": "Sarah"
}
```

Each line is a complete JSON object representing one order.

### Example Orders File

```jsonl
{"timestamp": "2025-11-22T16:10:34Z", "drinkType": "latte", "size": "medium", "milk": "oat", "extras": ["vanilla syrup"], "name": "Sarah"}
{"timestamp": "2025-11-22T16:15:22Z", "drinkType": "cappuccino", "size": "large", "milk": "whole", "extras": [], "name": "Mike"}
{"timestamp": "2025-11-22T16:20:18Z", "drinkType": "americano", "size": "small", "milk": "none", "extras": ["extra shot"], "name": "Alex"}
```

---

## 🏆 Challenge Requirements

This project fulfills all requirements for Day 2 of the "10 Days of Voice Agents" challenge:

- ✅ **Friendly barista persona** - Natural, welcoming conversation style
- ✅ **Order state object** - Structured tracking of all order details
- ✅ **Clarifying questions** - Intelligent follow-ups until order is complete
- ✅ **JSON storage** - Orders saved to persistent JSONL file
- ✅ **Voice pipeline** - Full voice → LLM → voice implementation
- ✅ **Working UI** - Clean Next.js interface with LiveKit integration

---

## 🔧 Configuration

### Customizing the Agent

**Edit `backend/src/agent.py`** to customize:
- System prompt and personality
- Available drink options
- Order validation rules
- TTS voice settings

**Example voice customization:**

```python
tts = cartesia.TTS(
    voice="a0e99841-438c-4a64-b679-ae501e7d6091",  # Default barista voice
    # Or try other Cartesia voices:
    # voice="95856005-0332-41b0-935f-352e296aa0df",  # Different voice
)
```

### Adding New Drink Options

Modify the order state validation in `backend/src/order_state.py`:

```python
valid_drinks = ["espresso", "latte", "cappuccino", "americano", "mocha", "macchiato"]
valid_sizes = ["small", "medium", "large"]
valid_milks = ["whole", "skim", "oat", "almond", "soy", "none"]
```

---

## 🐛 Troubleshooting

### Backend won't start
- Verify all API keys are set in `.env.local`
- Check Python version: `python --version` (must be 3.11+)
- Reinstall dependencies: `uv sync --reinstall`

### Frontend connection issues
- Ensure LiveKit server is running
- Verify `NEXT_PUBLIC_LIVEKIT_URL` matches your LiveKit server
- Check browser console for errors

### No audio input/output
- Grant microphone permissions in your browser
- Check system audio settings
- Try a different browser (Chrome/Edge recommended)

### Orders not saving
- Check file permissions in `backend/` directory
- Verify the agent has write access
- Look for errors in backend terminal output

---

## 📝 Development

### Running Tests

```bash
cd backend
uv run pytest
```

### Code Formatting

```bash
# Backend
cd backend
uv run black src/
uv run isort src/

# Frontend
cd frontend
pnpm format
```

### Building for Production

```bash
# Frontend build
cd frontend
pnpm build
pnpm start
```

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is part of the Murf AI + LiveKit "10 Days of Voice Agents" Challenge.

---

## 🙏 Acknowledgments

- **[Murf AI](https://murf.ai/)** - For hosting the challenge
- **[LiveKit](https://livekit.io/)** - For the amazing real-time framework
- **[OpenAI](https://openai.com/)** - For powerful language models
- **[AssemblyAI](https://www.assemblyai.com/)** - For accurate speech recognition
- **[Cartesia](https://cartesia.ai/)** - For natural-sounding TTS

---

## 📧 Contact

**Satyabrata** - [GitHub](https://github.com/Satya832)

Project Link: [https://github.com/Satya832/day2-coffee](https://github.com/Satya832/day2-coffee)

---

## 🎯 What's Next?

Check out the other days in the "10 Days of Voice Agents" challenge:
- Day 1: [Project Name]
- **Day 2: Coffee Shop Barista (You are here!)**
- Day 3: Coming soon...

---

**Made with ☕ and 🎙️ for the Murf AI + LiveKit Challenge**
