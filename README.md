# AI-Powered Lead Processing Workflow for n8n

This repository contains an optimized n8n workflow for AI-powered lead processing, sentiment analysis, and engagement prediction.

## 📋 Overview

This workflow consists of four main components:

1. **Lead Scoring** - Scores incoming leads based on industry and job title
2. **Call Analysis** - Transcribes and analyzes call recordings for sentiment and action items
3. **Email Analysis** - Analyzes email content for sentiment and key points
4. **Data Enrichment** - Fetches additional data from external sources and predicts engagement

## 🔧 Setup Instructions

### Prerequisites

1. n8n installed and running
2. The following API credentials:
   - OpenAI API key
   - GoHighLevel (GHL) API key
   - LinkedIn API key (if using LinkedIn enrichment)
   - CoStar API key (if using property data enrichment)

### Import Steps

1. Download the `n8n-lead-workflow.json` file from this repository
2. In your n8n interface, go to **Workflows**
3. Click on **Import from File**
4. Select the downloaded JSON file
5. Configure your credentials:
   - Go to **Settings** > **Credentials**
   - Add the required API credentials (OpenAI, GHL, etc.)

## 📝 Workflow Components

### 1. Lead Scoring

- **Webhook Endpoint**: `/lead-scoring`
- **Expected Payload**:
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "industry": "Technology",
    "title": "CTO"
  }
  ```
- **Process**: 
  1. Extract lead data
  2. Score lead using GPT-4
  3. Store lead info in GoHighLevel

### 2. Call Analysis

- **Webhook Endpoint**: `/call-logging`
- **Expected Payload**:
  ```json
  {
    "contact_id": "12345",
    "call_id": "67890",
    "call_audio_url": "https://example.com/recording.mp3"
  }
  ```
- **Process**:
  1. Transcribe call audio
  2. Analyze sentiment and extract action items
  3. Store analysis in GoHighLevel

### 3. Email Analysis

- **Webhook Endpoint**: `/email-analysis`
- **Expected Payload**:
  ```json
  {
    "contact_id": "12345",
    "email_id": "67890",
    "email_content": "Hello, I'm interested in your services..."
  }
  ```
- **Process**:
  1. Analyze email sentiment
  2. Extract key points and suggest responses
  3. Store analysis in GoHighLevel

### 4. Data Enrichment

- **Webhook Endpoint**: `/data-enrichment`
- **Expected Payload**:
  ```json
  {
    "contact_id": "12345",
    "linkedin_id": "john-doe",
    "property_id": "67890"
  }
  ```
- **Process**:
  1. Fetch data from LinkedIn and CoStar
  2. Run predictive engagement model
  3. Update lead profile and create follow-up task

## 🚀 Optimizations

The optimized workflow includes:

- **Security**: API keys stored in credentials rather than hardcoded
- **Error Handling**: Robust parsing of AI responses with fallbacks
- **Modularity**: Separate workflows for different functions
- **Integration**: Complete integration with GoHighLevel CRM

## 🔗 Webhook Endpoints

All webhook endpoints are relative to your n8n instance URL:

- `https://your-n8n-instance.com/webhook/lead-scoring`
- `https://your-n8n-instance.com/webhook/call-logging`
- `https://your-n8n-instance.com/webhook/email-analysis`
- `https://your-n8n-instance.com/webhook/data-enrichment`

## 🔐 API Security

For production use, consider adding authentication to your webhooks using one of the following methods:

1. n8n built-in webhook authentication options
2. API key in headers
3. Basic authentication
4. JWT token-based authentication