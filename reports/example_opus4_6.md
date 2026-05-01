# 正颌外科 × Embodied AI × Surgical Agent 系统战略研究报告

> 视角：顶尖 PI + AI Scientist + 产业战略研究员
> 覆盖：全球趋势 / 顶尖团队 / 正颌外科核心机会 / 3-10 年科研战略 / 国家级基金方向
> 日期：2026-05
> 说明：本报告所有链接均为可追溯的真实资料（论文 / 项目 / 代码 / 产品），已按 **类型** 与 **落地阶段** 标注，避免"只给名字不给地址"的空洞陈述。

---

## 0. Executive Summary（高密度结论版）

**一句话判断**：
> 2024–2026 是 **Surgical VLA + Surgical Agent** 从"demo 级 paper"迈向"系统级 breakthrough"的窗口期。通用 VLA（OpenVLA, π0, RT-2, GR00T）的范式已验证；真正的壁垒从 **算法** 转移到 **手术数据 × 临床闭环 × 机器人本体 × 监管**。谁掌握"**专科垂直数据 + 真机闭环 + 临床金标准**"，谁就拥有未来 5-10 年的话语权。

**给用户（正颌外科 PI）的五条核心结论**：

1. **正颌外科是 Surgical Embodied AI 最被低估、最适合中国团队"单点超车"的专科**。胸腹腔/神经外科虽然热，但被 Intuitive、Medtronic、JHU 等深度占据；正颌外科有 **结构化术前规划 + 硬组织（骨）操作 + 可数字孪生 + 面型可量化评价** 四重天然优势，是 VLA 训练的"干净环境"。
2. **不要和 Google/NVIDIA 比通用 Surgical Foundation Model**。应该做 **Orthognathic-Specialized VLA（OrthoVLA / CMF-VLA）**——专科数据 + 专科任务 + 专科机器人本体。通用大模型是土壤，专科模型才是果实。
3. **真正的 frontier 不是"autonomous orthognathic surgery"，而是"Surgical Copilot + Semi-Autonomous Osteotomy"**。完全自主短期不可监管落地；"术前自动规划 → 术中 AR/机器人导航 → 术后结果预测"的 **半自主闭环** 在 3 年内就能发 Nature Medicine / Science Robotics 级别成果。
4. **Digital Twin Face + Soft Tissue Simulation World Model** 是目前全球几乎空白、又 **最可能被生成式 AI 颠覆** 的点。现有 FEM/Mass-Spring 方法都已 20 年没有根本突破，这里是博士课题的"金矿"。
5. **国家基金布局三层次**：短期（面上/青年）打 **3D 关键点 + 自动规划 + 软组织预测**；中期（重点/重点研发）打 **正颌 Surgical Agent + AR 导航机器人**；长期（2030 战略科技）打 **中国自主正颌手术具身智能平台**，与口腔临床中心 + 国产机器人本体（天玑、柏惠维康、元化、精锋）形成数据-算法-硬件闭环。

**哪些不要碰 / 伪风口**：
- 纯 "ChatGPT 问诊病历总结" 类应用 — 无壁垒，3 年内被通用模型吞掉。
- "完全自主正颌手术机器人" — 监管、伦理、责任链条 10 年内不可能在中国落地，宣传可以，科研主线不应 all in。
- 仅仅把 LLaVA 换成医学图像微调 — 没有数据壁垒就是 PPT 论文。

---

## 1. 全球技术趋势图谱（2024–2026）

### 1.1 核心范式迁移路径

```
2017–2020 : CNN + Segmentation    （U-Net / nnU-Net 主导医学影像）
2020–2023 : Transformer + CLIP    （多模态预训练进入医疗）
2023–2024 : Surgical LLM / VLM    （SurgicalGPT, LLaVA-Surg, GSViT）
2024–2025 : Surgical VLA / Agent  （SRT-H, Surgical AI Copilot, SurgBox, SurgVLM）
2025–2027 : Surgical World Model  （Sim-to-Real + Digital Twin + RL 闭环）← 现在的 frontier
2027–2030 : Specialized Embodied Surgeon （专科自主/半自主手术 agent）
```

### 1.2 十大关键技术方向 × 爆发度/壁垒/落地度 矩阵

| 方向 | 当前阶段 | 爆发度 | 真壁垒 | 是否适合正颌切入 | 代表工作 |
|---|---|---|---|---|---|
| Surgical Foundation Model | 验证期 | ★★★★☆ | 数据 / 算力 | △ 作为 backbone | SurgVLM, GSViT, EndoFM |
| Medical VLA | 起步期 | ★★★★★ | 数据 + 机器人本体 | ◎ 核心机会 | OpenVLA→Surgical 适配 |
| Surgical Agent / Copilot | 原型期 | ★★★★★ | 临床闭环 | ◎ Copilot 方向最佳 | Surgical AI Copilot, SurgBox |
| 长时程规划 Long-horizon | 起步 | ★★★★ | 任务分解数据 | ◎ 正颌手术天然长程 | SRT-H |
| Agentic / Autonomous Surgery | 早期 | ★★★☆ | 监管 | ×（中期不推荐） | SRT-H gallbladder |
| Human-in-the-loop | 成熟中 | ★★★★ | 人机协同 UX | ◎ | da Vinci + AI assist |
| Digital Twin Surgery | 起步 | ★★★★★ | 软组织建模 | ◎◎ 金矿 | Atlas Meditech + NVIDIA |
| Real-to-Sim / Sim-to-Real | 爆发 | ★★★★★ | 仿真真实感 | ◎ | NVIDIA Isaac for Healthcare |
| RL for Surgery | 早期 | ★★★☆ | 奖励信号 | △ | ORBIT-Surgical |
| Surgical World Model | 概念期 | ★★★★ | 动力学数据 | ◎ 骨操作可量化 | SORA+Surgery 研究 |

### 1.3 "炒作 vs 真 Frontier" 判断

**是炒作（降权）**：
- "GPT-4 能看懂手术视频" — 看懂 ≠ 能指导操作；无动作空间 grounding。
- "自主手术机器人 2027 年临床" — 法规层面在中国、美国均无路径。
- 所有号称 "Surgical AGI" 的 PR 稿 — 现实是连 **单术式稳定 90%** 都极难。

**真 Frontier（值得 all in）**：
- **VLA 与手术机器人 embodied 的对齐（action token ↔ 解剖语义）**。
- **Surgical World Model**：可预测软组织/骨变形的视频生成式模型。
- **专科 Agent 的任务分解 + 验证 + 失败恢复**（不是单步预测，是 **17+ 步的长序列稳健性**，SRT-H 是第一个真正示范）。
- **Real→Sim→Real**：用真实手术视频驱动 Isaac/MuJoCo 数字孪生训练，再回真机。

---

## 2. Embodied AI 与外科手术结合的核心范式

### 2.1 三种技术路线对比

| 路线 | 代表 | 优点 | 缺点 | 正颌适配度 |
|---|---|---|---|---|
| **End-to-End VLA**（像素→动作） | OpenVLA, π0, RT-2 | 数据驱动 / 通用 | 可解释差、监管难 | ★★ |
| **Hierarchical Agent**（Planner + Skill） | SRT-H, Surgical Copilot | 可解释 / 可插入临床规则 | 训练管线复杂 | ★★★★★ |
| **Model-based + World Model** | Dreamer-style, UniSim | 样本效率高 / 可想象 | 动力学建模难 | ★★★★（骨结构可建模） |

**结论**：正颌场景 **Hierarchical Agent + 数字孪生 World Model** 是最优路径；纯 end-to-end VLA 在监管与解释性上过不了伦理委员会。

### 2.2 VLA 基础工作（都有真实链接，供纳入 Related Work）

- **OpenVLA** (Stanford, 2024): https://openvla.github.io/ · https://arxiv.org/abs/2406.09246 · Code: https://github.com/openvla/openvla
- **π0 / π0.5** (Physical Intelligence, 2024-25): https://www.physicalintelligence.company/blog/pi0 · arXiv: https://arxiv.org/abs/2410.24164
- **RT-2** (Google DeepMind, 2023): https://robotics-transformer2.github.io/
- **NVIDIA GR00T N1** (2025): https://developer.nvidia.com/isaac/gr00t
- **Open X-Embodiment** (2023-24): https://robotics-transformer-x.github.io/

### 2.3 Surgical 专科 VLA / VLM

- **SurgVLM** (2025, 大规模 surgical VLM 与系统评测)：https://arxiv.org/abs/2506.02555
- **LLaVA-Surg** (MICCAI-24 相关, 多模态手术助手): https://arxiv.org/abs/2408.07981
- **SurgicalGPT** (MICCAI-23, 手术 VQA): https://arxiv.org/abs/2304.09974
- **SurgPub-Video** (2025, 手术视频数据集+VLM): https://arxiv.org/abs/2508.10054
- **Awesome-Surgical-Video-Understanding**（综述式索引）: https://github.com/isyangshu/Awesome-Surgical-Video-Understanding

### 2.4 Surgical Agent / Copilot

- **Surgical AI Copilot** (arXiv 2503.09474, 2025): https://arxiv.org/abs/2503.09474 — 垂体手术 LLM Agent，做 conversation + planning + task execution。
- **SurgBox**: Agent-Driven OR Sandbox（arXiv 2412.05187）: https://arxiv.org/abs/2412.05187
- **Surgraw**: Multi-agent workflow with CoT for surgical intelligence（arXiv 2503.10265）
- **SRT-H**（Science Robotics 2025, JHU + Stanford, 首个真实胆囊切除自主）：
  - 项目主页: https://h-surgical-robot-transformer.github.io/
  - 论文: https://www.science.org/doi/10.1126/scirobotics.adt5254
  - 新闻: https://hub.jhu.edu/2025/07/09/robot-performs-first-realistic-surgery-without-human-help/

### 2.5 Digital Twin / Sim-to-Real

- **NVIDIA Isaac for Healthcare** + **Surgical Robotics Digital Twin**: https://developer.nvidia.com/blog/advancing-surgical-robotics-with-ai-driven-simulation-and-digital-twin-technology/
- **Atlas Meditech (脑外科数字孪生)**: https://blogs.nvidia.com/blog/atlas-meditech-brain-surgery-ai-digital-twins/
- **ORBIT-Surgical** (NVIDIA, CMU) — Isaac Sim 手术 RL benchmark: https://orbit-surgical.github.io/
- **SurRoL** (CUHK) — da Vinci 仿真 RL 平台: https://github.com/med-air/SurRoL

---

## 3. Surgical Foundation Model / Medical VLA / Surgical Agent 发展现状

### 3.1 代表性 Surgical Foundation Model

| 模型 | 机构 | 模态 | 规模 | 是否开源 | 链接 |
|---|---|---|---|---|---|
| **SurgVLM** | 多校（2025） | Video+Text | 数十亿 token | 部分 | https://arxiv.org/abs/2506.02555 |
| **GSViT / EndoFM** | 多校 | 手术视频 | 中等 | 是 | https://github.com/med-air/EndoFM |
| **Surgical-DINO** | CUHK | 视觉自监督 | — | 是 | https://github.com/BeileiCui/SurgicalDINO |
| **SurgVLP** | Imperial/ICL | 视频-语言对比 | — | 是 | https://github.com/CAMMA-public/SurgVLP |
| **SAMSurg / SAM2-Surg** | 多校 | 分割基础模型 | SAM 基座 | 是 | 多篇 2024 arXiv |

**判断**：通用 Surgical FM 主战场已被 **Imperial (CAMMA) / CUHK / JHU / Heidelberg / NVIDIA** 等占据；中国 **单独做通用 Surgical FM 难以弯道超车**，但做 **专科 FM（正颌/颌面专科 CMF-FM）** 反而是空白领域。

### 3.2 Medical VLA：从感知到动作的门槛

**核心挑战**：
1. **动作空间不统一** — 达芬奇、腔镜、开放正颌手术的 action token 完全不同。
2. **数据稀缺** — 单一术式带标注的真实机器人 trajectory 极少；正颌尤其稀缺。
3. **安全约束** — 骨结构操作不能"像机械臂抓杯子"那样靠 RL 探索。

**破局思路（建议用户采纳）**：
> 将"**正颌手术的截骨 / 磨削 / 植骨路径**"转化为 **可模拟、可量化误差的结构化动作序列**，在 **Isaac Sim / MuJoCo + 患者 CBCT 数字孪生** 中预训练，再蒸馏到真机。这比腹腔软组织 VLA 更容易获得 breakthrough（硬组织有刚体几何约束，世界模型好训）。

### 3.3 Surgical Agent 成熟度地图

```
[Low-level]  感知            —— 已成熟（SAM, SAM2, nnU-Net）
             短程操作         —— 成熟中（SRT-H 三基础技能）
             长程任务         —— SRT-H 2025 首次突破（17 步胆囊）
[High-level] 任务规划 LLM     —— 原型（Surgical Copilot, SurgBox）
             失败恢复/自纠错   —— 研究热点（2025-2026）
             临床闭环验证      —— 几乎空白 ← 中国团队机会
             监管级可解释性    —— 空白 ← 真正壁垒
```

---

## 4. 全球顶尖团队与产业机构分析

### 4.1 海外学术（已交叉验证核心方向）

| 机构 | 核心 PI/Lab | 主攻 | 代表/链接 |
|---|---|---|---|
| **Johns Hopkins (JHU)** | Axel Krieger, Russell Taylor (CIIS), Mathias Unberath | 自主手术机器人, CAI, SRT-H | https://ciis.lcsr.jhu.edu/ · https://h-surgical-robot-transformer.github.io/ |
| **Stanford** | Chelsea Finn, Jeannette Bohg | VLA, robot learning | https://openvla.github.io/ |
| **Imperial College (CAMMA)** | Nicolas Padoy（实际在 Strasbourg）, Ben Glocker | 手术 VLM, 视频理解 | https://camma.unistra.fr/ |
| **CMU** | Howie Choset, Nabil Simaan | 连续体机器人 | https://biorobotics.ri.cmu.edu/ |
| **ETH Zurich** | Bradley Nelson, Philipp Fürnstahl (ROCS/OR-X) | 骨科 AR/机器人 | https://rocs.balgrist.ch/en/ |
| **Oxford** | Andrew Zisserman, Michael Brady | 医学 CV | |
| **Heidelberg / DKFZ** | Lena Maier-Hein | Surgical data science 提出者 | https://www.dkfz.de/en/mic/ |
| **NVIDIA Research Healthcare** | Mona Flores, Holoscan team | Isaac Surgical / 数字孪生 | https://developer.nvidia.com/clara-holoscan |
| **Google DeepMind / Health** | — | Med-Gemini, AMIE | https://deepmind.google/technologies/med-gemini/ |
| **Mayo Clinic / UCSF** | 多 PI | 临床落地 + 真实世界数据 | |
| **MIT CSAIL** | Daniela Rus, Polina Golland | medical robotics, 医学影像 | |

### 4.2 海外产业

| 公司 | 方向 | 与 AI/VLA 结合 | 备注 |
|---|---|---|---|
| **Intuitive Surgical** (da Vinci) | 软组织机器人 | da Vinci 5 + Intuitive Hub 数据闭环 | https://www.intuitive.com/ |
| **Medtronic Hugo** | 通用软组织 | Touch Surgery 数字学习 | https://www.medtronic.com/covidien/en-us/robotic-assisted-surgery/hugo-ras-system.html |
| **CMR Surgical Versius** | 通用 | 数据平台 | https://cmrsurgical.com/ |
| **Vicarious Surgical** | 微创 + VR | 虚拟现实控制 | https://www.vicarioussurgical.com/ |
| **Moon Surgical (Maestro)** | Co-manipulation | AI 辅助 | https://moonsurgical.com/ |
| **Physical Intelligence (π)** | 通用 VLA | π0/π0.5 有望迁移手术 | https://www.physicalintelligence.company/ |
| **Figure AI / 1X / Agility** | 通用人形 | 与 OR 相关性弱，但 VLA 技术栈共享 | |
| **Caresyntax** | OR 数据/分析 | 手术视频平台 | https://caresyntax.com/ |
| **Proprio / Activ Surgical** | 手术视觉 AI | 术中 fluorescence + AI | https://proprio.com/ · https://www.activsurgical.com/ |

### 4.3 中国学术（与正颌/颌面 + AI + 机器人交叉最相关）

| 机构 | 代表方向 | 与用户方向相关度 |
|---|---|---|
| **上海交大九院** (沈国芳、王旭东等) | 正颌、数字化正颌、三维规划 | ★★★★★ 临床黄金标杆 |
| **北大口腔** | 正畸-正颌、AI 诊断 | ★★★★ |
| **四川大学华西口腔** | 颌面外科、AI 影像 | ★★★★ |
| **解放军总医院（301）** | 颅颌面外科、机器人 | ★★★★ |
| **清华 AIR / 电子系** | 医疗 AI、机器人 | ★★★ |
| **浙大 / 之江实验室** | 医学多模态大模型 | ★★★ |
| **中科大 / 中科院自动化所** | 具身智能、机器人 | ★★★ |
| **CUHK (MedAIR, Qi Dou)** | Surgical AI、EndoFM、SurRoL | ★★★★ |
| **HKUST / HKU** | 手术机器人仿真 | ★★★ |

### 4.4 中国产业（机器人本体 + AI）

| 公司 | 方向 | 备注 |
|---|---|---|
| **天智航（天玑）** | 骨科手术机器人（含口腔） | 国内骨科机器人龙头 |
| **柏惠维康 Remebot** | 神外 + 口腔导航机器人 | 已有口腔种植机器人 |
| **雅客智慧** | 口腔种植机器人 | 牙科垂直 |
| **精锋医疗 / 微创图迈** | 腔镜机器人 | 软组织主战场 |
| **元化智能 / 键嘉** | 关节 / 口腔 | 硬组织精准切削 |
| **商汤医疗 / 联影智能** | 医学影像大模型 | CBCT 影像基础 |
| **华为 / 腾讯觅影 / 阿里达摩院** | 医疗多模态 | 提供基座模型 |
| **智元 / 宇树 / 银河通用** | 通用具身 | VLA 技术栈可迁移 |

**战略判断**：正颌机器人在中国 **几乎没有成熟商业产品**（只有口腔种植机器人）。这是 **产业空白 + 临床需求刚需** 的黄金十字路口。

---

## 5. 正颌外科中的 AI 与具身智能机会（报告核心章节）

### 5.1 正颌外科 AI 现状（分模块证据链）

#### (a) 自动 3D Cephalometric Landmark Detection
- Sahlsten et al., PLOS ONE 2024, 多中心 CBCT 3D landmarking: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0305947
- Multi-Scale 3D Cephalometric Landmark Detection, 2024: https://pmc.ncbi.nlm.nih.gov/articles/PMC11592740/
- J Dent Res 2022, 自动 3D cephalometric landmarking: https://journals.sagepub.com/doi/abs/10.1177/00220345221112333
- **评估**：单点精度 1.5–2 mm，已接近临床可用；但 **一致性、跨中心泛化、稀有解剖变异** 仍是痛点。博士课题可做：**Foundation Model + few-shot adaptation** 替代目前 per-center 训练。

#### (b) CBCT 三维骨分割 + 自动术前规划
- Nature Sci Rep 2025, Multi-task RL + XAI 正颌规划平台: https://www.nature.com/articles/s41598-025-09236-z
- J Stomatol Oral Maxillofac Surg 2024: https://www.sciencedirect.com/science/article/abs/pii/S2212440324005078
- 综述 PMC12178734 (2024-25): https://pmc.ncbi.nlm.nih.gov/articles/PMC12178734/
- 颌面外科 AI 综述 PMC12223443 (2025): https://pmc.ncbi.nlm.nih.gov/articles/PMC12223443/

#### (c) 面型/软组织预测
- 目前主流仍为 **FEM (Finite Element) + Mass-Spring**，生物力学驱动，已 20 年。
- 深度学习生成式方法（GAN/Diffusion）已出现，但 **3D、患者特异、可量化到亚毫米** 的方法仍不成熟 → **最大的科研金矿**。
- Ref 综述：Tandfonline 2023, https://www.tandfonline.com/doi/full/10.1080/19424396.2023.2202444

#### (d) 机器人辅助颌面骨切除
- BMC Oral Health 2025 RARONS 系统：机器人 + AR 导航用于下颌截骨 + 腓骨重建：https://bmcoralhealth.biomedcentral.com/articles/10.1186/s12903-025-06566-2
- Frontiers in Surgery 2024, 机器人辅助下颌角截骨学习曲线：https://www.frontiersin.org/journals/surgery/articles/10.3389/fsurg.2024.1453135/full
- PMC8105801, 机器人辅助 MAO（电磁导航）：https://pmc.ncbi.nlm.nih.gov/articles/PMC8105801/

### 5.2 正颌外科与 LLM / MLLM / VLA / Agent 的结合机会（矩阵）

| 临床场景 | 可用范式 | 数据需求 | 可发表会议 | 3年可行性 |
|---|---|---|---|---|
| 自动 3D 关键点 + 手术计划生成 | VLM + Geometric Transformer | 千量级标注 CBCT | MICCAI / IPCAI / Med Image Anal | ★★★★★ |
| 软组织/面型数字孪生预测 | Diffusion + Neural Physics / 3D GS | 成对术前-术后 CBCT+面扫 | CVPR / NeurIPS / Nat BME | ★★★★ |
| 正颌 Surgical Copilot（多模态问答+计划） | LLM Agent + RAG + 影像工具 | 病历+影像+术式库 | AAAI / MICCAI / npj Digital Med | ★★★★★ |
| AR 导航 + 机器人辅助截骨（半自主） | Hierarchical Agent + Sim2Real | 配准+力反馈数据 | ICRA / IROS / Science Rob | ★★★★ |
| 术式推荐 / 并发症预测 | Clinical LLM + 多模态融合 | 大规模病历 | Nat Med / Lancet Digital Health | ★★★ |
| Digital Twin Face + 闭环优化 | World Model + RL | 仿真 + 真实配对 | CVPR / Nat Mach Intell | ★★★★★（长期） |

### 5.3 正颌场景相对其他专科的独特优势（为什么值得 all in）

1. **硬组织主导** → 数字孪生/世界模型更易建模（刚体 + 可量化）。
2. **术前规划高度结构化** → 天然适合 Agent 做 workflow。
3. **术后效果可量化**（面型 3D 扫描、咬合、头影测量）→ **可做闭环 RL/偏好对齐** 的少数外科领域。
4. **临床专家决策链清晰** → 容易做 Human-in-the-loop 的高质量数据标注。
5. **中国临床量巨大**（人口 + 颜面美学需求）→ 数据壁垒可快速建立。

### 5.4 全球几乎没人做、但潜力巨大的方向（突破点清单）

> 以下 5 条是本报告最重要的战略输出，建议 **优先立项**。

1. **OrthoVLA：正颌专科 Vision-Language-Action 模型**
   - 输入：CBCT + 面扫 + 病历 + 术式指令；输出：截骨路径序列 + 固定板位置 + 风险提示。
   - 关键创新：**Action token = 解剖学语义 token**（而非末端位姿），直接与临床决策对齐。
   - 为什么现在没人做：没有人同时拥有正颌高质量数据 + VLA 训练 know-how。中国顶级口腔医院 + AI Lab 联合是极少数能做到的组合。

2. **Digital Twin Face with Neural Biomechanics**
   - 用 3D Gaussian Splatting / NeRF + 物理约束 diffusion 替代 FEM，实现实时、个体化、亚毫米软组织预测。
   - 延伸：在此上做 **术式选择 RL**（奖励=美学+咬合+并发症）。

3. **Surgical Copilot for Orthognathic Pre-op Planning**
   - LLM Agent + 影像工具调用 + 可解释推理，面向 **主刀医生的副驾**。
   - 不挑战 autonomy 的伦理红线，3 年内可临床试用。

4. **Real-to-Sim-to-Real for Mandibular Osteotomy Robot**
   - 从真实手术视频自动重建 Isaac Sim 场景 → RL 训练 → 真机迁移。
   - 瓶颈：骨力反馈仿真；机会：与国产骨科机器人（天玑 / 元化 / 柏惠维康）联合。

5. **Orthognathic Surgical World Model**
   - 预测"如果这样截这里，面型 / 咬合 / 软组织会变成什么样"的 **生成式世界模型**，作为所有上层 Agent 的底座。全球空白。

---

## 6. 数据集、Benchmark 与开源生态

### 6.1 手术通用
- **Cholec80 / CholecT50 / Endoscapes**（CAMMA 系列）：https://camma.unistra.fr/datasets
- **AutoLaparo**（CUHK）：https://autolaparo.github.io/
- **SurgToolLoc / Surgical Visual Domain Adaptation Challenge**（MICCAI Grand Challenges）
- **SurgPub-Video** (2025)：https://arxiv.org/abs/2508.10054
- **Open X-Embodiment**（非手术，但 VLA 基础）：https://robotics-transformer-x.github.io/

### 6.2 颅颌面专用（稀缺，正是壁垒所在）
- **MICCAI ToothFairy / ToothFairy2**（下颌神经管/牙齿分割）：https://toothfairy.grand-challenge.org/
- **CTooth / 3D Teeth Scan Dataset**（多篇公开）
- **公开 3D cephalometric 数据极少** —— **中国团队自建数据集 = 国家级科学基础设施**。建议申请 **国家科技基础资源调查专项 / 重点研发"前沿生物技术"专项**。

### 6.3 仿真平台
- **NVIDIA Isaac Sim / Isaac Lab / Isaac for Healthcare**：https://developer.nvidia.com/isaac/sim
- **ORBIT-Surgical**（CMU+NVIDIA）：https://orbit-surgical.github.io/
- **SurRoL**（CUHK）：https://github.com/med-air/SurRoL
- **dVRK**（JHU, da Vinci 研究套件）：https://research.intusurg.com/dvrk

---

## 7. 未来 1-2 年可发表方向（短期，面向课题/论文）

目标：在 **MICCAI / IPCAI / CVPR / AAAI / ICRA / IROS / Nat Sci Rep / J Dent Res** 上形成课题群。

### 7.1 博士课题 A：**Multi-Center Foundation Model for 3D Cephalometric Landmarking**
- 科学问题：跨中心 CBCT 分布差异下的 landmarking 泛化。
- 方法：self-supervised pretraining on 10k+ unlabeled CBCT → few-shot fine-tune。
- 可发：MICCAI + Med Image Anal。

### 7.2 博士课题 B：**Generative Soft-Tissue Prediction with Diffusion + Biomechanics**
- 科学问题：亚毫米级个体化软组织预测。
- 方法：3D diffusion model + FEM loss + 3D GS 可视化。
- 可发：CVPR / MICCAI / Nat BME。

### 7.3 博士课题 C：**Orthognathic Surgical Copilot (LLM Agent)**
- 科学问题：多模态影像 + 病历 + 术式知识的临床可解释 Agent。
- 方法：LLM + tool-use（分割/配准/规划调用）+ RAG。
- 可发：AAAI / MICCAI / npj Digital Medicine。

### 7.4 博士课题 D：**AR-Guided Robot-Assisted Osteotomy Benchmark & Dataset**
- 科学问题：如何量化评估正颌机器人精度 + 建立公开 benchmark。
- 可发：ICRA / IROS / IPCAI。

### 7.5 博士课题 E：**Digital Twin of the Orthognathic Patient**
- 科学问题：术前-术中-术后三态数字孪生。
- 可发：Nat Mach Intell / Science Translational Medicine。

---

## 8. 未来 3-5 年基金与平台方向（中期）

### 8.1 国家自然科学基金（建议申报方向与口径）

| 基金类型 | 推荐主题（口径已按评审语言调整） |
|---|---|
| 面上/青年 | 面向正颌外科的三维头影测量自监督基础模型研究 |
| 面上 | 基于扩散模型与生物力学约束的个体化面型预测方法研究 |
| 重点项目 | 正颌外科多模态手术智能体（Surgical Agent）关键技术及临床验证 |
| 重点研发计划 "诊疗装备与生物医用材料" | 正颌外科 AR 导航与机器人辅助截骨协同系统研发 |
| 重点研发 "前沿生物技术" | 颅颌面手术数字孪生与世界模型关键技术 |
| 国际（地区）合作 | 与 JHU / ETH Zurich / Imperial 的正颌 Surgical AI 联合研究 |
| 联合基金（企业） | 联合国产骨科/口腔机器人企业（天玑/柏惠维康/元化）共建数据与算法平台 |

### 8.2 医工交叉实验室路线图

```
Year 1 : 数据中心（10 万例 CBCT + 面扫 + 病历结构化）+ 专科 FM 原型
Year 2 : 正颌 Copilot v1 + 手术规划 Agent + 仿真平台（Isaac-CMF）
Year 3 : AR 导航 + 机器人半自主截骨（与产业联合 FDA/NMPA 前期）
Year 4 : 多中心临床试验（自主规划 vs 人工）+ OrthoVLA v1
Year 5 : Specialized Surgical Foundation Model + 数字孪生闭环
```

### 8.3 三大壁垒构建

- **数据壁垒**：10 家顶级口腔医院联合 → 中国 CMF 数据联盟（建议由用户牵头）。
- **临床壁垒**：多中心 RCT + 手术标准化协议（中国口腔医学会背书）。
- **工程壁垒**：与国产机器人本体深度耦合（专用 API + 专用末端执行器）。

---

## 9. 未来 5-10 年长期战略路线（长期）

### 9.1 路线图

```
2026-2027 : OrthoFM（专科基础模型） + Orthognathic Copilot
2027-2028 : OrthoVLA + Sim2Real 机器人半自主截骨
2028-2030 : Surgical World Model for CMF + 数字孪生闭环 RL
2030-2033 : 中国自主"正颌具身智能手术平台"临床 + 产业化
2033-2036 : 向颅颌面、头颈重建、唇腭裂等邻近专科泛化 → CMF Surgical AGI
```

### 9.2 国际竞争格局与中国超车机会

- **美国**：JHU、Stanford 领跑 **通用自主手术机器人**；产业被 Intuitive、Medtronic 锁定。
- **欧洲**：ETH/Balgrist 在骨科机器人领先；Imperial/Strasbourg 在 surgical VLM 领先。
- **中国突破窗口**：
  - **数据** —— 人口优势带来全球最大 CMF 临床数据。
  - **机器人硬件** —— 国产骨科机器人已逼近国际水平。
  - **政策** —— "十四五/十五五"对医工交叉与高端医疗装备强支持。
  - **临床体系** —— 九院/华西/301 等超大规模正颌中心，世界独有。
- **建议战略**：**"专科垂直 + 数据闭环 + 国产本体"** 三位一体，避免与通用机器人/通用 FM 硬碰硬。

### 9.3 最值得 ALL IN 的三个方向（最终结论）

1. **OrthoVLA + Orthognathic Surgical Copilot**（学术 × 产业双峰）
2. **Digital Twin Face / Surgical World Model for CMF**（学术制高点，发顶刊）
3. **国产机器人 + 半自主截骨平台**（产业化 + 国家战略）

---

## 10. 中国团队突破机会（战略提炼）

| 维度 | 中国优势 | 建议策略 |
|---|---|---|
| 数据 | ★★★★★ | 牵头建 CMF 数据联盟，形成国家基础设施 |
| 临床 | ★★★★★ | 九院/华西等多中心 RCT，标准制定者 |
| 机器人本体 | ★★★★ | 与天玑/柏惠维康/元化深度定制 |
| 基础大模型 | ★★★ | 不追通用 FM，做专科 FM + Agent |
| 监管/产业化 | ★★★ | 与 NMPA 创新医疗器械通道提前对接 |
| 人才 | ★★★★ | 医-工-AI 三栖 PhD 培养（用户的核心资源） |

**一句话策略**：**"通用模型开源化 + 专科模型国产化 + 机器人本体自主化 + 临床数据壁垒化"**。

---

## 11. 风险、伦理与监管

- **伦理**：自主手术在中国临床 2030 年前几乎不可能全面放开；必须以 **Copilot / Semi-Autonomous** 为主叙事。
- **监管**：NMPA 创新医疗器械特别审批通道；FDA De Novo / 510(k)。
- **数据合规**：CBCT + 面部图像属于敏感个人信息，必须走 **数据出境安全评估 + 患者知情**。
- **模型风险**：幻觉、分布外失败、罕见解剖。必须构建 **失败检测与人类接管机制**（是 Agent 核心研究问题之一）。
- **IP 壁垒**：尽早布局"正颌专用 action token / 专用奖励函数 / 专用数字孪生架构"等核心专利。

---

## 12. 明确回答五大战略问题

### Q1. 当前真正的 frontier 在哪里？
> **Hierarchical Surgical Agent（SRT-H 类）+ Surgical World Model + 专科 VLA**，且必须是 **长时程 + 真机闭环**，而非单步感知。

### Q2. 哪些只是概念炒作？
> "Surgical AGI"、"完全自主机器人手术 2027 落地"、"GPT-4V 读懂手术视频就能指导操作"、纯病历总结型医疗大模型。

### Q3. 哪些方向真正具备长期壁垒？
> 专科数据闭环 / 真实机器人 trajectory / 数字孪生保真度 / 临床 RCT / 监管注册。**全是"数据 + 系统"壁垒，不是单点算法**。

### Q4. 哪些方向适合中国团队超车？
> 专科 FM（正颌 / 颅颌面 / 口腔）、与国产机器人硬件耦合的半自主平台、大规模 CMF 数据联盟、面型数字孪生。

### Q5. 哪些方向最适合从正颌外科切入？
> **(1) Orthognathic Surgical Copilot** 作为临床入口；**(2) Digital Twin Face** 作为学术制高点；**(3) OrthoVLA + 半自主截骨机器人** 作为产业+战略终局。按此顺序 3 / 5 / 10 年迭代。

---

## 13. 可执行的 90 天启动清单（给用户本人）

1. **本月**：组 3 人小组（1 博士后 AI + 1 博士生 医工 + 1 临床 fellow），定义 OrthoFM v0 的数据 schema。
2. **30-60 天**：与 2–3 家顶级口腔医院谈数据联盟 MOU；与 1 家国产机器人公司谈联合实验室。
3. **60-90 天**：投出 **面上/青年基金** 一份 + **MICCAI 2026** 短文一篇（选课题 A 或 C 最快）。
4. **同步**：联系 JHU Krieger 组 / Imperial CAMMA / CUHK MedAIR，建立海外合作通道（对国自科国际合作与长期人才很关键）。
5. **90 天内**：一份 **《中国正颌 Embodied AI 白皮书》** 作为基金/政策/产业对接的"叙事武器"（本报告可作草稿）。

---

## 附录 A：关键链接一览（去重）

**VLA / 基础**
- OpenVLA: https://openvla.github.io/
- π0: https://www.physicalintelligence.company/blog/pi0
- RT-2: https://robotics-transformer2.github.io/
- GR00T N1: https://developer.nvidia.com/isaac/gr00t
- Open X-Embodiment: https://robotics-transformer-x.github.io/
- VLA 综述 2025: https://arxiv.org/html/2505.04769v1

**Surgical AI / Agent**
- SRT-H: https://h-surgical-robot-transformer.github.io/ · https://www.science.org/doi/10.1126/scirobotics.adt5254
- Surgical AI Copilot: https://arxiv.org/abs/2503.09474
- SurgBox: https://arxiv.org/abs/2412.05187
- SurgVLM: https://arxiv.org/abs/2506.02555
- LLaVA-Surg: https://arxiv.org/abs/2408.07981
- SurgPub-Video: https://arxiv.org/abs/2508.10054
- Awesome-Surgical-Video-Understanding: https://github.com/isyangshu/Awesome-Surgical-Video-Understanding

**Simulation**
- NVIDIA Isaac Surgical: https://developer.nvidia.com/blog/advancing-surgical-robotics-with-ai-driven-simulation-and-digital-twin-technology/
- ORBIT-Surgical: https://orbit-surgical.github.io/
- SurRoL: https://github.com/med-air/SurRoL
- Atlas Meditech: https://blogs.nvidia.com/blog/atlas-meditech-brain-surgery-ai-digital-twins/

**正颌 / 颅颌面**
- 3D Cephalometric Landmarking PLOS ONE 2024: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0305947
- Multi-Scale 3D Ceph 2024: https://pmc.ncbi.nlm.nih.gov/articles/PMC11592740/
- Orthognathic AI 综述 2024-25: https://pmc.ncbi.nlm.nih.gov/articles/PMC12178734/
- OMFS AI 综述 2025: https://pmc.ncbi.nlm.nih.gov/articles/PMC12223443/
- 多任务 RL + XAI 正颌平台 Nat Sci Rep 2025: https://www.nature.com/articles/s41598-025-09236-z
- 机器人 AR 下颌截骨 RARONS 2025: https://bmcoralhealth.biomedcentral.com/articles/10.1186/s12903-025-06566-2
- 机器人辅助 MAO 学习曲线 Front Surg 2024: https://www.frontiersin.org/journals/surgery/articles/10.3389/fsurg.2024.1453135/full

**数据集与挑战赛**
- ToothFairy: https://toothfairy.grand-challenge.org/
- CAMMA datasets: https://camma.unistra.fr/datasets

---

## 附录 B：术语速查

- **VLA** (Vision-Language-Action)：把视觉、语言、动作统一到一个策略模型中。
- **Surgical Agent**：以 LLM 为规划核心、调用各类工具完成手术任务的智能体。
- **Surgical World Model**：可对手术过程与解剖变形做反事实预测的生成式动力学模型。
- **Digital Twin**：与真实患者/OR 高保真同步的数字副本，用于规划、训练、验证。
- **Sim-to-Real / Real-to-Sim**：仿真训练→真机部署 / 真实数据→重建仿真。
- **Hierarchical Policy**：高层语言规划 + 低层技能执行的双层策略。

---

> 本报告为战略研判文档，**不替代系统性文献综述**。建议下一步由团队围绕 §5.4 的 5 个突破方向，分别做 1 份 **15–25 页专题深挖报告**（含代码、实验、资源清单），即可直接转化为基金本子与博士课题。
