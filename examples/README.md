# Dataset Discovery Skill - 使用示例

本目录包含使用 Dataset Discovery Skill 的完整示例。

## 示例 1：寻找运动想象（MI）EEG 数据集

**场景：** 为机械手控制 BCI 寻找合适的运动想象 EEG 数据集

### 用户输入

```
帮我找 BCI 数据集，要求：
- 范式：运动想象（Motor Imagery, MI）
- 效果器：手部、手指
- 应用：机械手控制
- 访问：公开可下载
- 格式：EEG，BIDS 格式优先
```

### Agent 执行流程

#### Step 1: 范围接收

```
📋 已提取搜索范围：

主题词：motor imagery, motor execution, hand, finger, grasping, robotic hand control
种子门户：OpenNeuro, NEMAR, PhysioNet, Zenodo
包含约束：EEG, 公开下载, 健康受试者
排除约束：非 EEG, 侵入式, 不可下载
```

#### Step 2: 门户扫描（Portal Sweep）

```
🔍 正在扫描 13 个数据门户...

✅ OpenNeuro: 找到 8 个候选
✅ NEMAR: 找到 5 个候选
✅ PhysioNet: 找到 3 个候选
✅ EEGDash: 找到 6 个候选
⚠️  CRCNS: 部分需要申请
```

#### Step 3: 候选筛选（Candidate Screening）

```
📊 候选数据集表格（请审核）：

| rank | dataset_name | portal | task_match | relevance | access | keep? |
|------|--------------|--------|------------|-----------|--------|-------|
| 1 | WBBCIC-SHU | OpenNeuro | MI + hand/foot | 5 | public_direct | ? |
| 2 | EEGMMIDB | PhysioNet | MI (L/R hand) | 3 | public_direct | ? |
| 3 | Cho2017 (OpenBMI) | GigaDB | MI + ME | 4 | public_direct | ? |
| 4 | High-Gamma Dataset | GIN | MI/ME (grasp) | 4 | public_cli | ? |
| 5 | Dumont2019 | OSF | MI + robotic hand | 5 | public_direct | ? |

**请标记 keep / delete / maybe，确认后我将提取详细维度。**
```

#### Step 4: 用户确认后提取详细维度

```
✅ 你标记了 3 个数据集为 keep：WBCIC-SHU, Cho2017, Dumont2019

正在提取详细维度...

## 数据集详细维度

| field | WBBCIC-SHU | Cho2017 | Dumont2019 |
|-------|--------------|---------|------------|
| participants | N=20, healthy | N=52, healthy | N=10, healthy |
| modality | EEG, 64ch | EEG, 64ch | EEG, 32ch |
| paradigm | MI (L/R hand, foot) | MI + ME | MI + online feedback |
| sampling_rate | 1000 Hz | 1000 Hz | 500 Hz |
| robot_control | no | no | yes (robot arm) |
| access | public, PDDL | public, MIT | public, CC-BY |
| download_method | DataLad | wget | OSF API |

**审核完成？如需修改请告知，否则我将标记为 final。**
```

---

## 示例 2：寻找需要申请的受限数据集

**场景：** 寻找高质量但可能需要申请的数据集

### 用户输入

```
找 EEG 运动执行（ME）数据集，用于上肢康复 BCI，
不限访问类型（包括需要申请的也可以）。
```

### Agent 执行流程

```
🔍 正在扫描门户...

## 候选表格（含受限数据集）

| rank | dataset_name | portal | access_status | relevance |
|------|--------------|--------|----------------|-----------|
| 1 | OFf2023-RehabBCI | CRCNS | application_required | 5 |
| 2 | KIU-BCI-MI | PhysioNet | public_registration | 4 |
| 3 | Stroke-EEG-MI | OpenNeuro | public_direct | 4 |

⚠️  注意：
- OFf2023-RehabBCI 需要填写申请表 + 数据使用协议
- KIU-BCI-MI 需要注册 PhysioNet 账号

**是否保留需要申请的数据集？**
```

---

## 示例 3：使用种子数据集进行相似搜索

**场景：** 已知某个数据集很好，找类似的

### 用户输入

```
我已经知道 EEGMMIDB 这个数据集很好，
帮我找类似的（相似范式、相似任务）EEG 数据集。
```

### Agent 执行流程

```
🔍 以 EEGMMIDB 为种子进行相似搜索...

种子特征：
- 范式：MI（左右手）
- 受试者：健康，N=109
- 通道：64 EEG
- 采样率：160 Hz
- 访问：公开

找到相似数据集：

| dataset_name | similarity | reason |
|--------------|------------|--------|
| WBBCIC-SHU | 0.85 | 同样 MI L/R hand，更高采样率 |
| BCIC-IV-2a | 0.78 | 同样 MI 4-class，更多受试者 |
| Cho2017 | 0.72 | MI + ME，更多受试者 |

**是否添加到候选列表？**
```

---

## 📊 输出文件说明

发现完成后，输出目录结构：

```
outputs/
├── portal_sweep_results.json    # 门户扫描结果
├── candidate_screening_table.md  # 候选筛选表格
├── approved_datasets.json       # 用户确认的数据集
├── detailed_dimensions_table.md  # 详细维度表格
└── download_manifest.json       # 下载清单（含 MD5）
```

---

## 🤝 贡献你的示例

如果你用这个 Skill 成功发现了数据集，欢迎提交 PR 分享你的示例！

格式：
```
examples/
├── your_search_topic/
│   ├── README.md              # 搜索需求描述
│   ├── candidate_table.md      # 候选表格
│   └── detailed_table.md      # 详细维度表格
```
