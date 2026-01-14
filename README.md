# AI Stock Analyzer

A simple, fast, web-first stock analysis application that provides AI-powered buy/sell recommendations based on fundamental and technical analysis.

## Features

- Real-time stock data from Finnhub API
- Fundamental analysis (revenue growth, EPS, P/E ratio, ROE, etc.)
- Technical analysis (moving averages, RSI, momentum)
- AI-powered recommendation engine
- Web-first with React Native/Expo
- Cross-platform support (Web, iOS, Android)

## Project Structure

```
/src               # Unified source directory
  /components      # React Native UI components
  /screens         # Main app screens
  /services        # API services (Finnhub, etc.)
  /analysis        # Analysis logic (fundamental, technical)
  App.tsx          # React Native app entry point
  server.js        # Express server entry point

package.json       # Unified dependencies
.env.example       # Environment variables template
```

## Setup Instructions

### Prerequisites

- Node.js (v16 or higher)
- npm or yarn
- Expo CLI (`npm install -g @expo/cli`)

### Setup

1. Install dependencies:
   ```bash
   npm install
   ```

2. Create `.env` file from `.env.example`:
   ```bash
   cp .env.example .env
   ```

3. Add your Finnhub API key to `.env`:
   ```
   FINNHUB_API_KEY=your_api_key_here
   PORT=3001
   ```

4. Start the backend server:
   ```bash
   npm run server
   ```

5. In a new terminal, start the frontend:
   ```bash
   npm run web
   ```

### Getting API Keys

1. Sign up for a free account at [Finnhub](https://finnhub.io/)
2. Get your API key from the dashboard
3. Add it to your `.env` file

## API Endpoints

### POST /analyze

Analyzes a stock ticker and returns recommendation.

**Request:**
```json
{
  "ticker": "AAPL"
}
```

**Response:**
```json
{
  "ticker": "AAPL",
  "companyName": "Apple Inc",
  "price": 150.25,
  "fundamentalScore": 4,
  "technicalScore": 3,
  "recommendation": "BUY TODAY",
  "reasoning": [
    "Strong revenue and EPS growth",
    "Price above key moving averages",
    "RSI in healthy range"
  ]
}
```

## Analysis Logic

### Fundamental Analysis (0-5 score)
- Revenue growth positive → +1
- EPS growth > 10% → +1
- ROE > 15% → +1
- Debt/Equity < 1 → +1
- Reasonable P/E ratio → +1

### Technical Analysis (0-5 score)
- 50 DMA > 200 DMA → +1
- Price above 50 DMA → +1
- RSI 40-65 range → +1
- Positive 3-month momentum → +1
- Volume confirmation → +1

### Decision Engine
- **BUY TODAY**: Fundamental ≥ 4, Technical ≥ 3, RSI < 70
- **DO NOT BUY TODAY**: Weak fundamentals or overbought conditions

## Technology Stack

- **Frontend**: React Native, Expo, TypeScript
- **Backend**: Node.js, Express
- **APIs**: Finnhub (primary stock data)
- **Deployment**: Web-first, cross-platform ready

## License

MIT License
