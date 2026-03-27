# RAG-Based-Knowledge-Retrieval-System

##  项目简介

本项目是一个基于 RAG（Retrieval-Augmented Generation）的知识检索系统，结合大模型与向量数据库，实现对本地文档（PDF/TXT）的语义检索与问答能力。

项目基于 LangChain 构建，支持：

* 文档加载与处理
* 文本切分
* 向量存储（Chroma）
* Embedding 模型管理
* Prompt 管理
* 日志与配置解耦

---

##  项目结构

```bash
project/
│
├── utils/                  # 工具模块
│   ├── config_handler.py
│   ├── file_handler.py
│   ├── logger_handler.py
│   ├── path_tool.py
│   └── prompt_loader.py
│
├── model/
│   └── factory.py          # 模型工厂
│
├── rag/
│   └── vector_store.py     # 向量数据库服务
│
├── config/                 # 配置文件
│   ├── rag.yml
│   ├── chroma.yml
│   ├── prompts.yml
│   └── agent.yml
│
├── logs/                   # 日志目录
└── main.py
```

---

##  核心模块说明

###  1. 模型工厂（model/factory.py）

实现模型解耦管理：

* 聊天模型（LLM）
* 向量嵌入模型（Embedding）

支持：

* ChatTongyi
* DashScopeEmbeddings

特点：

* 工厂模式设计
* 配置驱动模型切换

---

###  2. 向量数据库服务（rag/vector_store.py）

核心模块：实现 RAG 检索能力

功能：

* 文档加载（PDF / TXT）
* 文本切分（RecursiveCharacterTextSplitter）
* 向量化存储（Chroma）
* 语义检索（Retriever）

关键特性：

 **MD5 去重机制**

* 避免重复向量化同一文件

 **递归文件加载**

* 支持多层目录扫描

 **异常日志记录**

* 完整错误堆栈

---

###  3. 文件处理模块（file_handler.py）

功能：

* 文件 MD5 计算
* 多层目录遍历
* PDF / TXT 加载（LangChain Loader）

---

###  4. 配置管理（config_handler.py）

功能：

* 统一加载 YAML 配置
* 支持多配置模块：

  * RAG
  * Chroma
  * Prompt
  * Agent

---

###  5. Prompt 管理（prompt_loader.py）

功能：

* 系统 Prompt 加载
* RAG Prompt 加载
* 报告 Prompt 加载

特点：

* 配置驱动
* 解耦 Prompt 与代码

---

###  6. 日志系统（logger_handler.py）

功能：

* 控制台日志
* 文件日志
* 自动生成日志文件

---

###  7. 路径管理（path_tool.py）

功能：

* 获取项目根路径
* 统一路径拼接

---

##  环境依赖

建议 Python 3.10+

安装依赖：

```bash
pip install -r requirements.txt
```

核心依赖：

```txt
langchain
langchain-community
langchain-text-splitters
langchain-chroma
chromadb
openai
tiktoken
PyYAML
```

---

##  使用方法

###  加载向量库

```python
from rag.vector_store import VectorStoreService

vs = VectorStoreService()
vs.load_document()
```

---

###  获取检索器

```python
retriever = vs.get_retriever()
res = retriever.invoke("你的问题")
```

---

###  示例输出

```text
耳机连接Apple设备...
--------------------
...
```

---
