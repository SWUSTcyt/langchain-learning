# LangChain学习与实践

本项目包含了LangChain框架的学习笔记和实践示例，旨在帮助开发者快速入门和掌握LangChain。

🚀大模型落地开发实战指南！请关注微信公众号：**「AGI启程号」** 深入浅出，助你轻松入门！

📚 数据分析、深度学习、大模型与算法的综合进阶，尽在CSDN[博客主页](https://blog.csdn.net/qq_33489955?type=blog)

## 项目简介

LangChain是一个面向大模型应用开发的框架，它提供了一系列工具和接口，帮助开发者更便捷地构建基于大模型的应用。本项目通过一系列实践示例，展示了LangChain的核心功能和使用方法。

## 环境要求

- Python 3.10+
- 各类API密钥（根据使用的模型提供商而定）

## 安装指南

1. 克隆仓库
```bash
git clone https://github.com/your-username/langchain-learning.git
cd langchain-learning
```

2. 创建并激活虚拟环境
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# Linux/Mac
source venv/bin/activate
```

3. 安装依赖
```bash
pip install -r requirements.txt
```

4. 创建.env文件，添加API密钥
```
OPENAI_API_KEY=your_openai_api_key
DEEPSEEK_API_KEY=your_deepseek_api_key
# 其他API密钥
```

## 目录结构

- `langchain-01-basic.ipynb`: LangChain基础用法，包括模型封装、Prompt模板、结构化输出和Function Calling
- `langchain-02-数据连接与流程编排.ipynb`: 数据连接与流程编排
- `langchain-03-langGraph.ipynb`: LangGraph
- `langchain-04-agent.ipynb`: Agent
- 更多内容持续更新中...

## 核心内容

1. **模型I/O封装**
   - 统一的模型接口
   - 多轮对话管理
   - 支持不同的模型提供商
   - 流式输出支持

2. **Prompt模板**
   - 基础Prompt模板
   - 对话式Prompt模板
   - 历史消息占位符
   - 从文件加载模板

3. **结构化输出**
   - Pydantic模型输出
   - JSON Schema定义
   - 输出解析器
   - 自动错误修复

4. **Function Calling**
   - 工具函数定义与调用
   - 结果处理

## 使用示例

### 基本模型调用

```python
import os
from dotenv import load_dotenv, find_dotenv
from langchain.chat_models import init_chat_model

# 加载环境变量
_ = load_dotenv(find_dotenv())

# 初始化模型
model = init_chat_model("gpt-4o-mini", model_provider="openai")

# 调用模型
response = model.invoke("你是谁")
print(response.content)
```

### 结构化输出

```python
from pydantic import BaseModel, Field
from langchain.prompts import PromptTemplate

# 定义输出结构
class Date(BaseModel):
    year: int = Field(description="Year")
    month: int = Field(description="Month")
    day: int = Field(description="Day")
    era: str = Field(description="BC or AD")

# 使用结构化输出
structured_llm = model.with_structured_output(Date)
template = PromptTemplate.from_template("提取用户输入中的日期。\n用户输入: {query}")
result = structured_llm.invoke(template.format(query="2023年四月6日天气晴..."))
print(result)
```

## 后续计划

- 数据连接封装
- 向量存储与检索
- RAG实现
- Chain与LCEL
- Agent开发
- LangGraph工作流

## 参考资料

- [LangChain官方文档](https://python.langchain.com/docs/get_started/introduction)
- [LangChain GitHub仓库](https://github.com/langchain-ai/langchain) 
