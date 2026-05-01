# 正颌外科 × Embodied AI × Surgical Agent 系统战略研究报告

**版本**：2026-05-01  
**报告定位**：面向正颌外科 PI、AI Scientist、医工交叉平台与产业战略团队  
**资料来源**：公开论文、PubMed/PMC、Nature/Science、arXiv、项目主页、GitHub、公司官网，以及本仓库 `reports/report_2_26_enhanced.md` 的既有资料整理。  
**重要说明**：本报告侧重科研战略判断与方向设计，所列链接应在正式基金申报或论文写作前再次核验版本、DOI、伦理与监管状态。

---

## 0. Executive Summary

正颌外科是外科具身智能最适合切入的专科之一。原因不是“机器人替代医生”这个宏大叙事，而是正颌手术具备一组罕见的工程友好特征：

- **强术前规划**：CBCT、头影测量、牙列扫描、咬合设计高度结构化。
- **强几何约束**：截骨线、骨段移动、咬合关系、神经管保护均可被三维建模。
- **强数据闭环**：术前影像、术中导航、术后CT/面像、长期咬合随访可以构成完整监督信号。
- **强临床价值**：减少反复试错、提升规划一致性、缩短年轻医生学习曲线。
- **强中国优势**：高病例量、数字化正颌基础、口腔颌面外科医生工程合作意愿强。

本报告的核心判断：

1. **短期最值得做**：正颌专属多模态数据集、CBCT/牙列/面像配准、术前规划生成、软组织预测、口内视频/术野 3DGS 重建。
2. **中期最值得做**：正颌 Surgical Copilot、术中导航与截骨路径实时反馈、医生-in-the-loop 的数字孪生规划平台。
3. **长期最值得做**：面向正颌的 Medical VLA / Surgical Agent，即能理解病例、生成规划、调用仿真、辅助导航、驱动机器人执行受限动作的系统。
4. **不要过早 All in**：完全自主正颌手术、端到端机器人自动截骨、纯 LLM 术式推荐、没有真实手术数据支撑的“医疗大模型平台”。
5. **真正壁垒**：不是模型本身，而是正颌全流程多模态数据、专家规划标签、术中-术后验证闭环、伦理合规与医生可解释交互。

---

## 1. 全球技术趋势图谱

```text
外科具身智能
├── 感知层
│   ├── 手术视频理解：phase / step / action / instrument / anatomy
│   ├── 3D/4D重建：NeRF / 3DGS / dynamic scene reconstruction
│   ├── 多模态病例理解：文本 + 影像 + 视频 + 机器人轨迹
│   └── 实时导航：AR / VR / 术中定位 / 数字孪生
├── 认知层
│   ├── Surgical Foundation Model
│   ├── Surgical World Model
│   ├── Medical VLM / MLLM
│   ├── Surgical Copilot
│   └── 长时程任务规划
├── 行动层
│   ├── dVRK / 腹腔镜机器人学习
│   ├── RL / imitation learning / diffusion policy
│   ├── VLA：vision-language-action
│   └── robot manipulation / constrained autonomy
└── 临床闭环
    ├── human-in-the-loop
    ├── safety guardrails
    ├── regulatory validation
    └── outcome-based evaluation
```

### 1.1 技术成熟度判断

| 方向 | 成熟度 | 爆发程度 | 正颌相关性 | 战略判断 |
|---|---:|---:|---:|---|
| 手术视频理解 | 高 | 高 | 中 | 已有 Cholec80、EndoVis、SAR-RARP50 等基础，正颌缺少专属数据集 |
| 3DGS 手术重建 | 中高 | 很高 | 很高 | 适合做口内视频、截骨面、软组织动态重建 Demo |
| Surgical Foundation Model | 中 | 很高 | 中高 | 外科视频基础模型正在形成，但正颌数据缺口巨大 |
| Medical VLA | 早期 | 很高 | 高 | 医疗 VLA 仍处概念验证，正颌可从“规划-导航-受限操作”切入 |
| Surgical Agent | 早期 | 高 | 高 | 最适合先做 Copilot，不宜直接宣称完全自主 |
| 自主手术机器人 | 中低 | 高 | 中 | 腹腔镜和软组织操作领先，正颌硬组织机器人仍需约束式自动化 |
| 数字孪生正颌 | 中 | 高 | 极高 | 最有基金与临床转化价值 |
| 纯 LLM 医疗问答 | 中 | 中 | 中 | 可作为辅助层，不构成长期壁垒 |

---

## 2. Embodied AI 与外科手术结合的核心范式

### 2.1 从“看懂手术”到“能参与手术”

外科 AI 正在从三类任务升级：

1. **Perception-only**：识别器械、解剖结构、手术阶段。
2. **Decision-support**：预测风险、提示下一步、辅助规划。
3. **Embodied action**：在医生监督下执行牵拉、夹持、缝合、切割、定位等动作。

正颌外科对应的理想路线不是一开始让机器人自主截骨，而是：

```text
病例理解 → 三维规划 → 仿真验证 → 导航提示 → 受限机器人辅助 → 术后评估 → 数据回流
```

### 2.2 Surgical Agent 的临床形态

面向正颌外科，Surgical Agent 不应定义为“聊天机器人”，而应定义为一个可调用工具的临床工作流智能体：

- **输入**：病历、CBCT、头影测量、口扫、面像、术中视频、医生偏好。
- **工具**：分割模型、配准模型、规划器、有限元/软组织预测、3DGS重建、导航系统。
- **输出**：规划建议、风险解释、截骨路径、骨段移动方案、术中提醒、术后评估报告。
- **安全机制**：医生确认、规则约束、禁区保护、可追溯日志。

---

## 3. Surgical Foundation Model / Medical VLA / Surgical Agent 发展现状

### 3.1 代表进展

| 类别 | 代表工作 / 项目 | 核心价值 | 链接 |
|---|---|---|---|
| Surgical Embodied Intelligence | Surgical embodied intelligence for generalized task autonomy | 多任务自主手术具身智能框架，结合 SurRoL 与真实机器人验证 | [Science Robotics](https://www.science.org/doi/10.1126/scirobotics.adt3093) · [PubMed](https://pubmed.ncbi.nlm.nih.gov/40668896/) |
| 手术 RL 平台 | SurRoL | dVRK 兼容、RL 中心的开源手术机器人学习平台 | [项目页](https://med-air.github.io/SurRoL/) · [GitHub](https://github.com/med-air/SurRoL) |
| 层级自主手术 | SRT-H: hierarchical framework for autonomous surgery | 面向长时程自主操作的层级框架 | [Science Robotics](https://www.science.org/doi/10.1126/scirobotics.adt5254) |
| Surgical Transformer | Surgical Robot Transformer | 将模仿学习与手术机器人轨迹结合 | [arXiv](https://arxiv.org/html/2407.12998v1) |
| 医疗 VLA | RoboNurse-VLA | 面向手术室器械护士场景的 VLA 系统 | [arXiv](https://arxiv.org/abs/2409.19590) |
| VLA 综述 | Vision-Language-Action Models for Robotics | 机器人 VLA 架构、数据、训练范式综述 | [项目页](https://vla-survey.github.io/) |

### 3.2 正颌外科启示

- **腹腔镜自主操作领先**，因为 dVRK 数据与仿真平台成熟；正颌应建设自己的“正颌仿真 + 轨迹 + 规划”平台。
- **Medical VLA 还未成熟到直接临床执行**，但可以先做“语义指令 → 规划工具调用 → 导航提示”的中间层。
- **长期壁垒在世界模型**：模型必须理解骨、牙、咬合、神经、软组织和器械约束，而不是只理解自然图像。

---

## 4. 全球顶尖团队与产业机构分析

### 4.1 海外机构

| 团队 / 机构 | 核心方向 | 与大模型 / VLA / Agent 关系 | 与正颌关系 | 判断 |
|---|---|---|---|---|
| Johns Hopkins | 医疗机器人、Surgical Data Science、SMART Tissue Autonomous Robot 传统强队 | 强，长期布局自主手术与机器人学习 | 间接 | 方法论强，可对标机器人自主操作 |
| Stanford | 医疗 AI、机器人、foundation model、临床转化 | 强 | 间接 | 适合对标 Medical AI + 临床平台 |
| MIT | 机器人学习、具身智能、AI for medicine | 强 | 间接 | VLA/机器人基础模型方法来源 |
| CMU | 机器人、操作学习、仿真到现实 | 强 | 间接 | 可借鉴操作学习与世界模型 |
| NVIDIA Research | Isaac Sim、数字孪生、机器人仿真、医疗影像平台 | 强 | 间接 | 正颌数字孪生可借鉴 Omniverse/Isaac 思路 |
| Google DeepMind | Gemini Robotics、RT 系列、Alpha 系列 | 极强 | 间接 | 通用 VLA 与世界模型方向标杆 |
| Google Health | 医疗基础模型、多模态医学 AI | 强 | 间接 | 可借鉴医学多模态评测体系 |
| OpenAI | GPT-4/5 系列、多模态 Agent | 极强 | 间接 | 适合做 Copilot 层，不适合直接执行医疗动作 |
| Physical Intelligence | 通用机器人基础模型 | 极强 | 间接 | VLA/动作模型重要趋势 |
| Figure AI | 人形机器人与通用操作 | 强 | 弱 | 技术方向相关，临床落地距离远 |
| Intuitive Surgical | da Vinci 平台、手术数据、机器人系统 | 中高 | 间接 | 全球最大手术机器人数据与平台壁垒 |
| Medtronic | Hugo RAS、导航、医疗器械生态 | 中 | 间接 | 产业渠道强 |
| CMR Surgical | Versius 手术机器人 | 中 | 间接 | 机器人平台生态 |
| Vicarious Surgical | 微创机器人系统 | 中 | 弱 | 系统创新参考 |
| Mayo Clinic / UCSF | 临床验证、数字手术、AI 医疗 | 中高 | 间接 | 临床转化路径可对标 |
| Oxford / Imperial College / ETH Zurich | 机器人、医学影像、导航、SDS | 强 | 间接 | 欧洲医工交叉强势 |

### 4.2 中国机构与机会

| 团队 / 机构 | 可能优势 | 与正颌结合机会 |
|---|---|---|
| 清华 / 北大 | AI、机器人、医学工程、基础模型 | 共建正颌 Medical VLA、数字孪生平台 |
| 上海交通大学 | 医工交叉、口腔医学、机器人 | 正颌规划、导航、机器人截骨 |
| 浙江大学 | 医学影像、机器人、AI | CBCT 分割、导航、临床数据平台 |
| 华中科技大学 | 医疗机器人、机械工程、临床医院资源 | 机器人辅助截骨与导航系统 |
| 中科院 | 机器人、自动化、AI基础模型 | 手术世界模型、具身智能算法 |
| 腾讯 AI Lab / 阿里 / 华为 | 多模态大模型、云平台、医疗 AI | 病例理解、知识库、Surgical Copilot |
| 商汤 | 医疗影像、视觉算法 | CBCT/面像/视频多模态视觉模型 |
| 智元 / 宇树 | 机器人硬件与具身智能 | 通用技术参考，临床应用需再设计 |
| 国内医疗机器人企业 | 硬件、注册、临床渠道 | 与正颌导航/截骨专机结合 |

**中国超车点**：不是复制 da Vinci 腹腔镜路线，而是在正颌、口腔颌面、牙颌数字化这类中国病例量大、数字化基础强、国际大厂尚未重点布局的垂直专科中建立数据闭环。

---

## 5. 正颌外科中的 AI 与具身智能机会

### 5.1 AI 在正颌中的现状

| 方向 | 当前进展 | 代表资料 | 瓶颈 | 机会 |
|---|---|---|---|---|
| 头影测量标志点检测 | 已有较多深度学习工作与公开 benchmark | [AI cephalometric review](https://pmc.ncbi.nlm.nih.gov/articles/PMC10287619/) | 2D 为主，泛化不足 | 建立中国多中心正颌 ceph benchmark |
| 术后面型/头影预测 | 生成模型开始进入正颌 | [GPOSC-Net Nature Communications](https://www.nature.com/articles/s41467-025-57669-x) · [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC11911408/) | 多为 2D ceph，缺少 3D软组织真实验证 | 3D face + CBCT + 术后随访生成模型 |
| 正颌 AI 综述 | 已覆盖诊断、规划、预测、评估 | [PMC Review](https://pmc.ncbi.nlm.nih.gov/articles/PMC12178734/) | 研究分散、缺少全流程系统 | 全流程正颌数字孪生 |
| 软组织预测 | 从有限元向数据驱动发展 | [AI facial change prediction review](https://pmc.ncbi.nlm.nih.gov/articles/PMC11231886/) | 标准化数据难、个体差异大 | 条件扩散 / 3D morphable / biomechanical hybrid |
| CBCT 分割 | 牙、颌骨、神经管分割快速进展 | [DentalSegmentator](https://www.medrxiv.org/content/10.1101/2024.03.18.24304458v1.full) | 正颌相关结构标签不足 | 正颌专属 42+ 类结构标注 |
| 术中 3D 重建 | 手术内镜 3DGS 爆发 | [Deform3DGS](https://github.com/jinlab-imvr/Deform3DGS) · [EndoGaussian](https://yifliu3.github.io/EndoGaussian/) | 正颌口内数据缺少 | 口内视频→动态截骨面重建 |

### 5.2 正颌专属突破点

#### 方向 A：正颌多模态数字孪生数据集

**数据结构**：

```text
术前：病历 + ceph + CBCT + 口扫 + 面像 + 医生规划
术中：导航日志 + 口内视频 + 截骨线 + 器械轨迹
术后：CBCT + 面像 + 咬合结果 + 并发症 + 满意度
```

**科学问题**：骨段移动如何映射到软组织、咬合、气道与长期稳定性？  
**基金价值**：高；可作为国家自然科学基金面上/重点项目的数据底座。  
**壁垒**：伦理、多中心标准化、专家规划标签、长期随访。

#### 方向 B：正颌 Surgical Copilot

**功能**：

- 自动读取病例并生成术前摘要。
- 调用分割/配准/规划模型生成候选方案。
- 解释风险：神经损伤、气道变化、咬合不稳定、软组织不协调。
- 生成术前讨论报告和患者沟通材料。

**不建议**：直接输出“最终术式推荐”而无医生确认。  
**建议定位**：医生-in-the-loop 的规划助手。

#### 方向 C：正颌 Medical VLA

**短期形式**：不是直接控制机械臂，而是：

```text
视觉输入（CBCT/术野视频） + 语言指令（医生意图） → 工具调用/导航动作/安全提示
```

**中期形式**：对接机器人系统，执行低风险受限动作：定位、保持、牵拉、钻孔引导、截骨线投影。  
**长期形式**：在严格安全边界内完成半自主截骨或骨段定位。

---

## 6. 数据集、Benchmark 与开源生态

### 6.1 手术视频与工作流数据

| 数据 / Benchmark | 任务 | 链接 | 对正颌启示 |
|---|---|---|---|
| Cholec80 | 手术阶段、器械识别 | [CAMMA datasets](https://camma.unistra.fr/datasets/) | 正颌需建立类似阶段识别数据集 |
| HeiChole | 手术 workflow benchmark | [Medical Image Analysis](https://www.sciencedirect.com/science/article/pii/S1361841523000312) | 可借鉴多算法评测框架 |
| EndoVis | 内镜视觉挑战 | [EndoVis](https://endovissub2017-roboticinstrumentsegmentation.grand-challenge.org/) | 器械分割/跟踪可迁移 |
| SAR-RARP50 | 机器人前列腺手术器械分割与动作识别 | [GitHub evaluation](https://github.com/surgical-vision/SAR_RARP50-evaluation) | 可借鉴 action segmentation 标注体系 |

### 6.2 口腔 / 颌面 / CBCT 数据

| 数据 / Challenge | 任务 | 链接 | 正颌价值 |
|---|---|---|---|
| ISBI Cephalometric Landmark Challenge | 2D ceph landmark | 相关综述：[PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC10287619/) | 建立标志点检测基线 |
| ToothFairy / ToothFairy2 | CBCT 多结构分割 | 搜索结果：[ToothFairy2](https://www.sciencedirect.com/science/article/pii/S1361841526001647) | 对牙、颌骨、修复体结构分割有价值 |
| STS MICCAI Challenge | 2D/3D teeth segmentation | [arXiv](https://arxiv.org/html/2407.13246v1) | 牙列分割与咬合建模基础 |
| DentalSegmentator | 牙颌面 CBCT 分割模型 | [medRxiv](https://www.medrxiv.org/content/10.1101/2024.03.18.24304458v1.full) | 可作为正颌 CBCT 自动建模起点 |

### 6.3 3DGS / 4D 重建生态

| 项目 | 类型 | 链接 | 适用性 |
|---|---|---|---|
| Deform3DGS | 手术可变形场景 3DGS | [GitHub](https://github.com/jinlab-imvr/Deform3DGS) · [MICCAI](https://papers.miccai.org/miccai-2024/206-Paper3887.html) | 正颌口内视频首选 Demo |
| EndoGaussian | 动态内镜 3DGS | [GitHub](https://github.com/CUHK-AIM-Group/EndoGaussian) · [项目页](https://yifliu3.github.io/EndoGaussian/) | 适合动态软组织和器械遮挡 |
| EndoGS | 变形内镜组织重建 | [GitHub](https://github.com/HKU-MedAI/EndoGS) · [arXiv](https://arxiv.org/abs/2401.11535) | 可迁移到口内组织重建 |
| MetalSplatter | Vision Pro 3DGS 渲染 | [GitHub](https://github.com/scier/MetalSplatter) | 教学展示与空间计算 |
| Spatial Fields | 3DGS 查看器 | [官网](https://spatialfields.app/) | 快速 Vision Pro Demo |

---

## 7. 未来 1-2 年可发表方向

### 7.1 MICCAI / IPCAI 方向

1. **正颌多模态术前规划生成模型**
   - 输入：CBCT、ceph、口扫、面像。
   - 输出：骨段移动参数、截骨线、风险解释。
   - 创新点：融合几何约束与专家偏好学习。
   - 投稿点：MICCAI / IPCAI。

2. **正颌口内视频 3DGS 动态重建 Benchmark**
   - 输入：术中口内视频。
   - 输出：截骨面/软组织/器械的 3D/4D 重建。
   - 创新点：面向正颌场景的反光、血液、遮挡、软组织牵拉处理。
   - 投稿点：MICCAI / IPCAI / TMI。

3. **CBCT + 面像 + 口扫的正颌数字孪生配准**
   - 创新点：跨模态刚性/非刚性配准，带解剖约束。
   - 投稿点：MICCAI / MedIA。

### 7.2 CVPR / AAAI 方向

1. **面向正颌的 3D facial outcome generation**
   - 条件扩散模型：术前面像 + 骨段移动 → 术后 3D face。
   - 强调个体化软组织响应。

2. **正颌病例多模态 VLM Benchmark**
   - 问答任务：诊断、规划解释、风险识别。
   - 评测：医生一致性、事实性、安全性、可解释性。

### 7.3 ICRA / IROS 方向

1. **机器人辅助截骨路径规划与安全约束控制**
   - 目标：不是全自动截骨，而是医生确认下的路径保持、禁区保护、力反馈。

2. **正颌仿真环境：Orthognathic-Sim**
   - 包含 Le Fort I、BSSO、颏成形、骨段移动、咬合约束。
   - 可支持 RL / imitation learning / VLA 训练。

---

## 8. 未来 3-5 年基金与平台方向

### 8.1 国家自然科学基金方向

#### 方向 1：面向正颌外科的多模态数字孪生与可解释术前规划

**关键科学问题**：如何建立骨-牙-软组织-咬合耦合的可解释预测模型？  
**技术路线**：

```text
多模态数据采集 → 解剖结构分割 → 跨模态配准 → 规划生成 → 软组织预测 → 术后验证
```

**创新点**：从单点任务升级为正颌全流程建模。

#### 方向 2：医生-in-the-loop 的正颌 Surgical Copilot

**关键科学问题**：如何让 AI 在高风险手术规划中既能生成建议，又能被医生审计与约束？  
**技术路线**：知识库 + 工具调用 Agent + 多模态模型 + 安全规则引擎。

#### 方向 3：正颌术中动态感知与导航智能体

**关键科学问题**：如何从口内视频、导航日志和器械轨迹中实时理解手术状态？  
**技术路线**：3DGS/SLAM + 器械识别 + 截骨线定位 + AR提示。

### 8.2 重点研发计划方向

建议凝练为：

> **面向口腔颌面复杂畸形矫治的全流程智能数字外科与机器人辅助系统**

子课题可包括：

- **多模态正颌数据底座与标准体系**
- **正颌数字孪生与术前规划基础模型**
- **术中导航、AR 显示与实时风险感知**
- **机器人辅助截骨与骨段定位系统**
- **多中心临床验证与注册路径研究**

---

## 9. 未来 5-10 年长期战略路线

### 9.1 分阶段路线图

| 阶段 | 时间 | 目标 | 标志性成果 |
|---|---:|---|---|
| Phase 1 | 0-2 年 | 建数据、做 Demo、发论文 | 正颌多模态数据集、3DGS Demo、软组织预测模型 |
| Phase 2 | 2-5 年 | 建平台、做 Copilot、临床验证 | Surgical Copilot、数字孪生规划系统、多中心研究 |
| Phase 3 | 5-7 年 | 对接导航与机器人 | AR 导航、路径保护、受限机器人辅助 |
| Phase 4 | 7-10 年 | 正颌 Surgical World Model | 半自主规划与受限执行平台 |

### 9.2 长期目标定义

**Autonomous Orthognathic Surgery Platform** 不应定义为“一键自动手术”，而应定义为：

- 自动理解病例。
- 自动提出可解释规划候选。
- 自动进行仿真和风险评估。
- 在术中实时感知偏差。
- 在医生监督下辅助执行受限动作。
- 术后自动评估结果并回流训练。

---

## 10. 中国团队突破机会

### 10.1 为什么中国可以超车

- **病例量优势**：正颌病例、复杂颌面畸形、正畸-正颌联合病例丰富。
- **数字化基础**：CBCT、口扫、3D打印导板、虚拟手术规划已广泛使用。
- **工程成本优势**：可快速建立医院-高校-企业联合 Demo。
- **国际空白**：全球 Surgical AI 主要集中腹腔镜、内镜、眼科；正颌专属 Surgical Agent 基本空白。

### 10.2 适合中国团队 All in 的方向

| 优先级 | 方向 | 原因 |
|---:|---|---|
| 1 | 正颌多模态数据集与 Benchmark | 数据壁垒最高，最适合长期积累 |
| 2 | 正颌数字孪生术前规划系统 | 临床痛点明确，基金价值高 |
| 3 | 正颌 Surgical Copilot | 可快速落地，结合大模型但不依赖大模型炒作 |
| 4 | 口内视频 3DGS 与 AR 教学/导航 | Demo 强、传播强、工程可行 |
| 5 | 机器人辅助截骨路径保护 | 有产业化潜力，但需长期安全验证 |

---

## 11. 博士课题设计

### 课题 1：面向正颌外科的多模态数字孪生建模与术后结果预测

- **数据**：CBCT、口扫、面像、术前规划、术后影像。
- **方法**：多模态配准、3D生成模型、解剖约束网络。
- **产出**：MICCAI/TMI 论文 + 数据集 + 临床验证。

### 课题 2：正颌术前规划生成模型与医生偏好对齐

- **核心问题**：不同专家对同一病例的规划差异如何建模？
- **方法**：专家轨迹学习、偏好学习、可解释规划生成。
- **产出**：AAAI/MICCAI + 规划辅助系统。

### 课题 3：基于口内视频的正颌术中 3D/4D 场景重建

- **核心问题**：如何在血液、反光、遮挡、牵拉下稳定重建？
- **方法**：Deformable 3DGS、语义约束、术中标志点融合。
- **产出**：MICCAI/IPCAI + Vision Pro 教学 Demo。

### 课题 4：正颌 Surgical Copilot 与临床安全评测体系

- **核心问题**：如何评估大模型在正颌规划中的可靠性？
- **方法**：病例问答 Benchmark、工具调用 Agent、医生审查闭环。
- **产出**：NPJ Digital Medicine / JAMIA / AAAI。

### 课题 5：机器人辅助正颌截骨路径规划与安全控制

- **核心问题**：如何在保护神经、血管、牙根和上颌窦的约束下执行精准截骨？
- **方法**：路径优化、力反馈、禁区约束、AR导航。
- **产出**：ICRA/IROS + 临床前实验。

---

## 12. 产业化路径与临床转化壁垒

### 12.1 产业化机会

| 产品形态 | 时间 | 商业价值 | 风险 |
|---|---:|---|---|
| AI术前报告生成 | 0-1 年 | 快速落地，辅助医生效率 | 医疗合规、事实性 |
| 3DGS + Vision Pro 教学系统 | 0-2 年 | 教学培训、会议展示 | 非治疗用途相对低风险 |
| 正颌数字孪生规划平台 | 2-5 年 | 高临床价值 | 数据、注册、医生采纳 |
| AR 导航截骨辅助 | 3-6 年 | 直接提高手术精度 | 术中稳定性、安全认证 |
| 机器人辅助截骨系统 | 5-10 年 | 高壁垒高价值 | 注册周期长、责任界定复杂 |

### 12.2 三类核心壁垒

#### 数据壁垒

- 多中心病例标准化难。
- 术前/术中/术后配对数据难。
- 专家规划标签昂贵。
- 长期随访缺失。

#### 临床壁垒

- 医生需要可解释，而不是黑箱推荐。
- 术式差异、个体美学偏好难量化。
- 伦理审批与患者隐私要求高。

#### 工程壁垒

- 术中视频质量不稳定。
- 口内空间狭小、血液反光、遮挡严重。
- 实时导航要求低延迟与高可靠。
- 机器人系统必须有安全冗余。

---

## 13. 最值得 All in 的方向

### 13.1 第一优先级：正颌多模态数据与 Benchmark

这是长期壁垒的根。没有数据，任何大模型、VLA、Agent 都只是概念包装。

### 13.2 第二优先级：正颌数字孪生与术前规划生成

这是最贴近临床核心价值的方向，能连接基金、论文、平台和产业。

### 13.3 第三优先级：Surgical Copilot + 工具调用 Agent

不要做泛泛医疗问答，而要做能调用正颌工具链的 Agent。

### 13.4 第四优先级：口内视频 3DGS + Vision Pro 教学/导航

最适合快速形成可见 Demo、吸引医院和基金评审注意。

### 13.5 第五优先级：机器人辅助截骨与骨段定位

长期价值极高，但不适合作为第一年唯一主线。

---

## 14. 哪些是 frontier，哪些是概念炒作

### 14.1 真正 frontier

- **手术视频基础模型 + 动作理解 + 机器人轨迹学习**。
- **Surgical World Model**：能预测组织/骨结构在操作后的变化。
- **Medical VLA**：视觉、语言、动作统一建模。
- **正颌数字孪生**：骨、牙、软组织、咬合、气道的多物理/数据融合。
- **医生-in-the-loop 自主系统**：可解释、可审计、可中止。

### 14.2 概念炒作

- **纯 LLM 直接推荐手术方案**：缺少几何、影像、临床验证。
- **完全自主正颌手术短期落地**：监管、安全、责任均不成熟。
- **没有数据闭环的医疗大模型平台**：缺少专科壁垒。
- **只做漂亮 3D 可视化但不连接规划/结果评估**：科研价值有限。

### 14.3 长期壁垒

- 正颌专属多模态数据。
- 专家规划偏好与术后结果配对。
- 术中导航与机器人执行日志。
- 多中心临床验证。
- 可解释、安全、可注册的软件医疗器械体系。

---

## 15. 关键参考文献与链接

### 15.1 Embodied AI / Surgical Robotics

| 资源 | 链接 |
|---|---|
| Surgical embodied intelligence for generalized task autonomy | [Science Robotics](https://www.science.org/doi/10.1126/scirobotics.adt3093) · [PubMed](https://pubmed.ncbi.nlm.nih.gov/40668896/) |
| SRT-H hierarchical framework for autonomous surgery | [Science Robotics](https://www.science.org/doi/10.1126/scirobotics.adt5254) |
| SurRoL | [项目页](https://med-air.github.io/SurRoL/) · [GitHub](https://github.com/med-air/SurRoL) |
| Surgical Robot Transformer | [arXiv](https://arxiv.org/html/2407.12998v1) |
| RoboNurse-VLA | [arXiv](https://arxiv.org/abs/2409.19590) |
| VLA Models for Robotics Survey | [项目页](https://vla-survey.github.io/) |

### 15.2 正颌 AI / 口腔颌面 AI

| 资源 | 链接 |
|---|---|
| Application of AI in Orthognathic Surgery review | [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12178734/) |
| GPOSC-Net postoperative cephalogram generation | [Nature Communications](https://www.nature.com/articles/s41467-025-57669-x) · [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC11911408/) |
| AI facial change prediction review | [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC11231886/) |
| Cephalometric landmark detection review | [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC10287619/) |
| Robot-assisted maxillary positioning | [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC8231103/) · [MDPI](https://www.mdpi.com/2077-0383/10/12/2596) |
| Robotic surgical systems in maxillofacial surgery review | [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC5518975/) |

### 15.3 3DGS / Vision Pro / 数据集

| 资源 | 链接 |
|---|---|
| Deform3DGS | [GitHub](https://github.com/jinlab-imvr/Deform3DGS) · [MICCAI](https://papers.miccai.org/miccai-2024/206-Paper3887.html) |
| EndoGaussian | [GitHub](https://github.com/CUHK-AIM-Group/EndoGaussian) · [项目页](https://yifliu3.github.io/EndoGaussian/) |
| EndoGS | [GitHub](https://github.com/HKU-MedAI/EndoGS) · [arXiv](https://arxiv.org/abs/2401.11535) |
| MetalSplatter | [GitHub](https://github.com/scier/MetalSplatter) |
| Spatial Fields | [官网](https://spatialfields.app/) |
| Cholec80 / CAMMA datasets | [CAMMA](https://camma.unistra.fr/datasets/) |
| SAR-RARP50 evaluation | [GitHub](https://github.com/surgical-vision/SAR_RARP50-evaluation) |
| STS MICCAI teeth segmentation challenge | [arXiv](https://arxiv.org/html/2407.13246v1) |
| DentalSegmentator | [medRxiv](https://www.medrxiv.org/content/10.1101/2024.03.18.24304458v1.full) |

---

## 16. 最终建议

如果团队只有一个主攻方向，建议选择：

> **正颌外科多模态数字孪生与 Surgical Copilot：从术前规划、软组织预测、术中感知到机器人辅助的全流程智能平台。**

原因：

- **临床价值最大**：直接改善规划质量和手术一致性。
- **科研延展性最强**：可拆成 MICCAI、CVPR、ICRA、AAAI 多条论文线。
- **基金表达最稳**：符合医工交叉、AI for Science、智能机器人、数字医疗方向。
- **产业路径清晰**：先教学/规划软件，再导航系统，最后机器人辅助。
- **中国超车概率最高**：国际大厂尚未占据正颌专科数据与场景。
