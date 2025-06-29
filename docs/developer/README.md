# Developer Guide

This guide provides technical documentation for developers working with or integrating Retenify.

## Architecture Overview

Retenify follows a microservices architecture built on Google Cloud Platform:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   React.js      │    │   Node.js API   │    │   Python ML     │
│   Frontend      │◄──►│   Gateway       │◄──►│   Services      │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │              ┌─────────────────┐              │
         │              │   PostgreSQL    │              │
         └──────────────►│   Database      │◄─────────────┘
                        └─────────────────┘
```

## Development Environment Setup

### Prerequisites

- Node.js (v18+)
- Python (v3.9+)
- PostgreSQL (v13+)
- Redis (v6+)
- Docker & Docker Compose

### Local Development

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-org/retenify.git
   cd retenify
   ```

2. **Environment Configuration**
   ```bash
   cp .env.example .env
   # Edit .env with your local configuration
   ```

3. **Database Setup**
   ```bash
   # Start PostgreSQL and Redis
   docker-compose up -d postgres redis
   
   # Run migrations
   npm run db:migrate
   
   # Seed test data
   npm run db:seed
   ```

4. **Start Services**
   ```bash
   # Start all services
   npm run dev
   
   # Or start individually
   npm run dev:frontend    # React app on :3000
   npm run dev:api        # API server on :3001
   npm run dev:ml         # ML services on :3002
   ```

## API Development

### Project Structure

```
src/
├── api/
│   ├── controllers/     # Request handlers
│   ├── middleware/      # Express middleware
│   ├── models/         # Database models
│   ├── routes/         # API routes
│   ├── services/       # Business logic
│   └── utils/          # Helper functions
├── ml/
│   ├── models/         # ML model definitions
│   ├── training/       # Model training scripts
│   ├── prediction/     # Prediction services
│   └── data/           # Data processing
└── frontend/
    ├── src/
    │   ├── components/ # React components
    │   ├── pages/      # Page components
    │   ├── hooks/      # Custom hooks
    │   ├── services/   # API clients
    │   └── utils/      # Utilities
    └── public/         # Static assets
```

### Adding New API Endpoints

1. **Create Model** (if needed)
   ```javascript
   // src/api/models/campaign.js
   const { DataTypes } = require('sequelize');
   
   module.exports = (sequelize) => {
     return sequelize.define('Campaign', {
       name: DataTypes.STRING,
       type: DataTypes.ENUM('email', 'push', 'sms'),
       status: DataTypes.ENUM('draft', 'active', 'paused'),
       // ... other fields
     });
   };
   ```

2. **Create Controller**
   ```javascript
   // src/api/controllers/campaignController.js
   const campaignService = require('../services/campaignService');
   
   exports.createCampaign = async (req, res) => {
     try {
       const campaign = await campaignService.create(req.body);
       res.status(201).json(campaign);
     } catch (error) {
       res.status(400).json({ error: error.message });
     }
   };
   ```

3. **Define Routes**
   ```javascript
   // src/api/routes/campaigns.js
   const express = require('express');
   const campaignController = require('../controllers/campaignController');
   const auth = require('../middleware/auth');
   
   const router = express.Router();
   
   router.post('/', auth, campaignController.createCampaign);
   router.get('/', auth, campaignController.getCampaigns);
   
   module.exports = router;
   ```

## Machine Learning Development

### Model Architecture

Our churn prediction uses ensemble methods:

- **Gradient Boosting** (XGBoost) - Primary model
- **Random Forest** - Secondary model for comparison
- **Logistic Regression** - Baseline model

### Adding New ML Models

1. **Create Model Class**
   ```python
   # src/ml/models/health_score_model.py
   import pandas as pd
   from sklearn.ensemble import RandomForestRegressor
   from .base_model import BaseModel
   
   class HealthScoreModel(BaseModel):
       def __init__(self):
           self.model = RandomForestRegressor(n_estimators=100)
           
       def prepare_features(self, data):
           # Feature engineering logic
           return processed_features
           
       def train(self, training_data):
           features = self.prepare_features(training_data)
           self.model.fit(features, training_data['health_score'])
           
       def predict(self, customer_data):
           features = self.prepare_features(customer_data)
           return self.model.predict(features)
   ```

2. **Create Training Pipeline**
   ```python
   # src/ml/training/train_health_score.py
   from ..models.health_score_model import HealthScoreModel
   from ..data.data_loader import load_training_data
   
   def train_health_score_model():
       model = HealthScoreModel()
       data = load_training_data('health_scores')
       
       model.train(data)
       model.save('health_score_v1.pkl')
       
       return model.evaluate(data)
   ```

### Feature Engineering

Key features for churn prediction:

- **Usage Metrics**: Login frequency, feature adoption, session duration
- **Engagement Metrics**: Email opens, in-app actions, support interactions
- **Business Metrics**: Plan type, MRR, account age, payment history
- **Behavioral Patterns**: Usage trends, feature exploration, collaboration

## Frontend Development

### Component Structure

```
src/components/
├── common/          # Reusable components
│   ├── Button/
│   ├── Modal/
│   └── DataTable/
├── dashboard/       # Dashboard-specific components
├── campaigns/       # Campaign management
├── customers/       # Customer views
└── analytics/       # Analytics components
```

### State Management

Using React Context + useReducer for global state:

```javascript
// src/context/AppContext.js
import React, { createContext, useReducer } from 'react';

const AppContext = createContext();

const initialState = {
  user: null,
  customers: [],
  campaigns: [],
  loading: false
};

function appReducer(state, action) {
  switch (action.type) {
    case 'SET_USER':
      return { ...state, user: action.payload };
    // ... other actions
    default:
      return state;
  }
}

export const AppProvider = ({ children }) => {
  const [state, dispatch] = useReducer(appReducer, initialState);
  
  return (
    <AppContext.Provider value={{ state, dispatch }}>
      {children}
    </AppContext.Provider>
  );
};
```

### API Integration

```javascript
// src/services/api.js
class ApiClient {
  constructor(baseURL = '/api/v1') {
    this.baseURL = baseURL;
    this.token = localStorage.getItem('authToken');
  }
  
  async request(endpoint, options = {}) {
    const response = await fetch(`${this.baseURL}${endpoint}`, {
      headers: {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${this.token}`,
        ...options.headers,
      },
      ...options,
    });
    
    if (!response.ok) {
      throw new Error(`API Error: ${response.statusText}`);
    }
    
    return response.json();
  }
  
  // Specific methods
  async getCustomers() {
    return this.request('/customers');
  }
  
  async createCampaign(campaignData) {
    return this.request('/campaigns', {
      method: 'POST',
      body: JSON.stringify(campaignData),
    });
  }
}

export default new ApiClient();
```

## Testing

### Backend Testing

```javascript
// tests/api/campaigns.test.js
const request = require('supertest');
const app = require('../../src/app');
const { Campaign } = require('../../src/models');

describe('Campaign API', () => {
  beforeEach(async () => {
    await Campaign.destroy({ where: {} });
  });
  
  test('POST /campaigns should create campaign', async () => {
    const campaignData = {
      name: 'Welcome Series',
      type: 'email',
      triggers: [{ event: 'user_signup' }]
    };
    
    const response = await request(app)
      .post('/api/v1/campaigns')
      .send(campaignData)
      .expect(201);
      
    expect(response.body.name).toBe('Welcome Series');
  });
});
```

### Frontend Testing

```javascript
// src/components/Dashboard/__tests__/Dashboard.test.js
import { render, screen } from '@testing-library/react';
import { AppProvider } from '../../../context/AppContext';
import Dashboard from '../Dashboard';

test('renders dashboard with metrics', () => {
  render(
    <AppProvider>
      <Dashboard />
    </AppProvider>
  );
  
  expect(screen.getByText('Churn Risk')).toBeInTheDocument();
  expect(screen.getByText('Health Score')).toBeInTheDocument();
});
```

### ML Model Testing

```python
# tests/ml/test_churn_model.py
import pytest
import pandas as pd
from src.ml.models.churn_model import ChurnModel

class TestChurnModel:
    def setup_method(self):
        self.model = ChurnModel()
        self.sample_data = pd.DataFrame({
            'customer_id': [1, 2, 3],
            'usage_score': [0.8, 0.3, 0.9],
            'engagement_score': [0.7, 0.2, 0.8],
            'churned': [0, 1, 0]
        })
    
    def test_prediction_format(self):
        predictions = self.model.predict(self.sample_data)
        assert len(predictions) == 3
        assert all(0 <= p <= 1 for p in predictions)
```

## Deployment

### CI/CD Pipeline

```yaml
# .github/workflows/deploy.yml
name: Deploy to Production

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: |
          npm test
          python -m pytest
  
  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GCP
        run: |
          gcloud app deploy app.yaml
```

### Environment Configuration

Production environments use:
- Google Cloud Run for containerized services
- Cloud SQL for PostgreSQL
- Cloud Storage for file uploads
- Cloud Functions for ML inference

## Performance Monitoring

### Key Metrics

- API response times
- Database query performance
- ML model inference latency
- Frontend bundle size and load times

### Monitoring Tools

- **Application Performance**: Google Cloud Monitoring
- **Error Tracking**: Sentry
- **User Analytics**: Google Analytics 4
- **API Monitoring**: Custom dashboards

## Security Guidelines

### Authentication

- JWT tokens for API access
- OAuth 2.0 for third-party integrations
- Multi-factor authentication for admin accounts

### Data Protection

- Encryption at rest and in transit
- PII data anonymization
- GDPR compliance measures
- Regular security audits

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make changes with tests
4. Submit pull request
5. Code review and merge

See [CONTRIBUTING.md](../../CONTRIBUTING.md) for detailed guidelines.
