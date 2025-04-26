# MCP Demo Project

A demonstration project showcasing the integration of multiple service providers (Airbnb, MakeMyTrip, DuckDuckGo) using MCP (Model Control Protocol) architecture. This project demonstrates how to build a unified interface for travel and search services.

## Table of Contents
- [Features](#features)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Available Commands](#available-commands)
- [Usage Examples](#usage-examples)
- [Error Handling](#error-handling)
- [Security Considerations](#security-considerations)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Browser Automation**: 
  - Automated browser control using Playwright
  - Headless and headed mode support
  - Cross-browser compatibility (Chrome, Firefox, Safari)

- **Multi-Platform Integration**:
  - Airbnb search and listing details
  - MakeMyTrip hotel booking interface
  - DuckDuckGo web search capabilities

- **Cross-Platform Compatibility**: 
  - Works on Windows, macOS, and Linux
  - Docker support for containerized deployment

## Architecture

### Core Components

1. **MCP Servers**:
   - Playwright MCP Server: Handles browser automation
   - Airbnb MCP Server: Manages Airbnb API interactions
   - DuckDuckGo MCP Server: Provides web search functionality

2. **Configuration**:
   - Centralized configuration in `browser_mcp.json`
   - Modular server setup for easy extension
   - Environment-based configuration support

### Service Integration

```
┌─────────────────┐
│    Main App     │
└────────┬────────┘
         │
┌────────┴────────┐
│   MCP Servers   │
└────────┬────────┘
         │
    ┌────┴────┐
    │        │
┌───┴───┐  ┌─┴────┐  ┌──────┐
│Airbnb │  │Browser│  │Search│
└───────┘  └───────┘  └──────┘
```

## Prerequisites

- Node.js (v14 or higher)
- npm or yarn package manager
- Python 3.8+ (for certain features)
- Docker (optional, for containerized deployment)

## Setup

1. Clone the repository:
```bash
git clone https://github.com/ykbeladiya/MCP-Demo-Project.git
cd MCP-Demo-Project
```

2. Install dependencies:
```bash
npm install @playwright/mcp @openbnb/mcp-server-airbnb duckduckgo-mcp-server
```

3. Configure MCP servers in `browser_mcp.json`:
```json
{
    "mcpServers": {
      "playwright": {
        "command": "npx",
        "args": ["@playwright/mcp@latest"]
      },
      "airbnb": {
        "command": "npx",
        "args": ["-y", "@openbnb/mcp-server-airbnb"]
      },
      "duckduckgo-search": {
        "command": "npx",
        "args": ["-y", "duckduckgo-mcp-server"]
      }
    }
}
```

4. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your configuration
```

## Available Commands

### Browser Control
- Navigate to URLs
- Take screenshots and PDF exports
- Handle file uploads
- Manage multiple tabs
- Perform clicks and form inputs
- Execute JavaScript in the page context

### Airbnb Integration
- Search for listings with filters
- Get detailed property information
- Filter by dates, guests, and location
- Access pricing and availability data
- Handle user authentication

### Search Capabilities
- Web search via DuckDuckGo
- Configurable search parameters
- Safe search options
- Region-specific search results
- Rich search result metadata

## Usage Examples

1. **Browser Navigation and Interaction**:
```javascript
// Navigate and interact with a page
await page.goto('https://www.example.com');
await page.click('#search-button');
await page.screenshot({ path: 'screenshot.png' });
```

2. **Airbnb Search with Filters**:
```javascript
const results = await airbnb.search({
  location: "New York",
  checkin: "2024-04-25",
  checkout: "2024-04-26",
  adults: 2,
  children: 0,
  maxPrice: 300
});
```

3. **Advanced Web Search**:
```javascript
const searchResults = await duckduckgo.search({
  query: "search term",
  safeSearch: "moderate",
  count: 20
});
```

## Error Handling

- Robust error handling for browser automation
- Automatic retries for failed requests
- Detailed error messages and logging
- Custom error types for different scenarios
- Graceful fallback mechanisms

## Security Considerations

- Safe handling of sensitive data
- No storage of API keys in code
- Respect for robots.txt and rate limiting
- Input sanitization and validation
- HTTPS enforcement for API calls

## Troubleshooting

Common issues and their solutions:

1. **Browser Automation Fails**
   - Ensure Playwright is properly installed
   - Check browser compatibility
   - Verify network connectivity

2. **API Rate Limiting**
   - Implement request throttling
   - Use caching where appropriate
   - Handle rate limit errors gracefully

3. **Configuration Issues**
   - Verify environment variables
   - Check JSON syntax in config files
   - Ensure proper file permissions

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request


## License

This project is licensed under the Apache License Version 2.0, January 2004 - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Playwright team for the browser automation framework
- Airbnb and MakeMyTrip for their service APIs
- DuckDuckGo for search capabilities
- All contributors who have helped shape this project
