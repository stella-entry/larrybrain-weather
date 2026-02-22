# Weather

Get current weather and forecasts for any location using free APIs.

## What This Skill Does

Fetches weather data using wttr.in or Open-Meteo (no API key required).

## Capabilities

- **Current weather** — Temperature, conditions, humidity, wind
- **Forecast** — Up to 3 days ahead
- **Location support** — City names, coordinates, or "here" for current location

## How to Use

Ask your agent:
- "What's the weather in Tokyo?"
- "Weather forecast for New York this weekend"
- "Is it going to rain today?"

## Implementation

### Current Weather (wttr.in)

```bash
# Simple format
curl -s "wttr.in/Tokyo?format=3"
# Output: Tokyo: ⛅️ +15°C

# Full current conditions (JSON)
curl -s "wttr.in/Tokyo?format=j1" | jq '.current_condition[0] | {temp: .temp_C, feels: .FeelsLikeC, humidity: .humidity, wind: .windspeedKmph, desc: .weatherDesc[0].value}'
```

### Forecast

```bash
# 3-day forecast
curl -s "wttr.in/Tokyo?format=j1" | jq '.weather[] | {date: .date, max: .maxtempC, min: .mintempC, desc: .hourly[4].weatherDesc[0].value}'
```

### Alternative: Open-Meteo (no rate limits)

```bash
# Geocoding (get coordinates)
curl -s "https://geocoding-api.open-meteo.com/v1/search?name=Tokyo" | jq '.results[0] | {lat, lon}'

# Current weather
curl -s "https://api.open-meteo.com/v1/forecast?latitude=35.68&longitude=139.69&current_weather=true" | jq '.current_weather'

# Daily forecast
curl -s "https://api.open-meteo.com/v1/forecast?latitude=35.68&longitude=139.69&daily=temperature_2m_max,temperature_2m_min,weathercode&timezone=Asia/Tokyo" | jq '.daily'
```

## Example Output

**Current weather:**
```
Tokyo: 15°C, partly cloudy. Feels like 13°C. Humidity 65%. Wind 12 km/h.
```

**3-day forecast:**
```
Tokyo forecast:
- Today: 12-18°C, partly cloudy
- Tomorrow: 10-16°C, light rain
- Wednesday: 8-14°C, sunny
```

## Notes

- wttr.in has rate limits (~1 request/sec)
- Open-Meteo has no rate limits
- No API keys needed
- Works globally

## Error Handling

If location not found:
```
Location not found. Try a city name, country, or coordinates (e.g., "35.68,139.69").
```

## Security

- ✅ No API keys required
- ✅ No user data stored
- ✅ Public APIs only
