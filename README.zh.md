# VibeDoc：AI 产品经理与架构师

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Gradio](https://img.shields.io/badge/Gradio-5.34.1-orange)](https://gradio.app/)
[![GitHub stars](https://img.shields.io/github/stars/calderbuild/VibeDoc?style=social)](https://github.com/calderbuild/VibeDoc)

<div align="center">

**一句产品想法，1 到 3 分钟生成完整开发方案**

OpenManus Hackathon 最佳选题奖（Best Topic Award）

[在线体验](https://modelscope.cn/studios/JasonRobert/Vibedocs) | [演示视频](https://www.bilibili.com/video/BV1ieagzQEAC/) | [问题反馈](https://github.com/calderbuild/VibeDoc/issues) | [English](./README.md)

</div>

---

## 这是什么

VibeDoc 把一个粗糙的产品想法，变成原本要花好几天写的开发方案：产品概述、带 Mermaid 图的技术架构、分阶段开发计划，以及可以直接交给 AI 编程工具的提示词。结果可以导出为 Markdown、Word、PDF 或 HTML。

它解决的是从「有个想法」到「可以开始写代码」之间的那段空白：

- 有想法，但不知道怎么变成可执行的开发计划。
- 写技术方案、架构文档太花时间。
- 想用 AI 辅助编程，但写不好提示词。
- 需要架构图、流程图、甘特图，又不熟悉画图工具。

![VibeDoc 主界面](./image/vibedoc.png)

## 核心功能

### 开发方案生成

输入产品想法，VibeDoc 生成：

- **产品概述**：项目背景、目标用户、核心价值
- **技术方案**：技术选型、架构设计、技术对比
- **开发计划**：分阶段实施、时间安排、人力配置
- **部署方案**：环境配置、CI/CD、运维监控
- **增长策略**：市场定位、运营建议、增长手段

### AI 编程提示词

为每个功能模块生成可直接使用的提示词，适配 Claude、GitHub Copilot、ChatGPT 和 Cursor。

![AI 编程提示词](./image/1.png)

### 可视化图表

基于 Mermaid 生成系统架构图、业务流程图、甘特图和技术对比表。

### 多格式导出

| 格式 | 适用场景 |
|------|----------|
| Markdown (.md) | 版本控制、GitHub 展示 |
| Word (.docx) | 商务文档、项目汇报 |
| PDF (.pdf) | 正式提案、打印归档 |
| HTML (.html) | 网页展示、在线分享 |

![生成示例](./image/2.png)

## 案例

输入：

```
开发一款AR手语翻译应用，能够实时将手语翻译成语音和文字，
同时也能将语音和文字翻译成手语动作，以AR形式展示
```

输出：[完整开发方案](./HandVoice_Development_Plan.md)，包括：

1. **产品概述**：目标用户（听障人群、医疗工作者、教育工作者）、核心功能、市场定位
2. **技术架构**：用 Mermaid 画出用户界面、后端服务、机器学习模型集成、数据库和 AR 渲染管线
3. **技术栈**：React Native、Node.js + Express、TensorFlow、spaCy、ARKit / ARCore、MongoDB
4. **开发时间表**：6 个月，3 个里程碑
5. **AI 编程提示词**：每个模块一条，例如：

```
功能：手势识别模型

上下文：
构建实时手势识别系统用于手语翻译。
需要检测和分类手部位置、动作和面部表情。

需求：
- 处理30+ FPS的视频帧
- 识别500+种手语手势
- 支持连续手势序列
- 处理不同光照条件

技术栈：
- TensorFlow/Keras 模型训练
- MediaPipe 手部关键点检测
- OpenCV 图像预处理

约束条件：
- 必须在移动设备运行 (iOS/Android)
- 模型大小 < 50MB 用于移动部署
- 推理时间 < 100ms 每帧

期望输出：
- 模型架构代码
- 训练管道
- 数据预处理函数
- 移动端优化策略
```

## 快速开始

### 在线体验

[在魔搭创空间体验 VibeDoc](https://modelscope.cn/studios/JasonRobert/Vibedocs)，无需安装：

1. 输入产品想法（例如「开发一个智能健身 App」）。
2. 可选填写参考链接，补充上下文。
3. 点击生成，等待 1 到 3 分钟。
4. 查看开发方案和 AI 编程提示词。
5. 导出为 Markdown、Word、PDF 或 HTML。

### 本地部署

环境要求：Python 3.11+，以及一个 [SiliconFlow API Key](https://siliconflow.cn)（免费注册）。

```bash
git clone https://github.com/calderbuild/VibeDoc.git
cd VibeDoc

python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

pip install -r requirements.txt
cp .env.example .env          # 然后填入 API Key
```

`.env`：

```env
# 必填
SILICONFLOW_API_KEY=your_api_key_here

# 可选
API_TIMEOUT=300
LOG_LEVEL=INFO
ENVIRONMENT=production
```

运行：

```bash
python app.py
```

应用启动在 http://localhost:7860。

### Docker

```bash
docker build -t vibedoc .
docker run -p 7860:7860 -e SILICONFLOW_API_KEY=your_key vibedoc
```

## 技术架构

```
┌─────────────────────────────────────────┐
│         Gradio Web Interface            │
│  (用户交互 + UI渲染 + 文件导出)           │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│       核心处理引擎 (app.py)              │
├─────────────────────────────────────────┤
│  • 输入验证与优化                        │
│  • AI生成协调                           │
│  • 内容质量控制                          │
│  • 多格式导出                            │
└──┬────────┬──────────┬─────────┬────────┘
   │        │          │         │
   ▼        ▼          ▼         ▼
┌──────┐ ┌────────┐ ┌──────┐ ┌──────────┐
│AI模型│ │提示词  │ │内容  │ │导出      │
│集成  │ │优化器  │ │验证  │ │管理器    │
└──────┘ └────────┘ └──────┘ └──────────┘
```

技术栈：

- **界面**：Gradio 5.34.1
- **模型**：Qwen2.5-72B-Instruct，通过 SiliconFlow API 调用
- **图表**：Mermaid.js
- **导出**：python-docx、reportlab
- **异步**：asyncio、aiofiles

## 适合谁

- **开发者**：验证技术可行性，生成项目文档，获取 AI 编程提示词。
- **产品经理**：把需求转成技术方案，估算周期，撰写提案。
- **创业者**：验证想法，规划 MVP，准备给投资人看的技术方案。
- **学生**：学习架构设计，准备技术面试，规划毕业设计。

## 参与贡献

欢迎提交 Bug、功能建议、文档改进和代码。

1. Fork 本仓库。
2. 创建分支（`git checkout -b feature/your-feature`）。
3. 提交改动。
4. 推送分支并发起 Pull Request。

## 交流群

<div align="center">
<img src="./image/discussion_group.jpg" width="300" alt="VibeDoc 交流群二维码">

扫码加入 VibeDoc 交流群。
</div>

## 文档

- [部署指南](./DEPLOYMENT.md)
- [安全策略](./SECURITY.md)
- [贡献与开发约定](./AGENTS.md)

## 路线图

- [ ] 支持更多模型（GPT-4、Claude 等）
- [ ] 团队协作
- [ ] 方案版本管理
- [ ] 在线编辑器
- [ ] 移动端适配
- [ ] 模板市场
- [ ] API 接口

## 致谢

- 阿里云 Qwen2.5-72B-Instruct
- Gradio
- SiliconFlow

## 开源协议

[MIT License](LICENSE)

## 联系方式

- **问题反馈**：[GitHub Issues](https://github.com/calderbuild/VibeDoc/issues)
- **邮箱**：johnrobertdestiny@gmail.com
- **演示视频**：[Bilibili](https://www.bilibili.com/video/BV1ieagzQEAC/)

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=calderbuild/VibeDoc&type=Date)](https://star-history.com/#calderbuild/VibeDoc&Date)
