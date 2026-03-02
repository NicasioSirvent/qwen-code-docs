# Vision Models and Multimodal Capabilities

## Overview

Qwen Code supports vision-enabled models that can analyze images, diagrams, screenshots, and other visual content. This allows you to get AI assistance for visual tasks like UI review, architecture diagram analysis, and screenshot-based debugging.

---

## Supported Visual Inputs

| Input Type | Description | Example Use Cases |
|------------|-------------|-------------------|
| **Images** | PNG, JPG, GIF, WEBP | Screenshots, diagrams, photos |
| **PDFs** | Multi-page documents | Technical docs, specifications |
| **Diagrams** | Architecture charts, flowcharts | System design review |
| **UI Screenshots** | Application interfaces | UI/UX feedback |

---

## How to Use Vision Models

### 1. Attach an Image to Your Question

**In Interactive Mode:**
```
@path/to/image.png Explain what this architecture diagram shows
```

**Drag and Drop:**
Simply drag an image file into the Qwen Code terminal.

### 2. Ask Vision-Based Questions

```
@src/assets/mockup.png Suggest improvements to this UI design
```

```
@diagrams/architecture.png Review this system architecture for potential bottlenecks
```

```
@screenshot.png What's causing this error message?
```

### 3. Analyze Multiple Images

```
@before.png @after.png Compare these two designs and explain the differences
```

---

## Common Use Cases

### 1. UI/UX Review

```
@mockup.png Review this landing page design and suggest improvements for conversion
```

### 2. Architecture Diagram Analysis

```
@system-design.png Explain the data flow in this architecture and identify single points of failure
```

### 3. Error Screenshot Debugging

```
@error-screenshot.png What does this error mean and how do I fix it?
```

### 4. Documentation from Images

```
@whiteboard-photo.png Convert this whiteboard diagram into markdown documentation
```

### 5. Code from Screenshots

```
@legacy-code.png Convert this code screenshot into editable text
```

---

## Configuration

### Enable Vision Models

In your settings file (`.qwen/settings.json` or `~/.qwen/settings.json`):

```json
{
  "model": {
    "name": "qwen-vl-plus"
  },
  "visionSettings": {
    "maxImageSize": 2048,
    "imageQuality": 0.8
  }
}
```

### Environment Variables

```bash
# For Qwen Vision API
export QWEN_API_KEY="your-api-key"
```

---

## Best Practices

### 1. Image Quality

- Use clear, high-resolution images for best results
- Ensure text in screenshots is readable
- Crop to relevant areas when possible

### 2. Be Specific in Your Prompts

| Vague Prompt | Specific Prompt |
|--------------|-----------------|
| "Analyze this" | "Review this UI design for accessibility issues" |
| "What's wrong?" | "Identify the error in this stack trace screenshot" |
| "Explain this" | "Explain the data flow shown in this architecture diagram" |

### 3. Provide Context

```
@api-diagram.png This is our current microservices architecture. We're experiencing latency issues. Identify potential bottlenecks.
```

### 4. Use Appropriate Image Formats

| Format | Best For |
|--------|----------|
| PNG | Screenshots, diagrams with text |
| JPG | Photos, complex images |
| GIF | Simple animations |
| PDF | Multi-page documents |

---

## Limitations

| Limitation | Description |
|------------|-------------|
| **Image Size** | Maximum 2048x2048 pixels recommended |
| **File Size** | Images over 10MB may be compressed |
| **Text Recognition** | Handwritten text may not be accurately recognized |
| **Complex Diagrams** | Very dense diagrams may need simplified views |

---

## Troubleshooting

### Image Not Processing

1. **Check file format**: Ensure image is PNG, JPG, GIF, WEBP, or PDF
2. **Verify file size**: Large files may need compression
3. **Check path**: Ensure the file path is correct

### Poor Quality Results

1. **Increase image resolution**: Use clearer, higher-quality images
2. **Provide more context**: Add details about what you're looking for
3. **Try a different model**: Some models have better vision capabilities

---

## Related Documentation

- [Commands](./commands) — Using @ file references
- [Configuration](../configuration/settings) — Model settings
- [Skills](./skills) — Create vision-processing skills

---

*Last updated: March 2, 2026*
