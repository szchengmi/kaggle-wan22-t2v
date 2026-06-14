# Kaggle Wan2.2-TI2V-5B — 15秒文生视频

Kaggle Notebook 代码，用 Wan2.2-TI2V-5B (GGUF Q4_K_M) 在 T4 GPU 上生成约15秒文生视频。

## 流程

```
第一段: T2V 生成 85 帧 (~10.6秒)
     ↓ 取末帧
第二段: TI2V 续 50 帧 (~6.25秒)
     ↓ ffmpeg concat
最终: ~135帧 ≈ 16.9秒 @ 8fps
```

## Kaggle 使用

1. 新建 Kaggle Notebook → Accelerator = GPU T4 × 1
2. 上传 `kaggle_wan22_t2v.ipynb` 或逐 cell 粘贴 `cells/` 目录中的代码
3. 按顺序运行 6 个 cell

## 文件说明

| 文件 | 说明 |
|---|---|
| `kaggle_wan22_t2v.ipynb` | 完整 Notebook (Jupyter 格式) |
| `cells/` | 逐 cell 纯代码版本 (推荐，避免 JSON null 问题) |
| `cells/cell1_setup.py` | 安装 ComfyUI + 依赖 |
| `cells/cell2_download.py` | 下载模型文件 |
| `cells/cell3_generate.py` | 生成脚本 |
| `cells/cell4_launch.py` | 启动 ComfyUI |
| `cells/cell5_run.py` | 执行生成 |
| `cells/cell6_preview.py` | 预览视频 |

## 硬件要求

- GPU: T4 16GB (Kaggle 免费配额)
- 预计耗时: ~16分钟/条
- 每周 30h GPU 配额 → 约 100 条视频

## 关键参数

- 分辨率: 846×480
- 帧率: 8 fps
- 采样器: dpmpp_2m / karras
- 步数: 20 + 20
- CFG: 5.0
- Shift: 8
