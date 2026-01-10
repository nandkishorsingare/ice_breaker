# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

IceBreaker is an AI-powered Flask application that generates personalized conversation starters by analyzing LinkedIn and Twitter profiles using LangChain. This is a learning project for mastering LangChain through building a practical generative AI application.

## Development Commands

### Package Management (Pipenv)
- **Install dependencies**: `pipenv install`
- **Run the application**: `pipenv run app.py`
- **Run tests**: `pipenv run pytest .`

### Code Quality
- **Linting**: `pylint` (configured)
- **Formatting**: `black` (configured)
- **Import sorting**: `isort` (configured)

## Architecture

### Core Processing Pipeline

The application follows a linear AI pipeline orchestrated by `ice_breaker.py:ice_break_with()`:

1. **Profile Discovery** (`agents/`): ReAct agents use Tavily search to find LinkedIn/Twitter URLs
   - `linkedin_lookup_agent.py`: GPT-4o-mini + Tavily for LinkedIn profile lookup
   - `twitter_lookup_agent.py`: Similar pattern for Twitter profile discovery

2. **Data Extraction** (`third_parties/`): External API integrations
   - `linkedin.py`: Scrapin.io API for LinkedIn profile scraping
   - `twitter.py`: Tweepy API for Twitter data (includes mock data option)

3. **AI Analysis** (`chains/custom_chains.py`): Three separate LangChain chains
   - `get_summary_chain()`: Generates professional summary and interesting facts
   - `get_interests_chain()`: Identifies potential conversation topics
   - `get_ice_breaker_chain()`: Creates personalized ice breakers

4. **Response Formatting** (`output_parsers.py`): Pydantic models for structured output
   - `Summary`, `TopicOfInterest`, `IceBreaker` models
   - Auto-serialization to dictionary for JSON API responses

5. **Web Interface** (`app.py`): Flask app with single `/process` endpoint

### LangChain Integration Patterns

**ReAct Agents**: Used for profile lookup with tool-based reasoning
- Pattern: Agent → Tool (Tavily search) → Observable action

**Chain Composition**: Independent chains for different AI tasks
- Each chain takes `{information, twitter_posts}` as input
- Returns typed Pydantic models for type safety

**Output Parsing**: All LLM outputs use Pydantic for structure
- Enables automatic validation and serialization
- Prevents response format issues

### Environment Variables

Required in `.env`:
```env
OPENAI_API_KEY=                 # LLM access
SCRAPIN_API_KEY=                # LinkedIn scraping
TAVILY_API_KEY=                 # Profile discovery search
```

Optional:
```env
TWITTER_API_KEY=                # Twitter API (if using real Twitter data)
TWITTER_API_SECRET=
TWITTER_ACCESS_TOKEN=
TWITTER_ACCESS_SECRET=

LANGCHAIN_TRACING_V2=true       # Enable LangSmith tracing
LANGCHAIN_API_KEY=              # Required if tracing enabled
LANGCHAIN_PROJECT=ice_breaker
```

**⚠️ Critical**: If `LANGCHAIN_TRACING_V2=true`, you must provide a valid `LANGCHAIN_API_KEY` or the app will error.

## Key Technical Details

### Mock Data for Testing
- Twitter scraper includes `scrape_user_tweets_mock()` function
- Used in main pipeline (`ice_breaker.py:25`) to avoid API costs during development
- Switch to `scrape_user_tweets()` for real Twitter data

### Flask Application Structure
- Single-page app with vanilla JavaScript frontend
- Static files in `static/`, templates in `templates/`
- MVP CSS framework for styling
- Real-time processing with loading states

### Python Version
- **Required**: Python 3.10 (specified in Pipfile)
- Application tested on 3.8+ but Pipfile locks to 3.10

## GitHub Integration

### Context7 MCP Server
The repository uses Context7 for accessing LangChain documentation via Claude Code:
- Integrated in `.github/workflows/claude.yml`
- Provides up-to-date package documentation
- **Usage**: When working with LangChain, use the context7 MCP server to get latest docs

### Automated Workflows
- **claude.yml**: `@claude` trigger on issues/PRs for code assistance
- **claude-code-review.yml**: Automatic PR reviews on all pull requests

### Triggering Claude
- Mention `@claude` in issues, PRs, or review comments
- Claude has access to Context7 MCP for documentation lookup
- Allowed tools: `mcp__context7__resolve-library-id`, `mcp__context7__get-library-docs`

## Development Notes

### LangChain Development
When making changes to LangChain code:
1. Use Context7 MCP server to access latest LangChain documentation
2. Check ReAct agent patterns in `agents/` before modifying lookup logic
3. Ensure Pydantic models in `output_parsers.py` match expected LLM outputs
4. Test chains individually before integrating into main pipeline

### Adding New Features
- **New AI chains**: Add to `chains/custom_chains.py`, follow existing pattern
- **New data sources**: Create module in `third_parties/`, follow LinkedIn/Twitter patterns
- **New output types**: Add Pydantic model in `output_parsers.py`, update pipeline

### API Cost Management
- All external APIs have costs (OpenAI, Scrapin, Tavily, Twitter)
- Use mock data functions during development when possible
- Consider rate limits and implement caching if adding frequent calls
- I like to eat Pizza