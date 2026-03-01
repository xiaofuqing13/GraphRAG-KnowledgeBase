# GraphRAG-KnowledgeBase — 基于 GraphRAG 的知识库检索系统

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)](https://python.org/)
[![GraphRAG](https://img.shields.io/badge/GraphRAG-Microsoft-0078D4?logo=microsoft)](https://github.com/microsoft/graphrag)
[![LanceDB](https://img.shields.io/badge/LanceDB-向量检索-FF6B35)](https://lancedb.com/)
[![License](https://img.shields.io/badge/License-MIT-blue)](LICENSE)

## 项目背景

传统的文档检索方式（如关键词搜索）在面对大量非结构化文档时，很难理解文档间的关联关系和上下文语义。用户提出一个复杂问题，往往需要翻阅多份文档才能拼凑出答案，效率很低。

本项目基于微软的 [GraphRAG](https://github.com/microsoft/graphrag) 框架，构建了一个知识图谱驱动的 RAG（检索增强生成）系统。系统先对文档进行实体抽取和关系建模，生成知识图谱，再结合大语言模型进行问答。相比普通 RAG，知识图谱能捕获文档间的深层关联，回答更准确、更完整。

## 效果展示

### 搜索界面
![搜索界面](docs/search-ui.png)

支持 Local Search（局部上下文检索）和 Global Search（全局摘要检索）两种模式。

### 检索结果对比
![检索结果对比](docs/search-results.png)

Local Search 返回基于具体文档片段的精确答案，Global Search 返回基于全局社区摘要的综合分析。

### 知识图谱浏览器
![知识图谱浏览器](docs/graph-explorer.png)

Graph Explorer 可视化展示文档中抽取的实体和社区关系，支持按层级筛选和查看详细报告。

## 核心功能

| 功能 | 说明 |
|------|------|
| 知识图谱构建 | 自动从文档中抽取实体和关系，构建索引 |
| 双模式检索 | Global（全局摘要）和 Local（局部上下文）检索 |
| 流式输出 | 结合大语言模型的流式回答，实时返回结果 |
| LanceDB 存储 | 向量数据库存储嵌入，高效相似度检索 |
| Web 搜索前端 | 基于 Docker 部署的统一搜索应用 |

## 项目结构

```
GraphRAG-KnowledgeBase/
├── graphrag/                   # GraphRAG 核心框架
├── ragtest/                    # 知识库实例配置
│   ├── input/                  # 输入文档
│   ├── output/                 # 索引输出（知识图谱）
│   ├── prompts/                # 自定义提示词
│   └── settings.yaml           # 配置文件
├── unified-search-app/         # 搜索前端
├── docs/                       # 文档
├── examples_notebooks/         # 使用示例
└── pyproject.toml              # 依赖配置
```

## 快速开始

```bash
# 安装依赖
pip install poetry
poetry install

# 构建知识图谱索引
python -m graphrag index --root ./ragtest

# 全局检索
python -m graphrag query --root ./ragtest --method global --query "你的问题" --streaming

# 局部检索
python -m graphrag query --root ./ragtest --method local --query "你的问题"
```

## 配置说明

编辑 `ragtest/settings.yaml`：
- LLM 模型接口地址和 API Key
- 嵌入模型配置
- 文档分块策略
- 索引存储路径

> 本项目基于 [Microsoft GraphRAG](https://github.com/microsoft/graphrag) 框架二次开发。

## 开源协议

MIT License
