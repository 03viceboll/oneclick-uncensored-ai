# OneClick-Uncensored-LLM 🚀

![OneClick Uncensored LLM Banner](banner.jpg)

> **一键在廉价云端 GPU (Clore.ai ~$0.15/h) 自动化部署 Hugging Face 无审查大模型，秒级生成标准 OpenAI 兼容接口。**  
> **1-Click deploy any uncensored LLM from Hugging Face on cheap GPU cloud instances with zero pip dependencies.**

[![GitHub stars](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-brightgreen.svg)](https://www.python.org/)
[![Zero-Pip](https://img.shields.io/badge/dependencies-0%20pip-orange.svg)](app.py)

---

## 🇨🇳 中文说明 (Chinese)

### 痛点与背景
当前各大商业大模型（OpenAI、Claude、甚至是部分国内中转 API）审查越来越严格，频繁出现拒绝回答、上下文拦截甚至封号风控。  
**OneClick-Uncensored-LLM** 是一个纯 Python 标准库编写的本地轻量化工具，无需安装任何复杂的 pip 依赖包。它通过 API 自动在 Clore.ai 挑选最高性价比的算力卡（如 RTX 3090 / 4090，价格低至 $0.08 - $0.15/小时），根据 Hugging Face 权重格式自动匹配最适合的推理引擎（vLLM / TabbyAPI / llama.cpp），一键暴露标准的 OpenAI 格式接口，随开随用，用完一键释放销毁！

### 核心特性
1. **零 pip 依赖 (Zero-Dependency)**：完全基于 Python 3 标准库，无需 `pip install` 各种地狱级依赖包，开箱即用。
2. **多引擎智能匹配 (Auto-Engine Selector)**：
   - `safetensors / AWQ / GPTQ / FP8` -> 自动配置 **vLLM** 高并发引擎
   - `GGUF` -> 自动编译启动 **llama.cpp server** (CUDA 极致加速)
   - `EXL2 / EXL3` -> 自动配置 **TabbyAPI (ExLlamaV3)** 压榨显存极限
3. **显存智能测算与劣质节点拉黑**：
   - 自动解析目标模型的 `config.json` 计算所需显存大小（VRAM）。
   - 自动在算力市场匹配最低价达标实例。
   - 自动心跳检测：若机器 5 分钟内无响应或下载网速过慢，自动拉黑坏节点并重选。
4. **全平台前端无缝接入**：
   - 自动生成 `http://<ip>:<port>/v1/chat/completions` API 与专属 Bearer Token。
   - 完美直连 **NextChat**, **New-API / One-API**, **Chatbox**, **OpenCode**, **Cursor**, **VSCode Cline** 等。
5. **一键释放销毁**：测试或跑完任务后，本地点击停止即可立刻退租服务器，拒绝多花一分冤枉钱。

### 推荐热门无审查模型
- `Qwen/Qwen2.5-72B-Instruct` / `Qwen2.5-72B-Instruct-Uncensored` (通义千问最强开源版)
- `meta-llama/Llama-3.3-70B-Instruct-Abliterated`
- `mistralai/Mistral-Small-24B-Instruct-2501`

### 极速上手 (Quick Start)
1. 克隆本仓库：
   ```bash
   git clone https://github.com/03viceboll/oneclick-uncensored-ai.git
   cd oneclick-uncensored-llm
   ```
2. 启动本地控制面板：
   - **Windows**: 双击运行 `ui.bat`
   - **Linux / macOS**: 运行 `./ui.sh`
3. 浏览器会自动打开 `http://127.0.0.1:8765`：
   - 输入你的 [Clore.ai](https://clore.ai/) API Key。
   - 选择或粘贴 Hugging Face 模型仓库地址。
   - 点击 **「一键租用并部署」**，静待几分钟即可拿到专属 API！

---

## 🇬🇧 English Description

### Overview
A dependency-free local UI & CLI automation engine (pure Python standard library) that automatically rents a high-value GPU on **Clore.ai** and deploys any uncensored AI model from Hugging Face in one click.

### Key Capabilities
- **Zero External Dependencies**: Runs entirely on the Python 3 standard library (`urllib`, `http.server`, `json`, `sqlite3`).
- **Engine Auto-Detection**:
  - GGUF files -> `llama.cpp server` with CUDA.
  - Safetensors / AWQ / GPTQ / FP8 -> `vLLM` high-throughput inference engine.
  - EXL2 / EXL3 -> `TabbyAPI` (ExLlamaV3).
- **VRAM Calculation & Dead Node Pruning**: Dynamically parses the model's `config.json` to calculate required VRAM, discovers the cheapest compliant GPU host, and auto-blacklists stalling nodes.
- **OpenAI-Compatible Gateway**: Exposes standard `/v1/chat/completions` endpoint for instant integration with NextChat, OpenCode, Cursor, and One-API.
- **Instant Teardown**: One click to stop and delete the instance, avoiding idle server costs.

---

## 🛠️ Architecture

```
[ Local Browser UI ] -> (http://127.0.0.1:8765)
          |
  [ Python Engine ] (Zero Dependencies)
          |-- 1. Parse Hugging Face config.json -> VRAM check
          |-- 2. Clore.ai API -> Filter cheapest GPU (RTX 3090/4090)
          |-- 3. Auto-pick Docker image (vLLM / llama.cpp / TabbyAPI)
          |-- 4. Monitor boot & healthcheck
          v
[ Dedicated GPU Server ] ===> OpenAI API (/v1/chat/completions)
```

## 📜 License
MIT License. Created for AI researchers, developers, and privacy enthusiasts worldwide.
