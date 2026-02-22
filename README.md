# Weather Skill for LarryBrain

Get current weather and forecasts for any location using free APIs.

## Features

- 🌤️ **Current weather** — Temperature, humidity, wind, conditions
- 📅 **3-day forecast** — Max/min temps, weather description
- 🌍 **Global support** — Any city name or coordinates
- 🔓 **No API keys** — Uses wttr.in and Open-Meteo (free)
- ⚡ **No rate limits** — Open-Meteo fallback available

## Installation

Install via LarryBrain marketplace or ask your agent:
```
install the weather skill
```

## Usage Examples

**Current weather:**
```
What's the weather in Tokyo?
Weather in New York right now
Is it raining in London?
```

**Forecast:**
```
Weather forecast for Paris this weekend
Will it rain tomorrow in Berlin?
3-day forecast for Sydney
```

## APIs Used

- **wttr.in** — Primary source, simple format
- **Open-Meteo** — Fallback, no rate limits

Both are free and require no API keys.

## Testing

Test the skill manually:
```bash
# Simple format
curl -s "wttr.in/Tokyo?format=3"

# Full JSON
curl -s "wttr.in/Tokyo?format=j1" | jq '.current_condition[0]'

# Forecast
curl -s "wttr.in/Tokyo?format=j1" | jq '.weather[]'
```

## License

MIT — Free to use and modify.
