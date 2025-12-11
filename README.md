# Scrape-any-web-page-into-structured-JSON-data-with-ScrapeNinja-and-AI
 Workflow Overview
Trigger: Starts the workflow (Manual or via Webhook).
ScrapeNinja (HTTP Request): Fetches the raw HTML, handling JavaScript rendering and proxy rotation.
HTML Cleaning (Code Node): Reduces token usage by stripping unnecessary tags (scripts, styles).
AI Extraction (LLM Chain): Analyzes the HTML and extracts specific data points into a JSON format.
📋 Prerequisites
n8n Instance: Self-hosted or Cloud.
ScrapeNinja API Key: You can get this from RapidAPI or APIRoad.
OpenAI API Key (or Anthropic/Google Gemini).
Step-by-Step Implementation
Step 1: The Trigger
Add a Manual Trigger node for testing. Later, you can replace this with a Webhook node if you want to trigger the scraper from an external app or a Schedule node for periodic scraping.
Step 2: Fetch HTML with ScrapeNinja
Instead of using the basic n8n HTTP node to hit the website directly (which often gets blocked), we use the HTTP node to call ScrapeNinja.
Add an HTTP Request node.
Method: POST
URL: https://scrapeninja.p.rapidapi.com/scrape
Authentication: Generic Credential Type -> Header Auth.
Name: x-rapidapi-key
Value: YOUR_SCRAPENINJA_API_KEY
Headers:
Content-Type: application/json
Body Parameters (JSON):
{
  "url": "[https://example.com/product-page](https://example.com/product-page)",
  "headers": [
    "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36"
  ],
  "retryNum": 1,
  "geo": "us"
}


Tip: Use expressions in the "url" field to make it dynamic based on your trigger input.
