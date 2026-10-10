# VibeDoc: AI Product Manager and Architect

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Gradio](https://img.shields.io/badge/Gradio-5.34.1-orange)](https://gradio.app/)
[![GitHub stars](https://img.shields.io/github/stars/calderbuild/VibeDoc?style=social)](https://github.com/calderbuild/VibeDoc)

<div align="center">

**Turn a one-line product idea into a complete development plan in 1 to 3 minutes**

Best Topic Award, OpenManus Hackathon

[Online Demo](https://modelscope.cn/studios/JasonRobert/Vibedocs) | [Demo Video](https://www.bilibili.com/video/BV1ieagzQEAC/) | [Issues](https://github.com/calderbuild/VibeDoc/issues) | [中文文档](./README.zh.md)

</div>

---

## What it is

VibeDoc takes a rough product idea and writes the plan you would otherwise spend days on: a product overview, a technical architecture with Mermaid diagrams, a phased development plan, and ready-to-use prompts for AI coding tools. You can export the result as Markdown, Word, PDF, or HTML.

It is built for the gap between "I have an idea" and "I can start coding":

- You have an idea but no actionable plan.
- Writing specs and architecture docs takes too long.
- You want AI coding tools to help, but writing good prompts is hard.
- You need architecture, flow, and Gantt charts without a diagramming tool.

![VibeDoc Interface](./image/vibedoc.png)

## Features

### Development plan generation

Enter a product idea and VibeDoc generates:

- **Product overview**: background, target users, core value
- **Technical solution**: stack selection, architecture design, technology comparison
- **Development plan**: phases, timeline, resource allocation
- **Deployment strategy**: environment setup, CI/CD, monitoring
- **Growth strategy**: positioning, operations, growth tactics

### AI coding prompts

Ready-to-use prompts for each feature module, written for Claude, GitHub Copilot, ChatGPT, and Cursor.

![AI Coding Prompts](./image/1.png)

### Diagrams

Mermaid-rendered system architecture diagrams, business flowcharts, Gantt charts, and technology comparison tables.

### Export

| Format | Good for |
|--------|----------|
| Markdown (.md) | Version control, GitHub |
| Word (.docx) | Business documents, reports |
| PDF (.pdf) | Formal proposals, archiving |
| HTML (.html) | Web display, sharing |

![Generated Example](./image/2.png)

## Example

Input:

```
Develop an AR sign language translation app that can translate sign language
into voice and text in real-time, and also translate voice and text into
sign language gestures displayed in AR
```

Output: [the complete development plan](./HandVoice_Development_Plan.md). It covers:

1. **Product overview**: target users (deaf community, healthcare workers, educators), core features, positioning
2. **Technical architecture**: Mermaid diagrams for UI, backend services, ML model integration, database, AR rendering
3. **Technology stack**: React Native, Node.js + Express, TensorFlow, spaCy, ARKit / ARCore, MongoDB
4. **Timeline**: a 6-month plan with 3 milestones
5. **AI coding prompts**: one per module, for example:

```
Feature: Hand Gesture Recognition Model

Context:
Building a real-time hand gesture recognition system for sign language translation.
Need to detect and classify hand positions, movements, and facial expressions.

Requirements:
- Process video frames at 30+ FPS
- Recognize 500+ sign language gestures
- Support continuous gesture sequences
- Handle varying lighting conditions

Tech Stack:
- TensorFlow/Keras for model training
- MediaPipe for hand landmark detection
- OpenCV for image preprocessing

Constraints:
- Must run on mobile devices (iOS/Android)
- Model size < 50MB for mobile deployment
- Inference time < 100ms per frame

Expected Output:
- Model architecture code
- Training pipeline
- Data preprocessing functions
- Mobile optimization strategies
```

## Quick Start

### Online demo

[Try VibeDoc on ModelScope](https://modelscope.cn/studios/JasonRobert/Vibedocs), no installation needed:

1. Enter your product idea (for example, "Build a smart fitness app").
2. Optionally add reference URLs for context.
3. Click generate and wait 1 to 3 minutes.
4. Review the plan and the AI coding prompts.
5. Export to Markdown, Word, PDF, or HTML.

### Local installation

Prerequisites: Python 3.11+ and a [SiliconFlow API key](https://siliconflow.cn) (free to register).

```bash
git clone https://github.com/calderbuild/VibeDoc.git
cd VibeDoc

python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

pip install -r requirements.txt
cp .env.example .env          # then add your API key
```

`.env`:

```env
# Required
SILICONFLOW_API_KEY=your_api_key_here

# Optional
API_TIMEOUT=300
LOG_LEVEL=INFO
ENVIRONMENT=production
```

Run:

```bash
python app.py
```

The app starts at http://localhost:7860.

### Docker

```bash
docker build -t vibedoc .
docker run -p 7860:7860 -e SILICONFLOW_API_KEY=your_key vibedoc
```

## Architecture

```
┌─────────────────────────────────────────┐
│         Gradio Web Interface            │
│   (User Interaction + UI + Export)      │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│       Core Processing Engine            │
├─────────────────────────────────────────┤
│  • Input Validation & Optimization      │
│  • AI Generation Coordination           │
│  • Content Quality Control              │
│  • Multi-format Export                  │
└──┬────────┬──────────┬─────────┬────────┘
   │        │          │         │
   ▼        ▼          ▼         ▼
┌──────┐ ┌─────────┐ ┌─────────┐ ┌────────┐
│ AI   │ │ Prompt  │ │ Content │ │ Export │
│Model │ │Optimizer│ │Validator│ │Manager │
└──────┘ └─────────┘ └─────────┘ └────────┘
```

Tech stack:

- **UI**: Gradio 5.34.1
- **Model**: Qwen2.5-72B-Instruct via the SiliconFlow API
- **Diagrams**: Mermaid.js
- **Export**: python-docx, reportlab
- **Async**: asyncio, aiofiles

## Who it is for

- **Developers**: check technical feasibility, generate project docs, get AI coding prompts.
- **Product managers**: turn requirements into a technical plan, estimate timelines, draft proposals.
- **Founders**: validate an idea, plan an MVP, prepare a technical plan for investors.
- **Students**: learn architecture design, prepare for interviews, plan a graduation project.

## Contributing

Bug reports, feature ideas, documentation fixes, and code are all welcome.

1. Fork the repository.
2. Create a branch (`git checkout -b feature/your-feature`).
3. Commit your changes.
4. Push the branch and open a pull request.

## Community

<div align="center">
<img src="./image/discussion_group.jpg" width="300" alt="VibeDoc Community QR Code">

Scan to join the VibeDoc community group.
</div>

## Documentation

- [Deployment Guide](./DEPLOYMENT.md)
- [Security Policy](./SECURITY.md)
- [Contributor and agent guidelines](./AGENTS.md)

## Roadmap

- [ ] More models (GPT-4, Claude, etc.)
- [ ] Team collaboration
- [ ] Plan version management
- [ ] Online editor
- [ ] Mobile support
- [ ] Template marketplace
- [ ] API

## Acknowledgments

- Qwen2.5-72B-Instruct by Alibaba Cloud
- Gradio
- SiliconFlow

## License

[MIT License](LICENSE)

## Contact

- **Issues**: [GitHub Issues](https://github.com/calderbuild/VibeDoc/issues)
- **Email**: johnrobertdestiny@gmail.com
- **Demo video**: [Bilibili](https://www.bilibili.com/video/BV1ieagzQEAC/)

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=calderbuild/VibeDoc&type=Date)](https://star-history.com/#calderbuild/VibeDoc&Date)
