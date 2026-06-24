# BCI Dataset Discovery Skill

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Codex Skill](https://img.shields.io/badge/Codex-Skill-green.svg)](https://github.com/openai/codex)

AI Agent 专用的 BCI/EEG 数据集发现与筛选工作流，让 Agent 像研究员一样系统性地发现和评估神经科学数据集。

## 🎯 为什么需要这个 Skill？

神经科学数据集分散在几十个平台上（OpenNeuro、PhysioNet、Zenodo……），手动搜索耗时且容易遗漏。

这个 Skill 提供了**分阶段、溯源优先**的数据集发现工作流：

- ✅ 自动扫描多个数据集门户（Portal Sweep）
- ✅ 按任务相关性评分（0-5 分）
- ✅ 审计访问权限（公开/注册/申请/受限）
- ✅ 生成候选表格供人工筛选（避免瞎找）
- ✅ 用户确认后才提取详细维度（节省 Token）
- ✅ 追踪证据来源（每个字段都有标签）

## 🚀 快速开始

### 1. 安装到 Codex

```bash
# 克隆仓库
git clone https://github.com/17373851063-ai/dataset-discovery.git ~/.codex/skills/dataset-discovery

# 或手动复制
cp -r dataset-discovery ~/.codex/skills/
```

### 2. 使用示例

在 Codex 中，直接对 Agent 说：

```
帮我找 BCI 运动想象数据集，要求：
- 范式：运动想象（MI）或运动执行（ME）
- 效果器：手部、手指、抓握
-  access：公开可下载
```

Agent 会自动：
1. 扫描 OpenNeuro、NEMAR、PhysioNet 等门户
2. 按相关性评分（0-5）
3. 审计每个数据集的访问权限
4. 生成候选表格供你确认
5. 确认后提取详细维度

## 📋 核心功能

### 1. 范围接收（Scope Intake）

从用户描述中提取：
- **主题词**：motor imagery, motor execution, grasping, robotic hand…
- **种子门户**：OpenNeuro, Figshare, NEMAR, PhysioNet…
- **种子数据集**：WBCIC-SHU, EEGMMIDB…
- **包含/排除约束**：模态、公开性、格式、大小…

### 2. 门户扫描（Portal Sweep）

自动扫描 13+ 个神经科学数据门户：

| 门户 | 用途 | 访问模式 |
|------|------|----------|
| OpenNeuro | BIDS EEG/MEG/iEEG 数据集 | 通常公开，DataLad 下载 |
| NEMAR | EEG/MEG BIDS 镜像，计算就绪 | 通常公开，CLI/git-annex |
| EEGDash | EEG 数据集元数据索引 | 索引/镜像，跳转源链接 |
| PhysioNet | 生理信号数据集 | 开放访问或凭证访问 |
| Zenodo | 开放研究档案 | 公开下载，API 可用 |
| Figshare | 科学数据，DOI 记录 | 通常直接公开下载 |

### 3. 候选筛选（Candidate Screening）

对每个候选数据集评分（0-5）：

| 分数 | 含义 | 示例 |
|------|------|------|
| 5 | 精确匹配 | EEG MI/ME + 真实机械手/手指/灵巧控制 |
| 4 | 高度相关 | 上肢或抓握 MI/ME，机械手控制的好代理 |
| 3 | 有用基线 | 通用左右手 MI/ME，可用于预训练 |
| 2 | 相邻领域 | 其他 BCI/神经反馈/多模态运动任务 |
| 1 | 弱相关 | EEG 但不涉及运动控制 |
| 0 | 不相关 | 超出范围 |

### 4. 访问审计（Access Audit）

分类每个数据集的访问状态：

| 状态 | 含义 | 示例 |
|------|------|------|
| `public_direct` | 直接浏览器/API/wget 下载 | OpenNeuro 公开数据集 |
| `public_cli` | 公开但需通过 CLI 下载 | DataLad, git-annex, S3 |
| `public_registration` | 公开但需注册/登录 | Figshare 某些记录 |
| `application_required` | 需申请/数据使用协议 | CRCNS 部分数据集 |
| `restricted` | 封闭/私有/不可用 | 未公开的数据集 |

### 5. 分阶段输出

**第一阶段：候选表格**（供人工筛选）

| rank | dataset_name | portal | relevance | access_status | keep? |
|------|--------------|--------|-----------|----------------|-------|
| 1 | WBCIC-SHU | OpenNeuro | 5 | public_direct | yes |
| 2 | EEGMMIDB | PhysioNet | 3 | public_direct | maybe |

**第二阶段：详细维度**（用户确认后）

| field | value | evidence |
|-------|-------|----------|
| participants | N=10, healthy | [Data] |
| modality | EEG, 64 channels | [Data] |
| paradigm | MI (left/right hand) | [Paper] |
| sampling_rate | 250 Hz | [Data] |
| access | public, Creative Commons | [Data] |

### 6. 证据标签系统

追踪每个字段的来源：
- `[Data]` — 来自数据集官方页面
- `[Paper]` — 来自论文
- `[Repo]` — 来自代码仓库
- `[Index]` — 来自索引/目录
- `[Inference]` — 推理得出
- `[Assumption]` — 基于假设
- `[Unknown]` — 证据不足

## 📊 输出示例

### 候选筛选表格（第一阶段）

```markdown
## BCI 数据集候选表格（请审核）

| rank | dataset_name | portal | task_match | relevance | access | keep? |
|------|--------------|--------|------------|-----------|--------|-------|
| 1 | WBCIC-SHU | OpenNeuro | MI + robotic hand | 5 | public_direct | ? |
| 2 | EEG Motor Movement | PhysioNet | MI (L/R hand) | 3 | public_direct | ? |
| 3 | Ding Robotic Hand | KiltHub | ME + robotic hand | 5 | public_registration | ? |
| 4 | High-Gamma | GIN | MI/ME (grasp) | 4 | public_cli | ? |

**请标记 keep / delete / maybe，确认后我将提取详细维度。**
```

### 详细维度表格（第二阶段）

```markdown
## 数据集详细维度：WBCIC-SHU

| field | value | evidence |
|-------|-------|----------|
| dataset_name | WBCIC-SHU | [Data] |
| canonical_url | https://openneuro.org/datasets/ds00XXXX | [Data] |
| participants | N=20, healthy, 22±3 yo | [Paper] |
| modality | EEG, 64 channels, Ag/AgCl | [Data] |
| paradigm | MI (left hand, right hand, foot) | [Paper] |
| sampling_rate | 1000 Hz | [Data] |
| access | public, PDDL license | [Data] |
| download_method | DataLad | [Data] |
| robot_control | no (offline BCI) | [Paper] |
| caveats | no robotic hand data | [Assumption] |
```

## 🛠️ 项目结构

```
dataset-discovery/
├── SKILL.md                          # Skill 定义（Codex 入口）
├── README.md                         # 本文件
├── LICENSE                           # MIT 开源协议
├── agents/
│   └── openai.yaml                  # OpenAI API 配置示例
├── references/
│   ├── portal-catalog.md            # 数据门户目录（13+ 门户）
│   └── table-schemas.md            # 输出表格结构定义
└── examples/
    └── README.md                   # 使用示例
```

## 🔧 配置

### Agent 配置（agents/*.yaml）

示例 `openai.yaml`：

```yaml
interface:
  display_name: "BCI Dataset Discovery"
  short_description: "Find and screen BCI/EEG datasets"
  default_prompt: "Use $bci-dataset-discovery to find public EEG motor imagery datasets."
```

## 📚 参考资料

- [OpenNeuro](https://openneuro.org) — BIDS 神经影像数据集
- [NEMAR](https://www.nemar.org) — EEG/MEG 计算就绪数据集
- [EEGDash](https://eegdash.org) — EEG 数据集元数据索引
- [PhysioNet](https://physionet.org) — 生理信号数据集
- [MOABB](https://moabb.neurotechlab.com) — BCI 基准框架

## 🤝 贡献

欢迎贡献！请查看：
- Issues：报告 Bug 或提出新功能
- Pull Requests：提交代码改进
- Discussions：讨论数据集发现经验

## 📄 许可证

[MIT License](LICENSE) — 自由使用、修改和分发。

## ✨ 作者

最初为 Codex Skill 创建，用于系统性地发现和筛选 BCI/EEG 数据集。

---

**⭐ 如果这个 Skill 对你有帮助，请给个 Star！**
