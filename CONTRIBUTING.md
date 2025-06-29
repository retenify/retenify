# Contributing to Retenify

Thank you for your interest in contributing to Retenify! This document provides guidelines and information for contributors.

## 🤝 How to Contribute

### Ways to Contribute

- **🐛 Bug Reports**: Help us identify and fix issues
- **💡 Feature Requests**: Suggest new features and improvements
- **📝 Documentation**: Improve our documentation and guides
- **🔧 Code Contributions**: Submit bug fixes and new features
- **🧪 Testing**: Help test new features and report issues
- **💬 Community Support**: Help other users in discussions

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have:
- **Node.js** (v18 or higher)
- **Python** (v3.9 or higher)
- **PostgreSQL** (v13 or higher)
- **Git** for version control
- **Docker** and **Docker Compose** (optional, for easier setup)

### Development Setup

1. **Fork the Repository**
   ```bash
   # Fork the repository on GitHub, then clone your fork
   git clone https://github.com/YOUR-USERNAME/retenify.git
   cd retenify
   ```

2. **Set Up Development Environment**
   ```bash
   # Copy environment configuration
   cp .env.example .env
   
   # Install dependencies
   npm install
   pip install -r requirements.txt
   
   # Set up database
   npm run db:setup
   
   # Start development servers
   npm run dev
   ```

3. **Verify Setup**
   - Frontend: http://localhost:3000
   - API: http://localhost:3001
   - ML Services: http://localhost:3002

## 📋 Development Guidelines

### Code Style

#### JavaScript/TypeScript
```javascript
// Use ES6+ features
const processCustomer = async (customer) => {
  try {
    const result = await churnPredictor.predict(customer);
    return { success: true, prediction: result };
  } catch (error) {
    logger.error('Prediction failed:', error);
    throw new Error('Prediction processing failed');
  }
};
```

#### Python
```python
# Follow PEP 8 guidelines
def calculate_health_score(customer_data: Dict[str, Any]) -> float:
    """Calculate customer health score based on multiple factors.
    
    Args:
        customer_data: Dictionary containing customer metrics
        
    Returns:
        Health score between 0 and 100
    """
    usage_score = customer_data.get('usage_score', 0)
    engagement_score = customer_data.get('engagement_score', 0)
    
    return (usage_score * 0.6) + (engagement_score * 0.4)
```

### Commit Messages

Follow the [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (no logic changes)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

**Examples:**
```
feat(api): add customer health score endpoint

fix(dashboard): resolve timezone display issues

docs(readme): update installation instructions

test(churn): add unit tests for prediction model
```

### Branch Naming

Use descriptive branch names:
```
feature/customer-health-scoring
bugfix/campaign-scheduling-timezone
hotfix/security-vulnerability-fix
docs/api-documentation-update
```

## 🧪 Testing

### Running Tests

```bash
# Run all tests
npm test

# Run frontend tests
npm run test:frontend

# Run backend tests
npm run test:backend

# Run ML tests
python -m pytest tests/ml/

# Run with coverage
npm run test:coverage
```

### Writing Tests

#### Frontend Tests (Jest + React Testing Library)
```javascript
import { render, screen, fireEvent } from '@testing-library/react';
import CustomerHealthCard from '../CustomerHealthCard';

describe('CustomerHealthCard', () => {
  test('displays health score correctly', () => {
    const customer = { id: '123', health_score: 85 };
    
    render(<CustomerHealthCard customer={customer} />);
    
    expect(screen.getByText('85')).toBeInTheDocument();
    expect(screen.getByText('Healthy')).toBeInTheDocument();
  });
});
```

#### Backend Tests (Jest + Supertest)
```javascript
const request = require('supertest');
const app = require('../app');

describe('Customer API', () => {
  test('GET /api/customers returns customer list', async () => {
    const response = await request(app)
      .get('/api/customers')
      .set('Authorization', 'Bearer ' + validToken)
      .expect(200);
      
    expect(response.body).toHaveProperty('customers');
    expect(Array.isArray(response.body.customers)).toBe(true);
  });
});
```

#### ML Tests (pytest)
```python
import pytest
from src.ml.models.churn_model import ChurnModel

class TestChurnModel:
    def setup_method(self):
        self.model = ChurnModel()
    
    def test_prediction_range(self):
        sample_data = {
            'usage_score': 0.8,
            'engagement_score': 0.6,
            'support_tickets': 2
        }
        
        prediction = self.model.predict(sample_data)
        assert 0 <= prediction <= 1
```

## 📝 Pull Request Process

### Before Submitting

1. **Create an Issue**: Discuss your changes before implementing
2. **Update Documentation**: Ensure docs reflect your changes
3. **Add Tests**: Include tests for new functionality
4. **Run Tests**: Ensure all tests pass
5. **Check Style**: Follow code style guidelines

### Pull Request Template

```markdown
## Description
Brief description of changes made.

## Type of Change
- [ ] Bug fix
- [ ] New feature  
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] Manual testing completed

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] Tests added and passing
```

### Review Process

1. **Automated Checks**: CI/CD pipeline runs automatically
2. **Code Review**: At least 2 team members review
3. **Testing**: QA team validates changes
4. **Approval**: Maintainer approves and merges

## 🐛 Bug Reports

### Before Reporting

1. **Search Existing Issues**: Check if already reported
2. **Reproduce**: Ensure the bug is reproducible
3. **Collect Information**: Gather relevant details

### Bug Report Template

```markdown
**Bug Description**
Clear description of the bug.

**Steps to Reproduce**
1. Go to '...'
2. Click on '...'
3. See error

**Expected Behavior**
What should happen.

**Actual Behavior**
What actually happens.

**Environment**
- OS: [e.g., macOS 12.0]
- Browser: [e.g., Chrome 96]
- Version: [e.g., 2.4.0]

**Additional Context**
Screenshots, logs, or other relevant information.
```

## 💡 Feature Requests

### Feature Request Template

```markdown
**Problem Statement**
What problem does this feature solve?

**Proposed Solution**
Describe your proposed solution.

**Alternatives Considered**
Other solutions you've considered.

**Use Cases**
How would this feature be used?

**Additional Context**
Any other relevant information.
```

## 📚 Documentation

### Documentation Standards

- **Clear and Concise**: Write for your audience
- **Examples**: Include code examples and use cases
- **Up-to-Date**: Keep documentation current with code
- **Accessible**: Use clear language and structure

### Documentation Types

- **API Documentation**: OpenAPI/Swagger specifications
- **User Guides**: Step-by-step instructions
- **Developer Docs**: Technical implementation details
- **Tutorials**: Learning-focused content

## 🏆 Recognition

### Contributor Levels

**🌱 New Contributor**
- First-time contributors
- Small bug fixes or documentation updates
- Learning the codebase

**🚀 Regular Contributor**
- Multiple merged contributions
- Feature implementations
- Code reviews and mentoring

**⭐ Core Contributor**
- Significant feature contributions
- Architectural decisions
- Community leadership

### Hall of Fame

We recognize outstanding contributors in our:
- **README**: Top contributors list
- **Website**: Contributor showcase
- **Community**: Special recognition badges
- **Events**: Conference speaking opportunities

## 🎯 Focus Areas

### Current Priorities

1. **Performance Optimization**
   - Database query optimization
   - Frontend bundle size reduction
   - API response time improvements

2. **User Experience**
   - Mobile responsiveness
   - Accessibility improvements
   - User interface enhancements

3. **Machine Learning**
   - Model accuracy improvements
   - New prediction algorithms
   - Real-time ML capabilities

4. **Integrations**
   - New third-party integrations
   - API improvements
   - Webhook enhancements

### Good First Issues

Look for issues labeled:
- `good first issue`: Perfect for new contributors
- `help wanted`: Community assistance needed
- `documentation`: Documentation improvements
- `beginner friendly`: Low complexity tasks

## 📞 Getting Help

### Community Support

- **GitHub Discussions**: [github.com/retenify/retenify/discussions](https://github.com/retenify/retenify/discussions)
- **Discord**: [discord.gg/retenify](https://discord.gg/retenify)
- **Stack Overflow**: Tag your questions with `retenify`

### Direct Contact

- **General Questions**: contribute@retenify.com
- **Security Issues**: security@retenify.com
- **Partnership Inquiries**: partners@retenify.com

## 📜 Code of Conduct

### Our Pledge

We pledge to make participation in our project a harassment-free experience for everyone, regardless of:
- Age, body size, disability, ethnicity
- Gender identity and expression
- Level of experience, nationality
- Personal appearance, race, religion
- Sexual identity and orientation

### Our Standards

**Positive Behavior Examples:**
- Using welcoming and inclusive language
- Respecting differing viewpoints and experiences
- Accepting constructive criticism gracefully
- Focusing on what's best for the community
- Showing empathy towards other community members

**Unacceptable Behavior Examples:**
- Trolling, insulting, or derogatory comments
- Public or private harassment
- Publishing others' private information
- Other conduct inappropriate for a professional setting

### Enforcement

Community leaders will:
- Clarify standards of acceptable behavior
- Take corrective action for inappropriate behavior
- Remove, edit, or reject contributions that violate standards
- Ban temporarily or permanently for serious violations

### Reporting

Report unacceptable behavior to conduct@retenify.com. All complaints will be reviewed and investigated promptly and fairly.

## 📄 License

By contributing to Retenify, you agree that your contributions will be licensed under the same license as the project (MIT License).

---

Thank you for contributing to Retenify! Together, we're building the future of customer retention and churn prevention. 🚀
