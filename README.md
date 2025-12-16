# **Z-Image-Turbo-LoRA-DLC**

> A Gradio-based demonstration for the Tongyi-MAI/Z-Image-Turbo diffusion pipeline, enhanced with a curated collection of LoRAs (Low-Rank Adaptations) for style transfer and creative image generation. Users can select from 27 pre-loaded LoRAs (e.g., Turbo Pencil, Ghibli Style, Pixel Art) or add custom ones from Hugging Face repositories. Generates high-quality images from text prompts, with trigger words automatically integrated for optimal results. Supports optimizations like AoTI compilation and FA3 for faster inference.

## Features

- **LoRA Gallery**: Interactive selection from 27 specialized LoRAs, each with preview images, trigger words, and direct links to Hugging Face repos.
- **Custom LoRA Support**: Input any Hugging Face repo (e.g., "Shakker-Labs/AWPortrait-Z") to dynamically load and use new styles; auto-detects weights, trigger words, and previews.
- **Prompt Integration**: Automatically prepends or appends LoRA trigger words to prompts for seamless style application.
- **Advanced Controls**: Adjustable steps (1-50), seed randomization, LoRA scale (0-3), resolution (up to 1536x1536), and CFG scale (forced to 0.0 for Turbo mode).
- **Optimizations**: Applies AoTI compilation and FA3 for reduced memory and faster generation on CUDA.
- **Custom Theme**: OrangeRedTheme with gradients, enhanced typography, and responsive CSS for a polished UI.
- **Queueing and Progress**: Handles up to 60 concurrent jobs with tqdm-tracked progress bars.
- **Base Model Fallback**: Generates without LoRAs using the pure Z-Image-Turbo pipeline.

---

## Example Inference

<img width="1798" height="1438" alt="Screenshot 2025-12-16 at 19-15-27 Z Image Turbo LoRA DLC - a Hugging Face Space by prithivMLmods" src="https://github.com/user-attachments/assets/f67aca8c-85d6-44ca-976c-bb7ab3e4c5f9" />

<img width="1344" height="1024" alt="image22" src="https://github.com/user-attachments/assets/14c1c882-f2ea-4f84-874f-bd0f2040aab5" />

---

## Prerequisites

- Python 3.10 or higher.
- CUDA-compatible GPU (recommended for bfloat16; falls back to CPU but slower).
- pip >= 23.0.0 (see pre-requirements.txt).
- Stable internet for initial model/LoRA downloads from Hugging Face.

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/PRITHIVSAKTHIUR/Z-Image-Turbo-LoRA-DLC.git
   cd Z-Image-Turbo-LoRA-DLC
   ```

2. Install pre-requirements (for pip version):
   Create a `pre-requirements.txt` file with the following content, then run:
   ```
   pip install -r pre-requirements.txt
   ```

   **pre-requirements.txt content:**
   ```
   pip>=23.0.0
   ```

3. Install dependencies:
   Create a `requirements.txt` file with the following content, then run:
   ```
   pip install -r requirements.txt
   ```

   **requirements.txt content:**
   ```
   git+https://github.com/huggingface/diffusers.git@refs/pull/12790/head
   huggingface_hub
   gradio==6.1.0
   sentencepiece
   transformers
   torchvision
   accelerate
   kernels
   spaces
   torch
   numpy
   peft
   ```

4. Start the application:
   ```
   python app.py
   ```
   The demo launches at `http://localhost:7860` (or the provided URL if using Spaces).

## Usage

1. **Select LoRA**: Browse the gallery and click a preview (e.g., "Turbo Pencil") to load it; the prompt placeholder updates with the style name.

2. **Enter Prompt**: Type a description (e.g., "a serene mountain landscape"); trigger words (e.g., "pencil sketch") are auto-added if applicable.

3. **Configure Settings**:
   - Expand "Advanced Settings" for steps (default 9), seed, resolution, and LoRA scale (default 0.95).
   - For custom LoRAs, enter a repo path (e.g., "Shakker-Labs/AWPortrait-Z") and press Enter.

4. **Generate**: Click "Generate" or submit the prompt; monitor the progress bar.

5. **Output**: View the generated image; download or regenerate with new seeds.

### Example Workflow
- Select "Ghibli Style" LoRA.
- Prompt: "a whimsical forest adventure".
- Settings: 1024x1024, 9 steps, seed 42.
- Output: Ghibli-inspired image with trigger "Ghibli Style" integrated.

### Pre-Loaded LoRAs

| Index | Title                  | Trigger Word                  | Repo Example |
|-------|------------------------|-------------------------------|--------------|
| 0     | Turbo Pencil          | pencil sketch                | Ttio2/Z-Image-Turbo-pencil-sketch |
| 1     | AWPortrait Z          | Portrait                     | Shakker-Labs/AWPortrait-Z |
| 2     | Childrens Drawings    | Children Drawings            | ostris/z_image_turbo_childrens_drawings |
| ...   | ...                   | ...                          | ... |

(Full list in code; supports 27 styles like Pixel Art, 80s Horror, etc.)

## Troubleshooting

- **LoRA Loading Errors**: Ensure repo has `.safetensors`; check console for warnings. Custom repos must match Z-Image-Turbo base.
- **Optimization Fails**: AoTI/FA3 requires compatible hardware; fallback to standard pipeline without errors.
- **OOM on GPU**: Reduce resolution/steps or use `low_cpu_mem_usage=True`; clear cache with `torch.cuda.empty_cache()`.
- **Custom LoRA Invalid**: Verify Hugging Face path; must contain model card with `instance_prompt` or detectable weights/image.
- **Generation Slow**: Turbo mode uses 0.0 CFG; increase steps for quality but expect longer times.
- **UI Issues**: CSS targets gallery/buttons; set `ssr_mode=True` if rendering fails.
- **Diffusers Branch**: Uses PR #12790; update via git if conflicts.

## Contributing

Contributions welcome! Fork the repo, add new LoRAs to the `loras` list, or enhance UI/optimizations, then submit PRs with tests. Ideas:
- More LoRA presets.
- Img2Img support (currently ignored for Turbo).
- Batch generation.
- 
Repository: [https://github.com/PRITHIVSAKTHIUR/Z-Image-Turbo-LoRA-DLC.git](https://github.com/PRITHIVSAKTHIUR/Z-Image-Turbo-LoRA-DLC.git)

## License

Apache License 2.0. See [LICENSE](LICENSE) for details.

Built by Prithiv Sakthi. Report issues via the repository.
