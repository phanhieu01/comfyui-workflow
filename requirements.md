# Custom-node và ComfyUI requirements

Commit được pin để workflow có thể tái lập. Các mục **modified/owned** là code đã chỉnh hoặc repo do `phanhieu01` sở hữu; các mục **original** chỉ dùng đúng upstream commit.

| Phân loại | Chức năng | Repository | Commit | Thư mục cài đặt |
|---|---|---|---|---|
| modified/fork | MiniMax H3 PDD Acc, PDD scheduler, SigmaShift | https://github.com/phanhieu01/ComfyUI-MiniMax-H3-PDD-Acc | `8e23e9501a39e6290e1112bf051a5ed63889b58d` | `custom_nodes/ComfyUI-MiniMax-H3-PDD-Acc` |
| owned | Reference Manager (counts/files/paired audio) | https://github.com/phanhieu01/ComfyUI-MiniMax-H3-Reference-Manager | `138b0d88b8f36d94f346b82527848f5e5e1c1539` | `custom_nodes/ComfyUI-MiniMax-H3-Reference-Manager` |
| owned | Phase scale + resolution controls | https://github.com/phanhieu01/ComfyUI-PhaseScale | `8b61cd6c7d2db0d5252db34a3665be5507779615` | `custom_nodes/ComfyUI-PhaseScale` |
| original | rgthree switches | https://github.com/rgthree/rgthree-comfy | `2c5342a8cb0eaecaabf61435a5f37dd594c510ba` | `custom_nodes/rgthree-comfy` |
| original | KJ constants/switches | https://github.com/kijai/ComfyUI-KJNodes | `e27a505b3ba6ce42687fe00500deda103d9d6071` | `custom_nodes/comfyui-kjnodes` |
| original | MiniMax H3 Image Studio resolution node | https://github.com/astropuzzo/ComfyUI-MiniMax-H3-Image-Studio | `47dea30d0bf07e7340ef0cc97e8174a15edf55b9` | `custom_nodes/ComfyUI-MiniMax-H3-Image-Studio` |
| original | VHS image/video/audio loaders | https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite | `4ee72c065db22c9d96c2427954dc69e7b908444b` | `custom_nodes/comfyui-videohelpersuite` |
| original | MiniMax H3 3D latent upscaler node | https://github.com/LBH-123-AI/Comfyui_Minimax_h3_latent_Upscaler | `40316cf008b2fd8663263270669eb4da23f89d2c` | `custom_nodes/Comfyui_Minimax_h3_latent_Upscaler` |
| original | Workflow Encrypt/subgraph support | https://github.com/jtydhr88/ComfyUI-Workflow-Encrypt | `5ec45fdac73d8bd6d732af76bbe81c94413b3e36` | `custom_nodes/ComfyUI-Workflow-Encrypt` |
| core | ComfyUI built-in nodes | https://github.com/comfyanonymous/ComfyUI | `b2da2b4247921dbd5410163f0f6bd0b741d1e377` (`v0.35.0-42-gb2da2b42`) | ComfyUI root |

## Cài bằng Git

```powershell
cd D:\ComfyUI\custom_nodes
git clone https://github.com/phanhieu01/ComfyUI-MiniMax-H3-PDD-Acc.git ComfyUI-MiniMax-H3-PDD-Acc
git -C ComfyUI-MiniMax-H3-PDD-Acc checkout 8e23e9501a39e6290e1112bf051a5ed63889b58d
```

Lặp lại `git clone`/`git checkout <commit>` cho các dòng còn lại. Nếu đã cài node, `git -C <folder> status --short` phải sạch trước khi checkout; không trộn file từ bản khác.

## Python extras

Các node trên tự khai báo dependencies trong repo. Với cài đặt tối thiểu thường cần `opencv-python`, `imageio-ffmpeg`, `cryptography`, `Pillow`, `color-matcher`, `matplotlib` và `mss` theo requirements của VHS/KJNodes/Workflow-Encrypt. ComfyUI Manager có thể cài tự động; không pin lại toàn bộ môi trường Python vào repo workflow.

