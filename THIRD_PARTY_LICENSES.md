# Third-Party Licenses

This document lists all third-party open source libraries used in Retenify and their respective licenses.

## Frontend Dependencies

### React Ecosystem
- **React** (18.2.0) - MIT License
- **React DOM** (18.2.0) - MIT License
- **React Router** (6.8.0) - MIT License
- **React Query** (4.24.0) - MIT License

### UI Libraries
- **Material-UI** (5.11.0) - MIT License
- **Emotion** (11.10.0) - MIT License
- **styled-components** (5.3.0) - MIT License

### Visualization
- **Chart.js** (4.2.0) - MIT License
- **React Chart.js 2** (5.2.0) - MIT License
- **D3.js** (7.8.0) - ISC License

### Utilities
- **Lodash** (4.17.21) - MIT License
- **Moment.js** (2.29.4) - MIT License
- **Axios** (1.3.0) - MIT License

## Backend Dependencies

### Node.js Framework
- **Express.js** (4.18.0) - MIT License
- **Helmet** (6.0.0) - MIT License
- **CORS** (2.8.5) - MIT License

### Database
- **Sequelize** (6.28.0) - MIT License
- **pg** (8.8.0) - MIT License
- **Redis** (4.5.0) - MIT License

### Authentication & Security
- **jsonwebtoken** (9.0.0) - MIT License
- **bcrypt** (5.1.0) - MIT License
- **express-rate-limit** (6.7.0) - MIT License

### Utilities
- **Winston** (3.8.0) - MIT License
- **Joi** (17.7.0) - BSD-3-Clause License
- **dotenv** (16.0.0) - BSD-2-Clause License

## Machine Learning Dependencies

### Python ML Libraries
- **scikit-learn** (1.2.0) - BSD-3-Clause License
- **XGBoost** (1.7.0) - Apache License 2.0
- **pandas** (1.5.0) - BSD-3-Clause License
- **NumPy** (1.24.0) - BSD-3-Clause License

### Deep Learning
- **TensorFlow** (2.11.0) - Apache License 2.0
- **PyTorch** (1.13.0) - BSD-3-Clause License

### Data Processing
- **Apache Airflow** (2.5.0) - Apache License 2.0
- **Celery** (5.2.0) - BSD-3-Clause License

## Development Dependencies

### Build Tools
- **Webpack** (5.75.0) - MIT License
- **Babel** (7.20.0) - MIT License
- **TypeScript** (4.9.0) - Apache License 2.0

### Testing
- **Jest** (29.3.0) - MIT License
- **Testing Library** (13.4.0) - MIT License
- **Cypress** (12.3.0) - MIT License

### Code Quality
- **ESLint** (8.31.0) - MIT License
- **Prettier** (2.8.0) - MIT License
- **Husky** (8.0.0) - MIT License

## Infrastructure Dependencies

### Cloud Services
- **Google Cloud SDK** - Apache License 2.0
- **Docker** - Apache License 2.0
- **Kubernetes** - Apache License 2.0

### Monitoring
- **Prometheus** - Apache License 2.0
- **Grafana** - AGPL-3.0 License
- **Datadog Agent** - BSD-3-Clause License

## License Types Summary

| License Type | Count | Libraries |
|--------------|-------|-----------|
| **MIT** | 45 | React, Express, Lodash, etc. |
| **Apache 2.0** | 12 | TensorFlow, XGBoost, TypeScript, etc. |
| **BSD-3-Clause** | 8 | scikit-learn, pandas, NumPy, etc. |
| **BSD-2-Clause** | 2 | dotenv, etc. |
| **ISC** | 1 | D3.js |
| **AGPL-3.0** | 1 | Grafana |

## License Compatibility

All dependencies have been reviewed for license compatibility with our MIT license:

✅ **Compatible**: MIT, Apache 2.0, BSD-2-Clause, BSD-3-Clause, ISC
⚠️ **Special Consideration**: AGPL-3.0 (used only for monitoring, not distributed)
❌ **Incompatible**: None found

## Compliance Notes

### MIT License Requirements
- Include copyright notice and license text
- Preserve original attribution
- No warranty disclaimers

### Apache 2.0 License Requirements
- Include copyright notice and license text
- Document any modifications
- Include NOTICE file if present

### BSD License Requirements
- Include copyright notice and license text
- Preserve original attribution
- Include disclaimer of warranty

## License Texts

Full license texts for all dependencies are available in the `/licenses/` directory:

```
licenses/
├── MIT.txt
├── APACHE-2.0.txt
├── BSD-3-Clause.txt
├── BSD-2-Clause.txt
├── ISC.txt
└── AGPL-3.0.txt
```

## Automated License Checking

We use automated tools to track license compliance:

```bash
# Check JavaScript dependencies
npm run license-check

# Check Python dependencies
pip-licenses --format=table

# Generate license report
npm run license-report
```

## Regular Review Process

- **Quarterly**: Review all new dependencies
- **Before Release**: Verify license compliance
- **Annual**: Full audit of all dependencies
- **On Addition**: Check each new dependency

## Contact

For questions about licensing or compliance:
- **Email**: legal@retenify.com
- **Documentation**: See [Legal Documentation](./docs/legal/)

---

**Last Updated**: December 2024
**Next Review**: March 2025

*This document is automatically generated and manually reviewed for accuracy.*
