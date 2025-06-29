# Asset Management Guide

This document provides comprehensive guidelines for managing visual assets in the Retenify documentation repository.

## 📁 Directory Structure

The assets are organized in a logical hierarchy that supports easy navigation and maintenance:

```
assets/
├── logo/                    # Brand logos and identity
├── screenshots/             # Platform interface screenshots
├── diagrams/               # Technical diagrams and flowcharts
├── features/               # Feature-specific visuals
├── misc/                   # Miscellaneous images
└── README.md              # This documentation
```

## 🎯 Asset Categories

### 1. Brand Assets (`/logo/`)

**Purpose**: Official Retenify branding materials

**Contents**:
- Primary logo (transparent background)
- Dark mode logo variants
- Favicon and app icons
- Horizontal and vertical layouts

**Usage**: Main README, documentation headers, presentations

**Specifications**:
- Format: PNG with transparent background
- Sizes: 64x64, 128x128, 256x256, 512x512
- Color: Follow brand guidelines (#0066CC primary)

### 2. Platform Screenshots (`/screenshots/`)

**Purpose**: Real interface captures showing actual platform usage

**Contents**:
- Dashboard views (desktop and mobile)
- Feature interfaces (churn prediction, campaigns, analytics)
- User flows (onboarding, setup, configuration)
- Different states (loading, empty, error, success)

**Usage**: User guide, feature documentation, tutorials

**Specifications**:
- Format: PNG
- Resolution: 2560x1440 or 1920x1080
- Content: Anonymized sample data only
- Browser: Chrome/Safari at 100% zoom

### 3. Technical Diagrams (`/diagrams/`)

**Purpose**: System architecture and process flows

**Contents**:
- System architecture diagrams
- Data flow illustrations
- ML pipeline visualizations
- User journey maps
- Integration flows

**Usage**: Developer documentation, architecture guides

**Specifications**:
- Format: SVG preferred (scalable), PNG fallback
- Tools: Figma, Draw.io, Lucidchart
- Style: Consistent colors and notation
- Export: Optimized for web

### 4. Feature Visuals (`/features/`)

**Purpose**: Marketing and explanatory visuals for specific features

**Contents**:
- Feature overview graphics
- Benefit illustrations
- Process explanations
- Comparison charts

**Usage**: Main README, marketing materials, feature announcements

**Specifications**:
- Format: PNG or SVG
- Style: Consistent with brand guidelines
- Content: Clear, professional, branded

## 📝 Naming Conventions

### File Naming Rules

1. **Use lowercase with hyphens**: `customer-health-dashboard.png`
2. **Be descriptive**: `campaign-builder-drag-drop.png` vs `builder.png`
3. **Include context**: `dashboard-mobile-view.png`
4. **Version when needed**: `logo-v2.png`, `architecture-2024.svg`
5. **Specify state**: `onboarding-step-1.png`, `error-state.png`

### Category Prefixes

- **Screenshots**: `screen-[feature]-[view].png`
- **Diagrams**: `diagram-[type]-[subject].svg`
- **Features**: `feature-[name]-[aspect].png`
- **Logos**: `logo-[variant]-[size].png`

## 🔧 Technical Guidelines

### Image Optimization

**Automatic Optimization**:
```bash
# Install optimization tools
npm install -g imageoptim-cli
brew install jpegoptim pngquant

# Optimize PNG files
pngquant --quality=65-90 --output assets/screenshots/ assets/screenshots/*.png

# Optimize JPG files
jpegoptim --max=85 assets/misc/*.jpg
```

**Manual Optimization**:
- Use tools like TinyPNG, Squoosh, or ImageOptim
- Target: <500KB for screenshots, <100KB for icons
- Maintain visual quality while reducing file size

### Git LFS (Large File Storage)

For repositories with many large images, consider Git LFS:

```bash
# Install Git LFS
git lfs install

# Track image files
git lfs track "*.png"
git lfs track "*.jpg"
git lfs track "*.gif"

# Add .gitattributes
git add .gitattributes
git commit -m "Add Git LFS tracking"
```

### Responsive Images

For documentation that needs to work across devices:

```markdown
<!-- Standard image -->
![Dashboard](assets/screenshots/dashboard.png)

<!-- Responsive image with HTML -->
<picture>
  <source media="(max-width: 768px)" srcset="assets/screenshots/dashboard-mobile.png">
  <img src="assets/screenshots/dashboard.png" alt="Dashboard Overview">
</picture>
```

## 📖 Documentation Integration

### Markdown Usage

**Basic Image Insertion**:
```markdown
![Alt Text](assets/category/filename.png)
```

**Image with Caption**:
```markdown
![Dashboard Overview](assets/screenshots/dashboard.png)
*Figure 1: Main dashboard showing customer health metrics*
```

**Sized Images**:
```markdown
<img src="assets/diagrams/architecture.svg" alt="System Architecture" width="800">
```

### Relative Path Guidelines

From different documentation locations:

```markdown
# From main README.md
![Logo](assets/logo/logo.png)

# From docs/user-guide/README.md
![Screenshot](../../assets/screenshots/dashboard.png)

# From docs/api/README.md
![Diagram](../../assets/diagrams/api-flow.svg)
```

### Alt Text Best Practices

**Good Alt Text**:
- Descriptive: "Customer health score dashboard showing risk distribution"
- Concise: Focus on essential information
- Contextual: Relevant to surrounding content

**Poor Alt Text**:
- Generic: "Image", "Screenshot", "Diagram"
- Redundant: Repeating caption text
- Too verbose: Describing every UI element

## 🔄 Asset Lifecycle

### Creation Process

1. **Planning**: Define purpose, audience, and specifications
2. **Creation**: Use approved tools and follow guidelines
3. **Review**: Technical and brand review before adding
4. **Optimization**: Compress and optimize for web
5. **Documentation**: Update relevant docs with new assets
6. **Testing**: Verify display across devices and contexts

### Update Schedule

**Regular Updates**:
- **Screenshots**: After major UI changes (within 1 sprint)
- **Diagrams**: When architecture or processes change
- **Feature Images**: With new feature releases
- **Brand Assets**: When brand guidelines update

**Maintenance Tasks**:
- Quarterly asset audit for outdated content
- Annual optimization and cleanup
- Regular link validation in documentation
- Performance impact assessment

### Version Control

**Asset Versioning**:
```
assets/
├── screenshots/
│   ├── dashboard.png              # Current version
│   ├── dashboard-v1.png          # Previous version
│   └── dashboard-archive/         # Historical versions
└── diagrams/
    ├── architecture.svg           # Current
    └── architecture-2023.svg     # Previous year
```

**Change Documentation**:
- Commit messages should describe asset changes
- Link to relevant issues or feature requests
- Note visual changes in release notes

## 🛡️ Legal and Compliance

### Copyright and Licensing

**Original Assets**:
- All Retenify-created assets: Company ownership
- External assets: Proper licensing required
- Stock photos: Commercial license verification
- Icons: Verify usage rights

**Attribution Requirements**:
- Third-party assets: Include required attribution
- Open source images: Follow license terms
- Design tools: Check export licensing
- Fonts: Verify commercial usage rights

### Privacy and Security

**Data Protection**:
- No real customer data in screenshots
- Anonymize all personal information
- Use fictional names and companies
- Remove sensitive system information

**Security Considerations**:
- No API keys or credentials visible
- Obscure internal URLs and endpoints
- Remove debug information
- Check for inadvertent data exposure

## 🎨 Brand Consistency

### Visual Guidelines

**Color Palette**:
- Primary: #0066CC (Retenify Blue)
- Secondary: #6B7280 (Neutral Gray)
- Success: #10B981 (Green)
- Warning: #F59E0B (Orange)
- Error: #EF4444 (Red)

**Typography**:
- Primary: Inter (web), San Francisco (macOS), Segoe UI (Windows)
- Monospace: JetBrains Mono, Consolas, Monaco
- Ensure consistent font usage in diagrams

**Layout Standards**:
- Consistent spacing and alignment
- Clear visual hierarchy
- Professional appearance
- Accessibility compliance

### Quality Standards

**Technical Quality**:
- Sharp, high-resolution images
- Consistent lighting and contrast
- Professional composition
- Error-free content

**Content Quality**:
- Accurate representation of features
- Current interface versions
- Representative use cases
- Clear value demonstration

## 🚀 Automation and Tools

### Automated Workflows

**CI/CD Integration**:
```yaml
# GitHub Actions example
name: Optimize Images
on: [push]
jobs:
  optimize:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Optimize images
        uses: calibreapp/image-actions@main
        with:
          githubToken: ${{ secrets.GITHUB_TOKEN }}
          compressOnly: true
```

**Pre-commit Hooks**:
```bash
# Install pre-commit
pip install pre-commit

# Add to .pre-commit-config.yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.0.1
    hooks:
      - id: check-added-large-files
        args: ['--maxkb=500']
```

### Useful Tools

**Image Optimization**:
- [TinyPNG](https://tinypng.com/) - PNG/JPG compression
- [Squoosh](https://squoosh.app/) - Advanced image optimization
- [ImageOptim](https://imageoptim.com/) - Mac image optimization

**Design Tools**:
- [Figma](https://figma.com/) - Collaborative design
- [Draw.io](https://draw.io/) - Free diagramming
- [Canva](https://canva.com/) - Quick graphics creation

**Screenshot Tools**:
- [CleanShot X](https://cleanshot.com/) - Professional screenshots (macOS)
- [Greenshot](https://getgreenshot.org/) - Free screenshot tool (Windows)
- [GoFullPage](https://gofullpage.com/) - Full page browser screenshots

This comprehensive asset management approach ensures that all visual materials in the Retenify documentation maintain professional quality, brand consistency, and technical excellence while supporting the project's public accessibility goals.
