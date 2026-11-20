# Web Cat MCP

## Introduction

Web Cat is a collection of Python-based APIs designed to enhance AI models with web search and content extraction capabilities. The project includes:

1. A serverless Python-based API hosted on Azure Functions
2. A Model Context Protocol (MCP) server that provides web search capabilities for AI models

Both implementations are designed to responsibly scrape and process website content, making it easy to integrate web content into AI applications like ChatGPT through Custom GPTs.

## Components

### Azure Functions API

The Azure Functions API leverages the readability library and BeautifulSoup to extract the main body of text and related images from web pages.

### MCP Server

The Model Context Protocol (MCP) server is a FastAPI-based implementation that provides web search capabilities with enhanced content extraction. It follows the MCP specification for standardized AI model interactions and uses SSE transport for compatibility with LiteLLM and other MCP clients.

## Features
 - **Content Extraction**: Utilizes the readability library for clean text extraction
 - **Text Processing**: Further processes extracted content for improved usability
 - **Search Functionality**: Integrates with Serper.dev to provide web search capabilities
 - **Free Fallback**: Automatically falls back to DuckDuckGo search when no API key is configured
 - **MCP Compliance**: Follows standardized Model Context Protocol specifications
 - **Multiple API Styles**: Supports both Server-Sent Events (SSE) streaming and RESTful endpoints
 - **Rate Limiting**: Protects the API from abuse with configurable rate limits
 - **API Versioning**: Ensures backward compatibility as the API evolves
 - **Docker Support**: Easy deployment with Docker containers
 - **Parallel Processing**: Faster response times with parallel search result processing
 - **Comprehensive Testing**: Includes unit tests for core functionality

## Getting Started

### Azure Functions API
- See the `customgpt` directory for specific documentation

### MCP Server (Docker)
- Current version: 2.2.0 (simplified - no authentication required)
- Docker image: `tmfrisinger/webcat:2.2.0` or `tmfrisinger/webcat:latest`

#### Running with Docker
```bash
# Run with Serper API (recommended for best results)
docker run -p 8000:8000 -e SERPER_API_KEY=your_key tmfrisinger/webcat:2.2.0

# Run with free DuckDuckGo fallback (no API key required)
docker run -p 8000:8000 tmfrisinger/webcat:2.2.0

# Run on a custom port
docker run -p 9000:9000 -e PORT=9000 -e SERPER_API_KEY=your_key tmfrisinger/webcat:2.2.0

# With custom rate limiting
docker run -p 8000:8000 -e SERPER_API_KEY=your_key -e RATE_LIMIT_WINDOW=60 -e RATE_LIMIT_MAX_REQUESTS=10 tmfrisinger/webcat:2.2.0
```

#### Building the Docker Image
```bash
# Navigate to the docker directory
cd docker

# Run the build script
./build.sh
```

For more detailed Docker information, see the `docker/README.md` file.

## Configuration

### Environment Variables
- `SERPER_API_KEY`: Your Serper API key (optional, enables premium search results)
- `PORT`: The port to run the server on (default: 8000)
- `RATE_LIMIT_WINDOW`: Time window in seconds for rate limiting (default: 60)
- `RATE_LIMIT_MAX_REQUESTS`: Max requests per window (default: 10)

## Testing

The project includes comprehensive test suites for both the Azure Functions API and the MCP Server:

### MCP Server Tests
```bash
# Navigate to the tests directory
cd docker/tests

# Run the tests
python -m unittest test_mcp_server.py
```

## Limitations and Considerations
- **Text-Based Content**: The APIs are optimized for text and image content and may not accurately represent other multimedia or dynamic web content.
- **Search Quality**: While DuckDuckGo fallback provides free search functionality, Serper API typically delivers higher quality and more comprehensive results

## Search Sources
- **Serper API**: Premium search results with high accuracy and comprehensive coverage (requires API key)
- **DuckDuckGo Fallback**: Free search functionality with good quality results (no API key required)

## LiteLLM Compatibility
WebCat's MCP server now uses SSE (Server-Sent Events) transport instead of streamable-http, making it fully compatible with LiteLLM and other MCP clients that expect SSE protocol. No authentication is required, making it simple to integrate.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the terms of the license included in the repository.

## Azure Functions Usage

Here's a quick example of how to test the Azure Functions API locally:

```bash
cd customgpt
func start
curl -X POST http://localhost:7071/api/scrape -H "Content-Type: application/json" -d "{\"url\":\"https://example.com\"}" # text only
curl -X POST http://localhost:7071/api/scrape_with_images -H "Content-Type: application/json" -d "{\"url\":\"https://bigmedium.com/speaking/sentient-design-josh-clark-talk.html\"}" #text and images
curl -X POST http://localhost:7071/api/search -H "Content-Type: application/json" -d "{\"query\":\"your search query\"}" # search and get content
```

## Gates

What blocks a change, and where. Nothing here waits on a person's click: a pull request
merges when its required checks are green.

- **Locally**, the hooks `make hooks` installs from `.githooks/` (refused in a worktree,
  whose hooks are its clone's). `pre-commit` refuses a file staged in part, then runs
  `make check`. `commit-msg` refuses a subject that is not a sentence starting with a
  capital letter. `pre-push` refuses a push straight to `staging` or `main`, then runs
  `make check`. Each fails closed. Never bypass them.
- **In CI**, `.github/workflows/ci.yml` runs the lanes on every pull request into
  `staging` and `main`, on every push to them and nightly. Every job has a timeout, every
  action is pinned by its commit, and every gate after `make deps` runs offline.
- **On the forge**, `rulesets.json` protects `staging` and `main`: a pull request is
  required with no approval, the `check` and `witnesses` jobs are required checks, and
  the branch can be neither deleted nor force-pushed, with no bypass actor.
