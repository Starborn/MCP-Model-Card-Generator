# Brave Search MCP Server - Model Card

**Version**: 2.0.72  
**Model Card Version**: 1.0.0  
**Last Updated**: 2026-02-13T18:48:24.944811Z

---

## Server Metadata

**Description**:  MCP server integrating Brave Search API with web search, local search, image search, video search, news search, and AI-powered summarization capabilities



Language: typescript
Transports: Select both "stdio" and "http+sse"
Tags: brave, search, web-search, local-search, image-search, api

**Protocol Version**: 2025-11-25

**Author**: Brave sotware   Model card geneated by PDM

**License**: MIT

**Implementation Language**: typescript

**Supported Transports**: stdio, http+sse

---

## Tools (3 total)

### 1. brave_web_search
**Description**: Performs comprehensive web searches with rich result types and advanced filtering options

**Read-only**: Yes  
**Async**: Yes  
**Destructive**: No

---

### 2. brave_local_search
**Description**: Searches for local businesses and places with detailed information including ratings, hours, and AI-generated descriptions

**Read-only**: Yes  
**Async**: Yes  
**Destructive**: No

---

### 3.  brave_image_search
**Description**: 
Description: Searches for images with comprehensive metadata
Destructive: NO
Read-only: YES
Async: YES

**Read-only**: Yes  
**Async**: Yes  
**Destructive**: No

---

## Performance & Operations

### Performance Benchmarks
- Average response time: 250ms

### Rate Limits
- 60 requests per minute
- 1998 requests per hour

### Known Limitations

- Free tier limited to 2,000 queries/month
- Extra snippets require Pro plan
- Local search requires Pro plan
- Maximum 20 results per web search request
- Maximum 9 page offset for pagination

---

## Security Profile

### Authentication
**Methods**: oauth2

**Credential Storage**: environment_variables

### Data Handling
**Retention Policy**: No data retained; acts as stateless proxy

**Encryption in Transit**: Yes

**PII Handling**: 

### Security Considerations


### Security Best Practices


---

## Deployment

### Intended Use Cases


### Out of Scope


### Maintenance
**Status**: ✅ Actively maintained

---

## Evaluation Results

**Compliance Score**: 95/100

**Test Coverage**: Not specified

**Tests**: 0 passed, 0 failed

---

**Generated with**: MCP Model Card Generator v1.0  
**Specification**: MCP Model Card Specification v1.0  
**W3C AI-KR Community Group**
