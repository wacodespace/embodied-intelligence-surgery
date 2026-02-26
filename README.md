# Embodied Intelligence in Surgery

具身智能在外科手术领域的前沿研究进展与工程落地追踪。

## 关注方向

- **具身智能 × 手术机器人**：自主手术、RL策略、人机协同
- **3D Gaussian Splatting × 手术重建**：内窥镜/口内视频→3D点云
- **Apple Vision Pro × 医疗教育**：沉浸式手术教学、AR导航
- **正颌外科专属**：截骨导航、软组织追踪、数字化规划

## 目录结构

```
reports/          # 行业调研报告（按日期更新）
references/       # 关键论文笔记与链接整理
resources/        # 配图、演示素材说明
pipeline/         # 技术路线与Demo脚本
```

## 核心报告

- [2026.2.26 增强版报告](reports/report_2_26_enhanced.md) — 具身智能与3D点云重建技术在正颌外科的应用

## 快速链接

### 具身智能

| 项目 | 链接 |
|------|------|
| Surgical Embodied Intelligence (Science Robotics 2025) | [论文](https://www.science.org/doi/10.1126/scirobotics.adt3093) |
| Cornerstone Sentire 系统 | [官方](https://en.csrbtx.com/press-release/45) |
| SurRoL 手术RL平台 | [GitHub](https://github.com/med-air/SurRoL) |

### 3D重建 (3DGS)

| 项目 | 链接 |
|------|------|
| Deform3DGS (MICCAI 2024, 首选) | [GitHub](https://github.com/jinlab-imvr/Deform3DGS) |
| EndoGaussian (TMI 2025) | [GitHub](https://github.com/CUHK-AIM-Group/EndoGaussian) |
| EndoGS (MICCAI 2024) | [GitHub](https://github.com/HKU-MedAI/EndoGS) |
| DentalSplat (正颌专属) | [arXiv](https://arxiv.org/abs/2511.03099) |
| Apple SHARP (单图秒级) | [GitHub](https://github.com/apple/ml-sharp) |

### Vision Pro 医疗

| 项目 | 链接 |
|------|------|
| MetalSplatter (3DGS → Vision Pro) | [GitHub](https://github.com/scier/MetalSplatter) |
| Spatial Fields App | [官网](https://spatialfields.app/) |
| Fundamental Surgery | [App Store](https://apps.apple.com/us/app/fundamental-surgery/id6612024672?platform=vision) |
| VSI HoloMedicine (FDA批准) | [官网](https://apoqlar.com/) |

## 更新日志

- **2026.2.26** — 初始版本：具身智能+3DGS+Vision Pro完整调研

## License

MIT
