<div align="center">

<h1 align="center"><strong>⚕️ 多智能体医疗助手 :<h6 align="center">基于 AI 的多智能体医疗诊断与辅助系统</h6></strong></h1>


## 📚 目录
- [概述](#overview)
- [演示](#demo)
- [技术流程图](#technical-flowchart)
- [核心功能](#key-features)
- [技术栈](#technology-stack)
- [安装与配置](#installation-setup)
  - [使用 Docker](#docker-setup)
  - [手动安装](#manual-setup)
- [使用方法](#usage)

----

## 📌 概述 

**多智能体医疗助手** 是一个基于 **AI 驱动的聊天机器人**，旨在辅助 **医疗诊断、研究和患者交互**。

🚀 **由多智能体智能驱动**，该系统集成了：
- **🤖 大语言模型 (LLMs)**
- **🖼️ 计算机视觉模型**，用于医学影像分析
- **📚 检索增强生成 (RAG)**，利用向量数据库
- **🌐 实时网络搜索**，获取最新医学信息
- **👨‍⚕️ 人机协同验证**，对 AI 医学影像诊断进行审核

## 🛡️ 技术流程图 

![技术流程图](assets/final_medical_assistant_flowchart_light_rounded.png)

---

## ✨ 核心功能 

- 🤖 **多智能体架构**：专业化智能体协同工作，处理诊断、信息检索、推理等任务

- 🔍 **高级智能体 RAG 检索系统**：

  - 基于 Docling 的解析，从 PDF 中提取文本、表格和图像。
  - 嵌入 Markdown 格式的文本、表格和基于 LLM 的图像摘要。
  - 基于 LLM 的语义分块，感知文档结构边界。
  - 基于 LLM 的查询扩展，包含相关医学领域术语。
  - Qdrant 混合搜索，结合 BM25 稀疏关键词搜索与稠密嵌入向量搜索。
  - 基于 HuggingFace Cross-Encoder 的检索文档块重排序，提升 LLM 响应准确性。
  - 输入输出护栏，确保安全和相关的响应。
  - 响应中附带源文档链接和参考文档块中的图像。
  - 基于置信度的 RAG 与网络搜索之间的智能体间交接，防止幻觉。

- 🏥 **医学影像分析**
  - 脑肿瘤检测（待开发）
  - 胸部 X 光疾病分类
  - 皮肤病变分割

- 🌐 **实时研究集成**：网络搜索智能体检索最新的医学研究论文和发现

- 📊 **基于置信度的验证**：通过对数概率分析确保医学建议的高准确性

- 🎙️ **语音交互功能**：由 Eleven Labs API 驱动的无缝语音转文字和文字转语音

- 👩‍⚕️ **专家监督系统**：医学专业人员在最终输出前进行人机协同验证

- ⚔️ **输入与输出护栏**：确保安全、无偏见和可靠的医学响应，同时过滤有害或误导性内容

- 💻 **直观的用户界面**：为技术基础较少的医疗专业人员设计

> [!NOTE]
> 即将推出的功能：
> 1. 脑肿瘤医学计算机视觉模型集成。
> 2. 欢迎提出建议和贡献。

---

## 🛠️ 技术栈 <a name="technology-stack"></a>

| 组件 | 技术方案 |
|-----------|-------------|
| 🔹 **后端框架** | FastAPI |
| 🔹 **智能体编排** | LangGraph |
| 🔹 **文档解析** | Docling |
| 🔹 **知识存储** | Qdrant 向量数据库 |
| 🔹 **医学影像** | 计算机视觉模型 |
| | • 脑肿瘤：目标检测 (PyTorch) |
| | • 胸部 X 光：图像分类 (PyTorch) |
| | • 皮肤病变：语义分割 (PyTorch) |
| 🔹 **护栏** | LangChain |
| 🔹 **语音处理** | Eleven Labs API |
| 🔹 **前端** | HTML, CSS, JavaScript |
| 🔹 **部署** | Docker, GitHub Actions CI/CD |

---

## 🚀 安装与配置 <a name="installation-setup"></a>

## 📌 方式一：使用 Docker <a name="docker-setup"></a>

### 前置条件：

- 系统已安装 [Docker](https://docs.docker.com/get-docker/)
- 所需服务的 API 密钥

### 1️⃣ 克隆仓库
```bash
git clone https://github.com/souvikmajumder26/Multi-Agent-Medical-Assistant.git
cd Multi-Agent-Medical-Assistant
```

### 2️⃣ 创建环境变量文件
- 在根目录下创建 `.env` 文件，添加以下 API 密钥：

> [!NOTE]
> 你可以选择任意 LLM 和嵌入模型...
> 1. 如果使用 Azure OpenAI，无需修改。
> 2. 如果使用 OpenAI 直连，需修改 'config.py' 中的 LLM 和嵌入模型定义，并提供相应的环境变量。
> 3. 如果使用本地模型，可能需要在整个代码库特别是 'agents' 中进行相应的代码修改。

> [!WARNING]
> 请确保 `.env` 文件中的 API 密钥正确且具有必要的权限。
> 变量名后不要有尾随空格。

```bash
# LLM 配置（开发中使用 Azure Open AI - gpt-4o）
# 如果使用其他 LLM API 密钥或本地 LLM，需要进行相应的代码修改
deployment_name=
model_name=gpt-4o
azure_endpoint=
openai_api_key=
openai_api_version=

# 嵌入模型配置（开发中使用 Azure Open AI - text-embedding-ada-002）
# 如果使用其他嵌入模型，需要进行相应的代码修改
embedding_deployment_name=
embedding_model_name=text-embedding-ada-002
embedding_azure_endpoint=
embedding_openai_api_key=
embedding_openai_api_version=

# 语音 API 密钥（新建 Eleven Labs 账户可获得免费额度）
ELEVEN_LABS_API_KEY=

# 网络搜索 API 密钥（新建 Tavily 账户可获得免费额度）
TAVILY_API_KEY=

# Hugging Face 令牌 - 使用重排序模型 "ms-marco-TinyBERT-L-6"
HUGGINGFACE_TOKEN=

# （可选）如果使用 Qdrant 服务器版本，本地版本不需要 API 密钥
QDRANT_URL=
QDRANT_API_KEY=
```

### 3️⃣ 构建 Docker 镜像
```bash
docker build -t medical-assistant .
```

### 4️⃣ 运行 Docker 容器
```bash
docker run -d --name medical-assistant-app -p 8000:8000 --env-file .env medical-assistant
```
应用将在以下地址可用：[http://localhost:8000](http://localhost:8000)

### 5️⃣ 在 Docker 容器中将数据导入向量数据库

- 导入单个文档：
```bash
docker exec medical-assistant-app python ingest_rag_data.py --file ./data/raw/brain_tumors_ucni.pdf
```

- 从目录中导入多个文档：
```bash
docker exec medical-assistant-app python ingest_rag_data.py --dir ./data/raw
```

### 容器管理：

#### 停止容器
```bash
docker stop medical-assistant-app
```

#### 启动容器
```bash
docker start medical-assistant-app
```

#### 查看日志
```bash
docker logs medical-assistant-app
```

#### 删除容器
```bash
docker rm medical-assistant-app
```

### 故障排除：

#### 容器健康检查
容器包含一个监控应用状态的健康检查。你可以通过以下命令查看健康状态：
```bash
docker inspect --format='{{.State.Health.Status}}' medical-assistant-app
```

#### 容器无法启动
如果容器启动失败，请检查日志中的错误信息：
```bash
docker logs medical-assistant-app
```


## 📌 方式二：不使用 Docker <a name="manual-setup"></a>

### 1️⃣ 克隆仓库
```bash
git clone https://github.com/souvikmajumder26/Multi-Agent-Medical-Assistant.git
cd Multi-Agent-Medical-Assistant
```

### 2️⃣ 创建并激活虚拟环境
- 使用 conda：
```bash
conda create --name <环境名称> python=3.11
conda activate <环境名称>
```
- 使用 python venv：
```bash
python -m venv <环境名称>
source <环境名称>/bin/activate  # Mac/Linux
<环境名称>\Scripts\activate     # Windows
```

### 3️⃣ 安装依赖

> [!IMPORTANT]
> 语音服务需要安装 ffmpeg。

- 使用 conda：
```bash
conda install -c conda-forge ffmpeg
```
```bash
pip install -r requirements.txt
```
- 使用 python venv：
```bash
winget install ffmpeg
```
```bash
pip install -r requirements.txt
```

### 4️⃣ 配置 API 密钥
- 创建 `.env` 文件，按照 `方式一` 中所示添加所需的 API 密钥。

### 5️⃣ 运行应用
- 在已激活的环境中运行以下命令：

```bash
python app.py
```
应用将在以下地址可用：[http://localhost:8000](http://localhost:8000)

### 6️⃣ 向向量数据库导入额外数据
根据需要运行以下命令之一：
- 逐个导入文档：
```bash
python ingest_rag_data.py --file ./data/raw/brain_tumors_ucni.pdf
```
- 从目录中导入多个文档：
```bash
python ingest_rag_data.py --dir ./data/raw
```

---

## 🧠 使用方法 <a name="usage"></a>

> [!NOTE]
> 1. 首次运行可能不太稳定并可能出现错误 — 请耐心等待，检查控制台中正在进行的下载和安装。
> 2. 首次运行时会下载许多模型 — yolo（用于 tesseract OCR）、计算机视觉智能体模型、cross-encoder 重排序模型等。
> 3. 下载完成后重试，一切应该可以正常运行，因为所有功能都经过了全面测试。

- 上传医学影像进行 **AI 辅助诊断**。特定任务的计算机视觉模型驱动的智能体 — 可上传 'sample_images' 文件夹中的图像进行体验。
- 提问医学问题，利用 **检索增强生成 (RAG)**（如记忆中有相关信息）或 **网络搜索** 获取最新信息。
- 使用 **语音交互**（语音转文字和文字转语音）。
- 通过 **人机协同验证** 审核 AI 生成的分析结果。

---

