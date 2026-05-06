# Standards & API Reference

> Project: Browser Automation Platform · Generated: 2026-05-03

## Industry Standards & Specifications

### W3C Standards

**WebDriver (W3C Recommendation)**
- URL: https://www.w3.org/TR/webdriver2/
- The foundational W3C standard defining a platform- and language-neutral wire protocol for remote control of web browsers. All major browser automation frameworks (Selenium 4+, WebdriverIO) implement this standard. Defines session management, element interaction, and navigation commands via HTTP REST.

**WebDriver BiDi (W3C Working Draft — March 2026)**
- URL: https://www.w3.org/TR/webdriver-bidi/ | Spec repo: https://github.com/w3c/webdriver-bidi
- The next-generation bidirectional browser automation protocol, extending WebDriver with two-way WebSocket communication. Allows the browser to push events (network requests, console logs, JS exceptions) back to the automation client in real time, replacing the one-shot request/response model of classical WebDriver. Playwright, Puppeteer, and Selenium 4+ are actively adopting this standard. As of 2026 it is a living working draft updated continuously.

**Content Security Policy Level 3 (W3C Candidate Recommendation)**
- URL: https://www.w3.org/TR/CSP3/
- Defines the `Content-Security-Policy` HTTP header, which affects what resources a browser is permitted to load and from where. Relevant to browser automation platforms when emulating realistic browser environments, injecting scripts, or intercepting page resources during testing.

**WebSocket Protocol — WHATWG Living Standard**
- URL: https://websockets.spec.whatwg.org/
- The browser-facing API spec for WebSocket connections; pairs with RFC 6455 below. WebDriver BiDi message transport is built on WebSockets, making this directly relevant to any BiDi implementation.

### IETF Standards

**RFC 6455 — The WebSocket Protocol**
- URL: https://www.rfc-editor.org/rfc/rfc6455
- The IETF Internet Standard (STD 34) that specifies the WebSocket framing protocol. Since WebDriver BiDi uses WebSockets as its transport layer, RFC 6455 is the foundational transport standard for modern bidirectional browser automation.

**RFC 9110 — HTTP Semantics**
- URL: https://www.rfc-editor.org/rfc/rfc9110
- Defines HTTP semantics underpinning the classical WebDriver REST protocol and REST APIs exposed by managed browser infrastructure providers (Browserbase, BrowserStack).

**RFC 6749 — The OAuth 2.0 Authorization Framework**
- URL: https://www.rfc-editor.org/rfc/rfc6749
- Governs API authentication for commercial browser automation SaaS platforms (Browserbase, BrowserStack, Firecrawl). Any platform exposing a REST API to external users must implement OAuth 2.0 or API-key authentication in line with this framework.

### Data Model & API Specifications

**OpenAPI Specification 3.1 / 3.2**
- URL: https://spec.openapis.org/oas/v3.2.0.html | GitHub: https://github.com/OAI/OpenAPI-Specification
- The industry standard for describing REST APIs in a machine-readable YAML/JSON document. Browser automation SaaS platforms (Firecrawl, Browserbase) publish OpenAPI specs to enable SDK auto-generation, interactive documentation, and contract testing. An AI-native browser automation platform should ship a versioned OpenAPI specification from day one.

**JSON Schema (Draft 2020-12)**
- URL: https://json-schema.org/
- Used within OpenAPI 3.1 documents to define request/response payload schemas. Browser automation configuration objects (browser launch options, network interception rules, extraction schemas) are commonly expressed as JSON Schema.

**Chrome DevTools Protocol (CDP)**
- URL: https://chromedevtools.github.io/devtools-protocol/
- The low-level, Chromium-team-maintained inspection and control protocol for Chrome/Chromium and Edge. Defined as Protocol Definition Language (PDL) files in the Chromium source tree, mirrored as JSON and TypeScript definitions on GitHub and NPM. Underlies Puppeteer and Playwright's Chromium backend. Also natively supported by Cloudflare Browser Rendering (2026).

### Security & Authentication Standards

**OWASP Web Security Testing Guide (WSTG)**
- URL: https://owasp.org/www-project-web-security-testing-guide/
- Provides guidance on testing for OAuth weaknesses and authentication flaws. Relevant for platforms that automate authenticated sessions and must handle credentials, cookies, and tokens securely.

**OWASP Content Security Policy Cheat Sheet**
- URL: https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html
- Practical guidance on CSP headers; relevant when designing an automation platform that injects instrumentation scripts into pages under automation.

**OAuth 2.0 with PKCE (RFC 7636)**
- URL: https://www.rfc-editor.org/rfc/rfc7636
- Best-practice flow for public clients. OWASP recommends Authorization Code + PKCE as the only safe OAuth flow for 2026. Browser automation APIs that issue access tokens to CI/CD pipelines or agent runtimes should follow this guidance.

### Observability Standards

**OpenTelemetry (CNCF Graduated Project)**
- URL: https://opentelemetry.io/ | JS SDK: https://github.com/open-telemetry/opentelemetry-js
- Vendor-neutral tracing, metrics, and logging specification increasingly adopted in production browser automation pipelines. The `@opentelemetry/sdk-trace-web` package enables distributed tracing of browser automation sessions. Relevant for correlating scraping pipeline latency, failure rates, and LLM inference calls in an AI-native platform.

### MCP Server Specifications

**Model Context Protocol (MCP) — Specification 2025-11-25**
- URL: https://modelcontextprotocol.io/specification/2025-11-25 | GitHub: https://github.com/modelcontextprotocol/modelcontextprotocol
- An open protocol (JSON-RPC 2.0 over stdio or HTTP+SSE) standardising how LLM agents connect to external tools and data sources. Multiple browser automation MCP servers already exist (chrome-devtools-mcp, Puppeteer-based servers). An AI-native browser automation platform should expose an MCP server interface so any MCP-compatible agent (Claude, Cursor, etc.) can drive the browser without bespoke integration code.

---

## Similar Products — Developer Documentation & APIs

### Playwright (Microsoft)
- **Description:** Cross-browser automation library for Node.js, Python, Java, and .NET, supporting Chromium, Firefox, and WebKit via a unified API. The current gold standard for code-first browser automation.
- **API Documentation:** https://playwright.dev/docs/api/class-playwright
- **SDKs/Libraries:** Node.js (`playwright`), Python (`playwright`), Java (`playwright`), .NET (`Microsoft.Playwright`)
- **Developer Guide:** https://playwright.dev/docs/intro
- **Standards:** WebDriver BiDi (in progress), CDP (Chromium)
- **Authentication:** N/A (local library; no hosted API)

### Puppeteer (Google)
- **Description:** Node.js and Python library providing a high-level API over CDP (and now WebDriver BiDi) for headless Chrome and Firefox control. Maintained by the Chrome DevTools team.
- **API Documentation:** https://pptr.dev/ | https://developer.chrome.com/docs/puppeteer
- **SDKs/Libraries:** Node.js (`puppeteer`), Python (`pyppeteer` community fork)
- **Developer Guide:** https://pptr.dev/guides/getting-started
- **Standards:** CDP, WebDriver BiDi (experimental)
- **Authentication:** N/A (local library; no hosted API)

### Selenium / WebDriver
- **Description:** The original browser automation standard with bindings across Java, Python, C#, Ruby, JavaScript, and Kotlin. Backed by the Selenium Foundation and aligned with W3C WebDriver.
- **API Documentation:** https://www.selenium.dev/documentation/webdriver/ | Python: https://selenium-python.readthedocs.io/api.html | Java: https://www.selenium.dev/selenium/docs/api/java/
- **SDKs/Libraries:** Java (`selenium-java`), Python (`selenium`), C# (`Selenium.WebDriver`), Ruby (`selenium-webdriver`), JavaScript (`selenium-webdriver`)
- **Developer Guide:** https://www.selenium.dev/documentation/
- **Standards:** W3C WebDriver, WebDriver BiDi (Selenium 4+)
- **Authentication:** N/A (local library; Grid uses basic auth)

### WebdriverIO
- **Description:** Node.js test automation framework built on top of WebDriver and WebDriver BiDi, with first-class support for Appium (mobile), visual testing, and component testing.
- **API Documentation:** https://webdriver.io/docs/api/
- **SDKs/Libraries:** Node.js (`webdriverio`)
- **Developer Guide:** https://webdriver.io/docs/gettingstarted/
- **Standards:** W3C WebDriver, WebDriver BiDi
- **Authentication:** N/A (local); optional Sauce Labs / BrowserStack cloud authentication via service plugins

### Stagehand (Browserbase)
- **Description:** Open-source AI-native Playwright wrapper exposing four natural-language primitives — `act`, `extract`, `observe`, and `agent` — that resolve instructions using LLM inference at runtime, making scripts resilient to UI changes.
- **API Documentation:** https://docs.stagehand.dev/ | https://docs.browserbase.com/introduction/stagehand
- **SDKs/Libraries:** TypeScript (`@browserbasehq/stagehand`), Python (`stagehand-py`), Java (alpha), PHP (alpha), C#/.NET (alpha)
- **Developer Guide:** https://www.stagehand.dev/
- **Standards:** Playwright API; supports OpenAI, Anthropic, and Google Gemini via the Vercel AI SDK
- **Authentication:** LLM API key (OpenAI/Anthropic/Gemini); optional Browserbase session API key

### Browserbase
- **Description:** Managed cloud browser infrastructure offering isolated session environments, persistent browser profiles, CAPTCHA solving, and a Functions runtime for co-located agent logic. REST API exposes Sessions, Projects, Contexts, and Extensions resources.
- **API Documentation:** https://docs.browserbase.com/reference/introduction
- **SDKs/Libraries:** Node.js (`@browserbasehq/sdk`), Python (`browserbase`)
- **Developer Guide:** https://docs.browserbase.com/
- **Standards:** REST/JSON; OpenAPI-described; Playwright and Puppeteer compatible
- **Authentication:** API Key (Bearer token in Authorization header)

### Firecrawl
- **Description:** Web search, scraping, and interaction API with an integrated Browser Sandbox. Exposes `/interact` for natural-language page interaction and `/extract` for structured data extraction. Primary target is AI agent pipelines.
- **API Documentation:** https://docs.firecrawl.dev/api-reference/introduction
- **SDKs/Libraries:** Node.js (`@mendable/firecrawl-js`), Python (`firecrawl-py`), Go, Ruby, C# (.NET)
- **Developer Guide:** https://docs.firecrawl.dev/
- **Standards:** REST/JSON; OpenAPI-described
- **Authentication:** API Key (`Authorization: Bearer fc-<key>`)

### BrowserStack Automate
- **Description:** Cloud cross-browser testing grid supporting Playwright, Selenium, and Cypress across thousands of real browser/OS/device combinations. REST API provides build, session, and project management.
- **API Documentation:** https://www.browserstack.com/docs/automate/api-reference/selenium/introduction
- **SDKs/Libraries:** BrowserStack SDK (Node.js, Java, Python, Ruby, C#)
- **Developer Guide:** https://www.browserstack.com/docs/
- **Standards:** W3C WebDriver, REST/JSON
- **Authentication:** HTTP Basic Auth (username:access-key) or API key

---

## Notes

- **WebDriver BiDi convergence**: As of mid-2026, WebDriver BiDi is the clear direction for all major browsers and automation tools. A new platform should implement BiDi as its primary protocol from inception rather than building on legacy WebDriver or CDP alone.
- **MCP as the agent integration layer**: MCP is rapidly becoming the standard integration surface for AI agents. Exposing browser automation primitives as MCP tools (rather than bespoke SDK calls) dramatically lowers the integration burden for agent builders.
- **No universal scraping ethics standard**: There is no ISO or W3C standard governing web scraping ethics or robots.txt compliance. The de facto norm is `robots.txt` (informally standardised) and the Robots Exclusion Protocol; any production platform should surface robots.txt compliance checks prominently.
- **Observability gap**: OpenTelemetry browser instrumentation remains experimental (Client Instrumentation SIG). A platform that provides first-class OTel export of automation session traces would occupy an underserved niche.
