# Retenify API Documentation

## Overview

The Retenify API provides programmatic access to all platform features, enabling developers to integrate churn prediction, customer health scoring, and automated engagement capabilities into their applications.

## Base URL

```
https://api.retenify.com/v1
```

## Authentication

All API requests require authentication using API keys:

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
     -H "Content-Type: application/json" \
     https://api.retenify.com/v1/customers
```

## Core Endpoints

### Customers

- `GET /customers` - List all customers
- `GET /customers/{id}` - Get customer details
- `POST /customers` - Create new customer
- `PUT /customers/{id}` - Update customer
- `DELETE /customers/{id}` - Delete customer

### Churn Prediction

- `GET /churn/predictions` - Get churn predictions
- `POST /churn/predict` - Generate churn prediction for customer
- `GET /churn/models` - List available ML models

### Health Scores

- `GET /health-scores` - Get customer health scores
- `POST /health-scores/calculate` - Calculate health score
- `GET /health-scores/history/{customer_id}` - Get score history

### Campaigns

- `GET /campaigns` - List campaigns
- `POST /campaigns` - Create campaign
- `PUT /campaigns/{id}` - Update campaign
- `POST /campaigns/{id}/trigger` - Trigger campaign

### Analytics

- `GET /analytics/retention` - Get retention metrics
- `GET /analytics/cohorts` - Get cohort analysis
- `GET /analytics/segments` - Get segmentation data

## SDKs

- [JavaScript/Node.js SDK](./sdks/javascript.md)
- [Python SDK](./sdks/python.md)
- [REST API Examples](./examples/README.md)

## Rate Limits

- 1000 requests per hour for standard plans
- 5000 requests per hour for enterprise plans

## Error Handling

All errors follow RFC 7807 problem details format:

```json
{
  "type": "https://api.retenify.com/errors/validation",
  "title": "Validation Error",
  "status": 400,
  "detail": "Missing required field: customer_id"
}
```

## Webhooks

Configure webhooks to receive real-time notifications:

- Customer churn risk alerts
- Campaign completion events
- Health score changes
- System events

For detailed API reference, see our [OpenAPI specification](./openapi.yaml).
