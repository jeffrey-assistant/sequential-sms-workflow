# Sequential SMS Dispatch - Setup Guide

## Overview

This n8n workflow takes AI-generated text responses with intentional line breaks and sends each line as a separate SMS in sequence with a configurable delay.

## Prerequisites

- n8n instance (self-hosted or cloud)
- Twilio account with phone number
- Node.js 18+ (for local testing)

## Installation

### 1. Import the Workflow

1. Open n8n dashboard
2. Click "Settings" (gear icon) → "Import from file"
3. Select `sequential-sms-workflow.json`
4. Click "Import"

### 2. Configure Twilio Credentials

1. Go to **Settings** → **Credentials**
2. Click "Add credential"
3. Select **Twilio API**
4. Enter your Twilio credentials:
   - Account SID
   - Auth Token
5. Save the credential

### 3. Update Workflow Parameters

In the workflow:
1. Click on "Send SMS" node
2. Update the **From** field with your Twilio number (E.164 format: +1234567890)
3. The **To** field should be set dynamically via webhook parameters

### 4. Activate the Workflow

1. Click "Activate" toggle in the top-right
2. Copy the webhook URL for testing

## Usage

### Send SMS via cURL

```bash
curl -X POST https://your-n8n-instance.com/webhook/sequential-sms \
  -H "Content-Type: application/json" \
  -d '{
    "from": "+1234567890",
    "to": "+0987654321",
    "message": "Bonjour! 👋\nMerci pour votre message.\n\nNous allons traiter votre demande.\nUn conseiller vous contactera sous 24h.\n\nBonne journée! 😊"
  }'
```

### Configuration Options

| Parameter | Description | Default |
|-----------|-------------|---------|
| `from` | Twilio phone number (sender) | Required |
| `to` | Recipient phone number | Required |
| `message` | AI-generated text with line breaks | Required |
| `delay` | Delay between SMS (seconds) | 0.6 |

### Adjusting Delay

To change the delay between SMS:
1. Click on the "Delay" node
2. Update the **Amount** field (recommended: 0.5-0.8 seconds)
3. Save and reactivate

## Testing

### Local Test Script

```bash
# Run the test script
node test-script.js
```

This will:
1. Parse the test message
2. Show how many SMS will be sent
3. Display each SMS content

### Test with Webhook

```bash
# Test with sample data
node test-script.js --send
```

This sends a test request to your n8n webhook.

## Troubleshooting

### SMS not sending
- Check Twilio credentials are valid
- Verify phone numbers are in E.164 format
- Check n8n logs for errors

### Messages out of order
- Increase the delay between messages
- Check network latency

### Empty messages sent
- Ensure AI output has no consecutive empty lines
- The workflow filters empty lines automatically

## Architecture

```
AI Output → Webhook → Parse Lines → Loop (1 msg) → Delay → Twilio SMS
                                                    ↓
                                           Confirmation Response
```

## Files

| File | Description |
|------|-------------|
| `sequential-sms-workflow.json` | n8n workflow file |
| `test-example.json` | Test data example |
| `test-script.js` | Local test script |
| `SETUP.md` | This setup guide |

## License

MIT