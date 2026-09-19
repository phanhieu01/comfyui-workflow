# MiniMax H3 model manifest

Không có model binary trong GitHub. Tải đúng tên file, đặt vào đúng thư mục ComfyUI và kiểm tra SHA-256 sau khi tải. Hash bên dưới là hash của các file đang được workflow sử dụng tại thời điểm đóng gói.

| Vai trò | Tên file | Thư mục ComfyUI | Link tải | SHA-256 |
|---|---|---|---|---|
| Ref2VA checkpoint | `MiniMax-H3-Ref2VA-pruned_rank8_int8_convrot.safetensors` | `models/diffusion_models/` (có thể map từ `Wan2GP/ckpts/`) | https://huggingface.co/DeepBeepMeep/MiniMax-H3/resolve/main/MiniMax-H3-Ref2VA-pruned_rank8_int8_convrot.safetensors | `e09db861c48d13560222948b4e38082bc21b1b7d4ddcaed9c865bf9c3233898c` |
| Text encoder | `qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors` | `models/text_encoders/` | https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/text_encoders/qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors | `35a88d51044231fe332301d7a62aa81e3f2cba62febeb446e2c1e3e0ef76f2c6` |
| Video VAE | `minimax_h3_video_vae_fp16.safetensors` | `models/vae/` | https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/vae/minimax_h3_video_vae_fp16.safetensors | `7c1f131492e7eddacaac9069a61b81bdd39de5cc96561e677c5eab1cdce5e522` |
| Audio VAE (official) | `minimax_h3_audio_vae_fp32.safetensors` | `models/vae/` | https://huggingface.co/Comfy-Org/MiniMax-H3/resolve/main/vae/minimax_h3_audio_vae_fp32.safetensors | `8e505d95dd1561d47abd43d4238fd40d9bb1ae9e147ed0a4cba778d76ae4db48` |
| Phase 1 PDD Acc 8-step | `minimax_h3_ref2va_pdd_acc_8step_comfyui.safetensors` | `models/pdd_acc/` | https://huggingface.co/aptech0081/MiniMax-H3-Acc-LoRAs-ComfyUI/resolve/main/minimax_h3_ref2va_pdd_acc_8step_comfyui.safetensors | `a27df750ad108393a9ef210b81574e9325da2c5f985df8c8897f055bfabe2386` |
| Phase 2 TaoMate 3-step LoRA | `MiniMax-H3/minimax_h3_taomate_3step_lora_avg_rank_19_bf16.safetensors` | `models/loras/MiniMax-H3/` | https://huggingface.co/DeepBeepMeep/MiniMax-H3/resolve/main/loras/minimax_h3_taomate_3step_lora_avg_rank_19_bf16.safetensors | `de9663d974a884b477556748239c6f28239f7ca1825be270f98f023ff5dab6a7` |
| H3 3D latent upscaler | `minimax_h3_latent_upscaler_3d_bf16.safetensors` | `models/latent_upscale_models/` | https://huggingface.co/DeepBeepMeep/MiniMax-H3/resolve/main/minimax_h3/minimax_h3_latent_upscaler_3d_bf16.safetensors | `4f57821f5837f32f7142b67d815606dbd7550f194e5c769f7d6c3f83b146a5e6` |

The checkpoint is user-provided/locally mapped in the current installation; the public URL above is the matching DeepBeepMeep release. Do not commit any of these files because several are multi-gigabyte.
