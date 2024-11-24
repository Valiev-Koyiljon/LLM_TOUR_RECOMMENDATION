

# LLM Tour Recommendation

An intelligent travel planning system that generates optimized daily schedules and recommendations for travelers in Busan using LangChain and multiple AI agents.

## 🌟 Features

- **Dual-Agent System**:
  - **Schedule Generator**: Crafts detailed daily itineraries based on attraction visit times.
  - **Recommendation Generator**: Offers contextual travel tips and weather precautions.
- **Weather-Aware Planning**: Adapts to temperature, air quality, and weather conditions.
- **Dynamic Scheduling**: Adjusts plans for optimal travel experiences.
- **GPU Acceleration**: Supports M1 Macs with Metal Performance Shaders (MPS).

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

The system processes weather data and attraction information to create personalized travel plans. Here's an example:

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

The system leverages two key AI agents:

1. **Schedule Generator**
   - Designs efficient daily schedules.
   - Considers weather and attraction visit times.
   - Optimizes visit order for convenience.

2. **Recommendation Generator**
   - Provides weather-specific advice.
   - Recommends precautions based on air quality.
   - Shares tips to enhance travel enjoyment.

## 📝 Input Data Format

Input data should follow this JSON structure:

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

- GPU acceleration is enabled for M1 Macs via MPS.
- The system utilizes the llama3.2 model through Ollama.
- Agent verbosity is adjustable during initialization.

