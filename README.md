# MiniMax H3 — ComfyUI two-phase workflow

Đây là bản workflow cuối dùng MiniMax H3 Ref2VA với PDD Acc 8-step ở phase 1 và TaoMate 3-step sau latent upscale ở phase 2. Repo không chứa checkpoint, LoRA, VAE hay dữ liệu đầu vào; xem [`models-manifest.md`](models-manifest.md) để tải đúng file và kiểm tra SHA-256.

## Cài đặt nhanh

1. Cài/ cập nhật ComfyUI theo commit được ghi trong [`requirements.md`](requirements.md).
2. Tạo thư mục `ComfyUI/custom_nodes` nếu chưa có.
3. Cài custom node theo thứ tự trong `requirements.md`. PDD phải dùng fork `phanhieu01/ComfyUI-MiniMax-H3-PDD-Acc` và đúng commit đã pin; không thay bằng bản upstream chưa có compatibility patch.
4. Tải model vào đúng thư mục trong [`models-manifest.md`](models-manifest.md). Không đưa file model lớn vào Git.
5. Khởi động lại ComfyUI rồi mở `workflows/minimax_h3_two_phase_socket_refs.json` từ menu **Load**.

Ví dụ clone node:

```powershell
cd D:\ComfyUI\custom_nodes
git clone https://github.com/phanhieu01/ComfyUI-MiniMax-H3-PDD-Acc.git ComfyUI-MiniMax-H3-PDD-Acc
git -C ComfyUI-MiniMax-H3-PDD-Acc checkout 8e23e9501a39e6290e1112bf051a5ed63889b58d
```

Các node còn lại và commit chính xác nằm trong `requirements.md`; `comfyui-manager-snapshot.json` là bản tóm tắt để nhập/đối chiếu với ComfyUI Manager.

## Sử dụng workflow

- **Reference Manager** ở ngoài subgraph chỉ lưu số lượng, tên file và lựa chọn nguồn audio ghép với từng video. Các `VHS_LoadImagePath`, `VHS_LoadVideoPath`, `VHS_LoadAudio`, crop/resize/FPS và công tắc slot nằm bên trong subgraph.
- Chọn số lượng reference image/video/video-audio/audio trong manager, sau đó chọn file. Thứ tự tag trong prompt phải khớp thứ tự input: `<Picture 1..9>`, `<Video 1..3>`, `<Audio 1..3>`; audio ghép lấy theo video được chọn, không nạp lại cùng video.
- Bật **Generate audio without reference** khi muốn H3 tự sinh soundtrack. Khi bật, bỏ các câu `<Audio N>: fully_copy`/mô tả copy audio khỏi prompt và để các ô reference audio trống.
- `Final resolution (MP)` và `Aspect ratio` quyết định WIDTH/HEIGHT cuối. FPS và số frame nên khớp video tham chiếu.
- **One phase (on)**: bỏ latent upscale/TaoMate, chạy PDD 8-step trực tiếp ở độ phân giải cuối.
- **Two phase (off)**: phase 1 chạy PDD 8-step ở `phase1_scale` (mặc định 0.5, có giới hạn tối thiểu theo node), sau đó latent upscale và phase 2 TaoMate 3-step.
- `Phase 2 sigma schedule` dùng ManualSigmas. Giá trị đầu là mức denoise hiệu dụng; baseline hiện tại là `0.6000, 0.4667, 0.2333, 0.0000`. Có thể chỉnh thận trọng khi đã xác nhận bố cục phase 1.
- Giữ `Seed` cố định khi so sánh one-phase với two-phase.

## PDD và audio VAE

PDD node giữ `enabled=true` qua `BOOLConstant`; fork có fallback cho graph cũ gửi `enabled=false` mà không nối `bypass_sigmas`. Audio VAE phải là `minimax_h3_audio_vae_fp32.safetensors` chính thức. Không dùng bản `_comfy` cũ vì có thể gây nhiễu/rè audio.

## Kiểm tra lỗi thường gặp

- Node đỏ/missing: kiểm tra `requirements.md`, đúng commit và restart ComfyUI.
- Không có audio: kiểm tra audio VAE, đường `VAEDecodeAudio` phase 1 và lựa chọn audio mode/prompt.
- Motion/layout lệch: kiểm tra prompt H3, thứ tự reference tags, cùng seed và `phase1_scale`; phase 2 không được nối audio latent mới.

