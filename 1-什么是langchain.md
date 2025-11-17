## 1.1 什么是LangChain
LangChain 是一个开源的 Python（也支持 JS/TS）框架，用来构建基于大语言模型（LLM, Large Language Model）的应用。

简单来说，LangChain 是在 LLM 之上做的工程化工具，是提供快捷的构建LLM自定义工作流/工具的框架。

## 1.2 LangChain的核心概念
### 1.2.1 LLM Wrapper（大预言模型包装器）
提供调用大模型的统一接口。
例如：
```python
from langchain_openai import ChatOpenAI
llm = ChatOpenAI(model="gpt-4o-mini", api_key="xxx")
llm("写一句关于LangChain的介绍")
```
### 1.2.2 PromptTemplate (提示模板)
模块化指令，便于多次调用。
```python
from langchain_core.prompts import PromptTemplate
prompt = PromptTemplate.from_template("请写一段关于{topic}的介绍。")
```
### 1.2.3 Chains (链式调用)
组合多个步骤，链式执行多步任务。  
例子：先将中文翻译成英文 → 再优化英文内容 → 再将英文重新翻译成中文与原文对比  
例子：先拼接提示词，再回答
```python
prompt = PromptTemplate.from_template("写一句关于{topic}的简短介绍。")
llm = ChatOpenAI(model="gpt-4o-mini", api_key="xxx")
chain = prompt | llm

resp = chain.invoke({"topic": "LangChain"})
print(resp.content)
```
### 1.2.4 Embeddings + Vectorstore
文本向量化，用于 语义搜索  
结合 LLM 做 RAG（Retrieval-Augmented Generation）
### 1.2.5 Agents + Tools (智能体+工具)
让模型自己决定调用哪个工具完成任务
### 1.2.6 Memory (记忆机制)
让对话模型记住历史信息
短期：BufferMemory
长期：结合向量数据库存储知识
## 1.3 LangChain 的应用场景
- 企业知识库问答：把文档或 PDF 转成向量，用模型回答问题
- 智能助理：规划任务、搜索信息、生成报告
- RAG（检索增强生成）：检索资料 + 生成内容
- 多工具代理：调用 API、做计算、发邮件、自动化任务
- 对话机器人：带记忆和多轮上下文管理