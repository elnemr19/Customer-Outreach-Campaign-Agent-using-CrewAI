# 📣 Customer Outreach Campaign using CrewAI

This project demonstrates how to create a powerful **multi-agent customer outreach system** using [CrewAI](https://github.com/joaomdmoura/crewAI), enhanced with custom tools and Google's **Gemini LLM**.

The agents are capable of **profiling leads** and **writing personalized outreach messages** based on real-time data, files, and sentiment analysis.

---

## 🚀 Project Overview

This system is composed of two collaborative AI agents:

1. 🕵️‍♂️ **Sales Representative Agent**
   - Identifies and researches high-value leads.
   - Uses tools like Google search and file reading to compile rich lead profiles.

2. 🧑‍💼 **Lead Sales Representative Agent**
   - Crafts personalized outreach campaigns.
   - Tailors communications to resonate with the lead’s values and recent milestones.

---

## 🧰 Tech Stack

- **Python 3.10 – 3.13**
- [CrewAI](https://github.com/joaomdmoura/crewAI)
- **Google Gemini LLM**
- Tools Used:
  - 🔍 `SerperDevTool` – Google Search capability
  - 📂 `DirectoryReadTool` – Reads local directories
  - 📄 `FileReadTool` – Parses local files
  - 😊 `SentimentAnalysisTool` – Custom tool for sentiment analysis

---

## 🔑 API Keys

Set your API keys as environment variables. This project uses:

`GEMINI_API_KEY` – for Google Gemini LLM

`GROQ_API_KEY` – (optional, for other models)

`SERPER_API_KEY` – for Google Search via Serper API

Example in Colab:

```python
import os
from google.colab import userdata

os.environ["GROQ_API_KEY"] = userdata.get('GROQ_API_KEY')
os.environ["GEMINI_API_KEY"] = userdata.get('GEMINI_API_KEY')
os.environ["SERPER_API_KEY"] = userdata.get('SERPER_API_KEY')
os.environ["OPENAI_API_KEY"] = userdata.get('Open_AI')
```

## 🧠 Agent Details

### 🔍 Sales Representative Agent

- **Role**: Identify high-value leads
- **Goal**: Analyze lead companies using multiple tools
- **Tools**:

`SerperDevTool`

`DirectoryReadTool`

`FileReadTool`

### ✉️ Lead Sales Representative Agent

- **Role**: Personalize communication for lead nurturing
- **Goal**: Convert leads into clients through compelling outreach
- **Tools**:

`SerperDevTool`

`SentimentAnalysisTool` (custom)

## 🛠️ Custom Tool: Sentiment Analysis
```python
class SentimentAnalysisTool(BaseTool):
    name = "Sentiment Analysis Tool"
    description = "Analyzes the sentiment of text to ensure positive and engaging communication."

    def _run(self, argument: str) -> str:
        return "positive"
```

## 📋 Example Task
```python
inputs = {
    "lead_name": "DeepLearningAI",
    "industry": "Online Learning Platform",
    "key_decision_maker": "Andrew Ng",
    "position": "CEO",
    "milestone": "product launch"
}

result = crew.kickoff(inputs=inputs)
```

This will output:

- 🧾 A comprehensive **lead profile** including key personnel, business developments, and pain points

- 📬 A **series of personalized email** drafts tailored for outreach to decision-makers

## 📄 Output Display (in Colab)

```python
from IPython.display import Markdown
import re

content = result.raw
markdown_content = re.sub(r'```(?:markdown)?\n?(.*?)\n?```', r'\1', content, flags=re.DOTALL).strip()
Markdown(markdown_content)
```

## ✅ Features
- 🎯 Lead profiling with real-time search

- 💬 Personalized communication generation

- 🔗 Tool-enhanced agent capabilities

- 🤖 Fully autonomous, end-to-end pipeline

- 📄 Markdown output ready for review or integration
