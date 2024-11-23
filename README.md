# LLM Tour Recommendation

An intelligent travel planning system that generates optimized daily schedules and recommendations for travelers in Busan using LangChain and multiple AI agents.

## 🌟 Features

- Dual-agent system for comprehensive travel planning:
  - Schedule Generator: Creates detailed daily itineraries
  - Recommendation Generator: Provides contextual travel tips and precautions
- Weather-aware planning that considers temperature, air quality, and conditions
- Dynamic scheduling based on attraction visit times
- GPU acceleration support for M1 Macs (MPS)

## 📋 Prerequisites

- Python 3.7+
- PyTorch
- LangChain
- Ollama

## 🚀 Installation

1. Clone the repository:
```bash
git clone https://github.com/Valiev-Koyiljon/LLM_TOUR_RECOMMENDATION.git
cd LLM_TOUR_RECOMMENDATION
```

2. Install required packages:
```bash
pip install torch langchain ollama
```

3. Install Ollama and download the llama3.2 model:
```bash
# Install Ollama (varies by OS)
curl https://ollama.ai/install.sh | sh

# Pull the model
ollama pull llama3.2
```

## 💻 Usage

The system takes weather data and attraction information to generate personalized travel plans. Here's a basic example:

```python

# Sample data
data = [{
    "date": "2024-10-05",
    "temp_high": 30,
    "temp_low": 14,
    "weather": "Windy",
    "air_quality": "Hazardous",
    "attractions": [
        {"name": "Haeundae Beach", "recommended_time": 2.98},
        {"name": "Gwangalli Beach", "recommended_time": 3.18},
        {"name": "Taejongdae", "recommended_time": 3.63},
        {"name": "Beomeosa Temple", "recommended_time": 2.4},
        {"name": "Gamcheon Culture Village", "recommended_time": 1.0}
    ]
}]

# Initialize agent and process the data
agent = initialize_agent(tools, llm, agent=AgentType.OPENAI_FUNCTIONS, verbose=True)
for entry in data:
    result = process_prompt(agent, entry["date"], entry["temp_high"], 
                          entry["temp_low"], entry["weather"], 
                          entry["air_quality"], entry["attractions"])
    print(result)
```

## 🏗️ System Architecture

The system consists of two main AI agents:

1. **Schedule Generator**
   - Creates detailed daily schedules
   - Considers weather conditions and attraction visit times
   - Optimizes the order of visits

2. **Recommendation Generator**
   - Provides weather-specific advice
   - Suggests precautions based on air quality
   - Offers tips for maximizing the travel experience

## 📝 Input Data Format

The system expects data in the following JSON format:

```json
{
    "date": "YYYY-MM-DD",
    "temp_high": float,
    "temp_low": float,
    "weather": string,
    "air_quality": string,
    "attractions": [
        {
            "name": string,
            "recommended_time": float
        }
    ]
}
```

## 🔧 Configuration

- GPU acceleration is automatically enabled for M1 Macs using MPS
- The system uses the llama3.2 model through Ollama
- Agent verbosity can be configured during initialization
