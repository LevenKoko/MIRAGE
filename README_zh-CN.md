# MIRAGE CanaryDocs

MIRAGE CanaryDocs 是一个英文合成企业文档数据集，用于结构化隐私单元、Canary 与有序多分块评测。
本数据集是 EMNLP 2026 论文 *When Metadata Remembers: Ordered Provenance Enables
Document-Level Embedding Inversion* 的配套数据集。

## 数据规模

- 版本：`1.0.0`
- 文档：`20,700`（Shadow 20,000 / Dev 100 / Test 600）
- Gold units：`286,240`
- Canary units：`33,379`
- Occurrences：`319,887`
- Chunks：`113,332`

三个划分均有意公开输入和完整 Gold 标注。Test 是公开标注的参考划分，不是隐藏测试集，
也不依赖私有评测服务。

## 数据获取

完整数据集托管在 Hugging Face：

**[LevenKoko/MIRAGE-CanaryDocs](https://huggingface.co/datasets/LevenKoko/MIRAGE-CanaryDocs)**

本 GitHub 仓库只包含文档、schema 和发布元数据，不重复存储 JSONL、Parquet 或 SQLite 数据文件。

使用 Git LFS 克隆完整数据集：

```bash
git lfs install
git clone https://huggingface.co/datasets/LevenKoko/MIRAGE-CanaryDocs
```

也可以通过 Python 下载完整快照：

```python
from huggingface_hub import snapshot_download

snapshot_download(
    repo_id="LevenKoko/MIRAGE-CanaryDocs",
    repo_type="dataset",
    local_dir="MIRAGE-CanaryDocs",
)
```

## 数据集目录说明

以下路径位于 Hugging Face 数据集仓库中：

- `data/`：规范化 JSONL，是数据实体的标准来源。
- `views/bundled/`：每行一篇完整文档，适合直接阅读和加载。
- `views/canaries/`：只聚合 Canary 及其 occurrence/chunk 映射。
- `views/benchmark/`：Dev/Test 的嵌套 Parquet 视图。
- `database/canarydocs.sqlite`：只包含公开数据表与外键的关系数据库。
- `metadata/`：schema、taxonomy、统计、切块定义、文件清单和哈希。

实体关系为：`document -> section -> paragraph`、`document -> chunk`、
`document -> unit -> occurrence <-> chunk`。跨位置重复通过 `dependencies` 表达。

## 配套论文

**When Metadata Remembers: Ordered Provenance Enables Document-Level Embedding Inversion**  
Liwen Zheng, Qing Li, Qingsong Zou, Yong Jiang，EMNLP 2026。

联系人：Liwen Zheng（`zhenglw25@mails.tsinghua.edu.cn`）。引用信息见 `CITATION.cff`。

数据采用 CC BY 4.0 许可。
