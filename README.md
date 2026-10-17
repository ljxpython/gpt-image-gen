# 🎨 gpt-image-gen

> **生产级 AI Agent 视觉工艺师 (Production-Grade Visual Crafting Skill for AI Agents)**  
> 专为现代 AI Coding Agent（Antigravity、Cursor、Claude Code、OpenCode 等）量身打造的高可用、渐进式、高保真生图与视觉工程技能。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-brightgreen.svg)](https://www.python.org/)
[![OpenAI-Compatible](https://img.shields.io/badge/API-OpenAI--Compatible-orange.svg)](https://platform.openai.com/)
[![Zero-Cost Linter](https://img.shields.io/badge/Linter-Zero--Token--Cost-brightgreen.svg)](#-零成本本地静态-linter)

---

## 🌟 核心价值主张 (Why gpt-image-gen?)

现代 AI Coding Agent 擅长编写代码与分析文档，但在**生成专业级技术图纸、知识卡片与社媒爆款图文**时，普遍面临四大工程痛点：

1. **上下文爆炸 (Context Bloat)**：把几十套生图提示词全部塞进 Agent 提示词，消耗上万 Tokens，模型严重降智。
2. **文本乱码翻车 (Hallucination & Glitches)**：扩散模型在处理高密度中文与多重小卡片时，文字粘连变形。
3. **单点故障 (SPOF)**：单一网关偶发 502/429 报错，导致 Agent 整体工作流中断。
4. **教条僵化缺乏灵性**：机械套用固定骨架，出图千篇一律、死气沉沉。

**`gpt-image-gen` 通过严谨的软件工程架构彻底攻克上述难题：**

```
用户需求 ("画一张复古素描学霸手账")
   │
   ▼ (冷启动仅 50~80 Tokens 元数据)
[意图路由决策矩阵] ──► 精准单点抽取 target.yaml (约 400~500 Tokens，渐进式加载)
   │
   ▼
[零成本静态 Linter] ──► 0 Token 消耗提前排查超长字段与语法缺陷
   │
   ▼
[多网关高可用调度引擎] ──► 主备网关自动故障转移 + 指数退避重试 (Failover)
   │
   ▼
[高保真渲染成图] ──► 100% 物理留存，自动校验图片完整度
```

---

## 🏛️ 核心架构特性

### 1. ⚡️ 极轻量渐进式加载 (Progressive Disclosure)
- **冷启动零负担**：常态下 Agent 仅挂载轻量元数据（`name` + `description`），占用小于 **80 Tokens**。
- **单模板按需注入**：内置路由决策矩阵（Decision Matrix）。仅当命中生图意图时，才单点拉取目标 `.yaml` 模板（约 **400~500 Tokens**），其余模板安睡于磁盘，绝不污染上下文。

### 2. 🛡️ 零成本本地静态 Linter
在呼叫任何昂贵的生图 API 之前，`generate.py` 会自动执行本地语法检查：
- 结构化 JSON 校验
- 关键文本预算审计（Text Budget Audit）
- 负向提示词安全性检查  
**全程本地计算，0 Token 消耗，0 成本！**

### 3. 🔄 双网关高可用自动容灾 (HA Failover & Exponential Backoff)
- 支持本地工程级 `.env` 与全局配置双通道自动探测。
- 遇 429 限流或 5xx 故障，自动启动指数退避重试（2s ➔ 4s ➔ 8s）并无缝降级转移至备用网关。

### 4. 🎨 沉淀 11+ 生产验证视觉流派模板
涵盖从严肃大厂技术架构到社媒爆款视觉全矩阵：
- **Style 01: 学霸手绘手账知识地图** (`sketchnote-knowledge-map.yaml`)
- **Style 02: 现代学院派方格手绘笔记** (`studygram-swiss-grid.yaml`)
- **Style 03: 极客活页草稿本手记** (`binder-geek-guide.yaml`)
- **Style 04: 线圈手账便签拼贴风** (`spiral-notebook-scrapbook.yaml`)
- **Style 05: 可爱日漫少女手账指南** (`cute-anime-studygram.yaml`)
- **Style 06: 大厂生产架构全景图** (`enterprise-architecture-blueprint.yaml`)
- **Style 07: 全景自检互动式架构栈** (`diagnostic-architecture-stack.yaml`)
- **Style 08: 单列流式五层技能流水线** (`linear-skills-pipeline.yaml`)
- **Style 09: 治愈系彩泥定格手账套图** (`claymation-studygram-guide.yaml`)
- **Style 10: 复古线圈素描学霸手记** (`vintage-sketchbook-studygram.yaml`)
- **Style 11: 萌系马卡龙手账清单** (`kawaii-planner-checklist.yaml`)

---

## 🖼️ 实机效果展示 (Showcase)

| 样式流派 | 实机效果图 | 特性亮点 |
| :--- | :--- | :--- |
| **Style 10: 复古线圈素描学霸手记** | ![Style 10](assets/showcase/sample-18-vintage-sketchbook-studygram.png) | 真实金属双螺旋打孔、黑墨水笔素描排线、焦糖淡彩、伏案少女 |
| **Style 11: 萌系马卡龙手账清单** | ![Style 11](assets/showcase/sample-19-kawaii-planner-declutter-checklist.png) | 方格纸手账、8 宫格色彩矩阵、和纸胶带、高密度物品手绘 |
| **反常识极限实测: 800字仿真手写信** | ![800w Letter](assets/showcase/sample-20-simulated-letter-800w.png) | 单栏自然线性流，95%+ 真实汉字高保真手写行楷，墨水渗透质感 |
| **Style 09: 治愈彩泥手账套图 (P1+P2)** | ![Style 09](assets/showcase/sample-16-claymation-p1-cover-v2.png) | 真实微距移轴、3D 黏土捏制质感、小熊白兔吉祥物、卡片式工作流 |
| **Style 06: 企业级生产架构全景图** | ![Style 06](assets/showcase/sample-13-mimic-enterprise-arch-iceblue.png) | 纯白矢量底、三栏翼展工业拓扑、纯中文无乱码、浅冰蓝中枢 |

---

## 🚀 快速上手 (Quick Start)

### 1. 配置环境变量
在项目根目录创建 `.env` 文件：
```bash
cp .env.example .env
```
填写你的 OpenAI-Compatible 图像生成服务商凭据：
```env
IMAGE_25_URL="https://api.openai.com/v1"
IMAGE_25_MODEL="gpt-image-2.5"
IMAGE_25_KEY="your-api-key-here"
```

### 2. 独立 CLI 命令行使用
```bash
# 1. 基础生图
python3 scripts/generate.py "Prompt 内容" -o output.png -s 1024x1024

# 2. 高质量竖版比例 (适用于小红书/手机知识卡片)
python3 scripts/generate.py "Prompt 内容" -o card.png -s 1024x1536 -q high

# 3. 零成本本地 Prompt 校验 (不消耗任何 Token 和 API 费用)
python3 scripts/generate.py "Prompt 内容" --lint

# 4. 零成本网络健康探针检查
python3 scripts/generate.py "Prompt 内容" --dry-run
```

### 3. 集成到 AI Coding Agent

#### 针对 Antigravity / Gemini CLI:
将本技能克隆或软链接至技能目录即可自动识别：
```bash
git clone https://github.com/ljxpython/gpt-image-gen.git ~/.gemini/config/skills/gpt-image-gen
```

#### 针对 Cursor / Claude Code / 项目级使用:
直接放入项目 `.agents/skills/` 目录：
```bash
git clone https://github.com/ljxpython/gpt-image-gen.git <your-project>/.agents/skills/gpt-image-gen
```

---

## 📐 设计哲学与黄金准则

本项目践行**“去教条化的艺术灵性”**：

1. **色彩克制与呼吸通透 (Color Harmony)**：
   - 拒绝杂乱刺眼的大红大绿碰撞。底色与主视觉保持协调（低饱和或同色阶统合），点缀色适度提神。
   - 避免在提示词中堆砌冲突的高饱和原色，防止扩散模型产生 **Color Bleeding（颜色渗漏污染）**。
2. **主次分明与空间呼吸 (Visual Hierarchy)**：
   - **文字是主角，装饰是绿叶**：配图与装饰只烘托氛围，严禁遮挡、压盖文字主体。
   - **构图灵动透气**：不拘泥死板骨架，根据内容自然排版流动，留足呼吸空间。

---

## 🤝 贡献与共创

欢迎提交新的视觉风格模板（位于 `templates/`）和测试用例！
1. Fork 本仓库
2. 创建你的特性分支 (`git checkout -b feature/new-style-template`)
3. 提交变更 (`git commit -m 'Add new style template'`)
4. 推送分支 (`git push origin feature/new-style-template`)
5. 新建 Pull Request

---

## 📄 License

本项目采用 [MIT License](LICENSE) 开源协议。
