# 🧊 Ice Breaker

**An intelligent ice breaker generator powered by LangChain and social media intelligence**

![Ice Breaker Demo](https://github.com/emarco177/ice_breaker/blob/main/static/demo.gif)

[![LangChain](https://img.shields.io/badge/LangChain-🦜🔗-brightgreen)](https://langchain.com/)
[![Tavily](https://img.shields.io/badge/Tavily-🔍-orange)](https://app.tavily.com/home?utm_campaign=eden_marco&utm_medium=socials&utm_source=linkedin)
[![Python](https://img.shields.io/badge/Python-3.8+-blue)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-2.0+-red)](https://flask.palletsprojects.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Udemy Course](https://img.shields.io/badge/LangChain%20Udemy%20Course-Coupon%20%2412.99-brightgreen)](https://www.udemy.com/course/langchain/?referralCode=AUGUST-2025)

## 🎯 Overview

**Ice Breaker** is a sophisticated AI-powered web application that creates personalized ice breakers by analyzing LinkedIn and Twitter profiles. This project serves as a comprehensive learning tool for mastering LangChain while building a practical generative AI application that combines social media intelligence with natural language generation.

### ✨ Key Features

**AI Pipeline Flow:**

1. 🔍 **Profile Discovery**: Intelligent lookup and discovery of LinkedIn and Twitter profiles
2. 🌐 **Data Extraction**: Advanced web scraping of professional and social media data
3. 🧠 **AI Analysis**: Deep analysis of personality, interests, and professional background
4. ✍️ **Ice Breaker Generation**: Context-aware creation of personalized conversation starters
5. 🎨 **Smart Formatting**: Professional presentation of generated content
6. 💬 **Interactive Interface**: User-friendly web interface powered by Flask
7. 🚀 **Real-time Processing**: Fast end-to-end pipeline from profile input to ice breaker output


_Watch Ice Breaker analyze social profiles and generate personalized conversation starters_

## 🛠️ Tech Stack

| Component | Technology | Description |
|-----------|------------|-------------|
| 🖥️ **Frontend** | Flask | Web application framework |
| 🧠 **AI Framework** | LangChain 🦜🔗 | Orchestrates the AI pipeline |
| 🔍 **LinkedIn Data** | Scrapin.io | Professional profile scraping |
| 🐦 **Twitter Data** | Twitter API | Social media content analysis |
| 🌐 **Web Search** | Tavily | Enhanced profile discovery |
| 🤖 **LLM** | OpenAI GPT | Powers the conversation generation |
| 📊 **Monitoring** | LangSmith | Optional tracing and debugging |
| 🐍 **Backend** | Python 3.8+ | Core application logic |

## 🚀 Quick Start

### Prerequisites

* Python 3.8 or higher
* OpenAI API key
* Scrapin.io API key
* Twitter API credentials
* Tavily API key

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/emarco177/ice_breaker.git
   cd ice_breaker
   ```

2. **Set up environment variables**
   
   Create a `.env` file in the root directory with your API keys (see [Environment Variables](#-environment-variables) section for details).

3. **Install dependencies**
   ```bash
   pipenv install
   ```

4. **Start the application**
   ```bash
   pipenv run app.py
   ```

5. **Open your browser** and navigate to `http://localhost:5000`

## 🧪 Testing

Run the test suite to ensure everything is working correctly:

```bash
pipenv run pytest .
```

## 💰 API Costs & Credits

> **📋 Note**: This project uses paid API services for optimal functionality:
> 
> - **[Scrapin.io](https://app.scrapin.io/auth/register)** 💼 - LinkedIn data scraping  
>   *[Sign up for API access](https://app.scrapin.io/auth/register)*
> 
> - **[Tavily](https://app.tavily.com/home?utm_campaign=eden_marco&utm_medium=socials&utm_source=linkedin)** 🌐 - Enhanced web search and profile discovery  
>   *[Sign up for Tavily API access](https://app.tavily.com/home?utm_campaign=eden_marco&utm_medium=socials&utm_source=linkedin)*
> 
> - **Twitter API** 🐦 - Social media content access  
>   *Paid service for accessing Twitter data*

> **⚠️ Important**: If you enable LangSmith tracing (`LANGCHAIN_TRACING_V2=true`), ensure you have a valid `LANGCHAIN_API_KEY`. Without it, the application will throw an error. If you don't need tracing, simply omit these variables.

## 📁 Project Structure

```
ice_breaker/
├── agents/                    # AI agents for profile lookup
│   ├── linkedin_lookup_agent.py
│   └── twitter_lookup_agent.py
├── chains/                    # LangChain custom chains
│   └── custom_chains.py
├── third_parties/            # External API integrations
│   ├── linkedin.py
│   └── twitter.py
├── tools/                    # Utility tools and functions
│   └── tools.py
├── templates/                # Flask HTML templates
│   └── index.html
├── static/                   # Static assets
│   ├── banner.jpeg
│   └── demo.gif
├── app.py                    # Flask application entry point
├── ice_breaker.py           # Core ice breaker logic
├── output_parsers.py        # Response formatting utilities
└── requirements files       # Pipfile, Pipfile.lock
```

## 🔧 Environment Variables

Create a `.env` file in the root directory:

```env
OPENAI_API_KEY=your_openai_api_key_here
SCRAPIN_API_KEY=your_scrapin_api_key_here
TAVILY_API_KEY=your_tavily_api_key_here

# Optional: Twitter scraping (only needed for the live scrape_user_tweets;
# the pipeline uses scrape_user_tweets_mock by default)
TWITTER_API_KEY=your_twitter_api_key_here
TWITTER_API_KEY_SECRET=your_twitter_api_key_secret_here
TWITTER_BEARER_TOKEN=your_twitter_bearer_token_here
TWITTER_ACCESS_TOKEN=your_twitter_access_token_here
TWITTER_ACCESS_TOKEN_SECRET=your_twitter_access_token_secret_here

# Optional: Enable LangSmith tracing
LANGCHAIN_TRACING_V2=true
LANGCHAIN_API_KEY=your_langsmith_api_key_here
LANGCHAIN_PROJECT=ice_breaker
```

> **⚠️ Important Note**: If you enable tracing by setting `LANGCHAIN_TRACING_V2=true`, you must have a valid LangSmith API key set in `LANGCHAIN_API_KEY`. Without a valid API key, the application will throw an error. If you don't need tracing, simply remove or comment out these environment variables.

| Variable | Description | Required |
|----------|-------------|----------|
| `OPENAI_API_KEY` | Your OpenAI API key for LLM access | ✅ |
| `SCRAPIN_API_KEY` | Scrapin.io API key for LinkedIn scraping | ✅ |
| `TAVILY_API_KEY` | Tavily API key for enhanced web search | ✅ |
| `TWITTER_API_KEY` | Twitter API key for social data access (optional) | ⚪ |
| `TWITTER_API_KEY_SECRET` | Twitter API key secret (optional) | ⚪ |
| `TWITTER_BEARER_TOKEN` | Twitter bearer token (optional) | ⚪ |
| `TWITTER_ACCESS_TOKEN` | Twitter access token (optional) | ⚪ |
| `TWITTER_ACCESS_TOKEN_SECRET` | Twitter access token secret (optional) | ⚪ |
| `LANGCHAIN_TRACING_V2` | Enable LangSmith tracing (optional) | ⚪ |
| `LANGCHAIN_API_KEY` | LangSmith API key (required if tracing enabled) | ⚪ |
| `LANGCHAIN_PROJECT` | LangSmith project name (optional) | ⚪ |

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## 📚 Learning Resources

This project is designed as a comprehensive learning tool for understanding:

* 🦜 **LangChain Framework** - Agent orchestration and chain composition
* 🔗 **API Integration** - Working with multiple external services
* 🧠 **AI Application Architecture** - Building production-ready AI systems
* 🌐 **Web Scraping** - Ethical data collection from social platforms
* 💬 **Natural Language Generation** - Context-aware content creation

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🌟 Support

If you find this project helpful, please consider:

* ⭐ Starring the repository
* 🐛 Reporting issues
* 💡 Contributing improvements
* 📢 Sharing with others
* 🎓 Taking the [LangChain Course](https://www.udemy.com/course/langchain/?referralCode=JJULY-2025)

---

### 🔗 Connect with Me

[![Portfolio](https://img.shields.io/badge/Portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://www.udemy.com/course/langchain/?referralCode=JJULY)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/eden-marco/)
[![Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://www.udemy.com/user/eden-marco/)

**Built with ❤️ by Eden Marco**

