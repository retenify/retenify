# Assets Directory Structure

This directory contains all static resources used in documentation and the main README.

## Directory Structure

```
assets/
├── logo/
│   ├── logo.png                # Primary logo (transparent background, for docs/README)
│   ├── logo-dark.png           # For dark backgrounds
│   └── favicon.ico             # Favicon for web docs
├── screenshots/
│   ├── dashboard.png           # Example dashboard screenshot
│   ├── onboarding.png          # Onboarding flow screenshot
│   ├── churn-prediction.png    # Churn prediction interface
│   ├── campaign-builder.png    # Campaign creation interface
│   ├── health-scores.png       # Customer health scoring view
│   ├── analytics.png           # Analytics dashboard
│   └── mobile-view.png         # Mobile responsive design
├── diagrams/
│   ├── architecture.svg        # System architecture diagram
│   ├── data-flow.svg           # Data flow diagram
│   ├── ml-pipeline.svg         # Machine learning pipeline
│   ├── user-journey.svg        # Customer journey mapping
│   └── integration-flow.svg    # Integration architecture
├── features/
│   ├── feature-overview.png    # Visual summary of all features
│   ├── churn-prediction.png    # Churn prediction feature highlight
│   ├── segmentation.png        # Customer segmentation feature
│   ├── automation.png          # Campaign automation feature
│   ├── analytics.png           # Analytics and reporting feature
│   └── integrations.png        # Third-party integrations feature
└── misc/
    ├── team-photo.jpg          # Team photo for about section
    ├── office.jpg              # Office/workspace images
    ├── success-stories.png     # Customer success story graphics
    └── awards.png              # Industry awards and recognition
```

## Usage Guidelines

### In Documentation
Reference images using relative paths from the document location:

```markdown
# From main README.md
![Retenify Dashboard](assets/screenshots/dashboard.png)

# From docs/ subdirectories
![Architecture](../assets/diagrams/architecture.svg)
```

### Best Practices

#### Image Specifications
- **Screenshots**: PNG format, 1920x1080 or 2560x1440 for high-DPI displays
- **Logos**: PNG with transparent background, multiple sizes (64x64, 128x128, 256x256)
- **Diagrams**: SVG preferred for scalability, PNG fallback if needed
- **Photos**: JPG format, optimized for web (< 500KB when possible)

#### Naming Convention
- Use lowercase with hyphens: `churn-prediction.png`
- Be descriptive: `dashboard-mobile-view.png` vs `mobile.png`
- Include version if multiple iterations: `logo-v2.png`

#### Organization
- Keep related images together in appropriate subdirectories
- Maintain consistent aspect ratios within categories
- Remove outdated images when features change

## Asset Sources

### Screenshots
- Capture at 2x resolution for Retina displays
- Use clean, representative data (no customer PII)
- Ensure consistent UI state (proper navigation, clean data)
- Include browser chrome only when necessary

### Diagrams
- Created with tools like Figma, Draw.io, or Lucidchart
- Export as SVG for best quality and scalability
- Use consistent color scheme matching brand guidelines
- Include source files in project management tools

### Logos and Branding
- Follow brand guidelines for colors and usage
- Maintain vector source files (.ai, .sketch, .figma)
- Provide multiple formats and sizes
- Include usage guidelines for external use

## Maintenance

### Regular Updates
- Screenshot updates with major UI changes
- Diagram updates with architecture changes
- Logo updates with brand evolution
- Performance optimization (compress images)

### Quality Control
- Review images for outdated content quarterly
- Ensure all referenced images exist and load properly
- Optimize file sizes without quality loss
- Validate image accessibility (alt text in docs)

## Tools and Resources

### Recommended Tools
- **Screenshots**: CleanShot X, Snagit, or built-in OS tools
- **Diagrams**: Figma, Draw.io, Lucidchart, Miro
- **Image Optimization**: TinyPNG, ImageOptim, Squoosh
- **Batch Processing**: ImageMagick, GIMP batch processing

### Browser Extensions
- **Full Page Screenshots**: GoFullPage, Awesome Screenshot
- **Design Tools**: Figma browser extension
- **Color Picker**: ColorZilla for brand consistency

## Contributing Images

When contributing new images:

1. **Follow naming conventions** described above
2. **Optimize file sizes** before committing
3. **Update documentation** that references the images
4. **Test on different devices** to ensure proper display
5. **Include alt text** in documentation for accessibility

## Image Optimization

### Automated Optimization
Consider setting up automated image optimization in CI/CD:

```yaml
# Example GitHub Action for image optimization
- name: Optimize Images
  uses: calibreapp/image-actions@main
  with:
    githubToken: ${{ secrets.GITHUB_TOKEN }}
    compressOnly: true
```

### Manual Optimization
- PNG: Use tools like TinyPNG or pngquant
- JPG: Optimize with quality setting 80-85%
- SVG: Remove unnecessary metadata and comments

---

*For questions about asset usage or contributions, contact the design team or maintainers.*
