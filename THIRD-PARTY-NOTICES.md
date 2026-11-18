# Third-party notices

Transcribe Studio is distributed under the MIT licence (see `LICENSE`). The Windows installer and the
components it downloads include software from other projects, listed below with their licences. In an
installed copy, the licence texts are in `resources\licenses\` inside the installation folder.

## Shipped in the installer

| Component | Version | Licence | Source |
|---|---|---|---|
| Electron (includes Chromium and Node.js) | 33.4.11 | MIT; Chromium and Node.js licences in `LICENSES.chromium.html` and `LICENSE.electron.txt` next to the executable | https://github.com/electron/electron |
| CPython, build of python-build-standalone | 3.12.16 (release 20261026, `install_only_stripped`, x86_64-pc-windows-msvc) | Python Software Foundation License Version 2 and the licence terms of the third-party code it includes, as listed in `licenses\python-LICENSE.txt` (the CPython licence file of this build) | https://github.com/astral-sh/python-build-standalone/releases/tag/20261026 · https://www.python.org/ |
| FFmpeg (`ffmpeg.exe`, static LGPL build by BtbN/FFmpeg-Builds) | n8.1.3-27-g8dca1586f4 (autobuild-2026-10-31-12-59, `win64-lgpl-8.1`) | GNU Lesser General Public License version 3 (`--enable-version3`, no `--enable-gpl`, no `--enable-nonfree`); `licenses\ffmpeg-LICENSE.txt` | Binary: https://github.com/BtbN/FFmpeg-Builds/releases/tag/autobuild-2026-10-31-12-59 · FFmpeg source of this build: https://github.com/FFmpeg/FFmpeg/commit/8dca1586f4 (tag n8.1.3 + 27 commits) · build scripts and the exact versions of the bundled libraries: https://github.com/BtbN/FFmpeg-Builds |
| uv (`uv.exe`, the Python package installer by Astral, used by the first-run setup to install the downloaded packages) | 0.13.8 (`uv-x86_64-pc-windows-msvc.zip`) | MIT OR Apache-2.0; `licenses\uv-LICENSE-MIT.txt` and `licenses\uv-LICENSE-APACHE.txt`. The binary includes third-party Rust crates under their own licences, listed in the uv repository | https://github.com/astral-sh/uv/releases/tag/0.13.8 |
| pywhispercpp (Python bindings for whisper.cpp) built with the Vulkan backend, as the wheel `pywhispercpp-1.5.1+vulkan-cp312-cp312-win_amd64.whl`; it contains whisper.cpp and ggml (`whisper.dll`, `ggml*.dll`). Installed by the first-run setup; used by the experimental "GPU Vulkan" profile | pywhispercpp 1.5.1 (commit `f7bf62118c0a33a43cf8aabb58eef16cea5d16c4`) with whisper.cpp commit `f24588a272ae8e23280d9c220536437164e6ed28`; built by this project's CI (`.github/workflows/whispercpp-vulkan-wheel.yml`) with the Vulkan SDK 1.4.357.0, sha256 `e847089a401681715d550d3f0309b72f2bbf5cee81a9d03a0e85f90b9f091dbb` | MIT (pywhispercpp, whisper.cpp and ggml; licence file inside the wheel). The wheel also carries, with hashed file names, the DLLs it links to: the Khronos Vulkan loader `vulkan-1.dll` from the Vulkan SDK (Apache-2.0, https://github.com/KhronosGroup/Vulkan-Loader) and the Microsoft Visual C++ runtime `msvcp140.dll` and OpenMP runtime `vcomp140.dll` (Visual Studio redistribution terms, as below) | https://github.com/absadiki/pywhispercpp · https://github.com/ggml-org/whisper.cpp |
| Microsoft Visual C++ 2015-2022 runtime DLLs (`msvcp140*.dll`, `vcruntime140*.dll`, `concrt140.dll`, `vcomp140.dll`), taken from the official Microsoft Visual C++ Redistributable (x64), `vc_redist.x64.exe` | 14.44.35211.0 (redistributable sha256 `cc0ff0eb1dc3f5188ae6300faef32bf5beeba4bdd6e8e445a9184072096b713b`; the version and hash of the file used by each build are recorded in `licensesuild-manifest.txt`) | Microsoft Visual C++ Redistributable licence terms; the files are redistributed app-local next to `python.exe` under the Visual Studio redistribution terms ("redistributable files") | https://aka.ms/vs/17/release/vc_redist.x64.exe · https://learn.microsoft.com/cpp/windows/latest-supported-vc-redist |

FFmpeg is used as a separate program (`ffmpeg.exe`), called by the app to convert audio and video; it is
not linked into the app. Its source code is available at the links above; the version and build
configuration are printed by `ffmpeg.exe -version`. The FFmpeg build includes LGPL-compatible libraries
such as LAME (MP3 encoding), Opus, Vorbis, dav1d and libvpx; their licences are documented by the
FFmpeg-Builds project.

## Downloaded by the first-run setup (not in the installer)

The setup downloads these Python packages from PyPI (and, for the NVIDIA option, PyTorch from
download.pytorch.org) into the per-user folder. Exact versions and checksums are in
`python-setup/lock-cpu.json` and `python-setup/lock-cuda.json`. Main packages and their declared
licences:

| Package | Licence |
|---|---|
| PyTorch (`torch`), `torchaudio` | BSD-3-Clause / BSD-2-Clause (the CUDA build includes NVIDIA CUDA runtime libraries under the NVIDIA CUDA EULA) |
| faster-whisper, CTranslate2 | MIT |
| silero-vad | MIT |
| SpeechBrain | Apache-2.0 |
| scikit-learn, SciPy | BSD-3-Clause |
| NumPy | BSD-3-Clause (bundled parts: 0BSD, MIT, Zlib, CC0-1.0) |
| soundfile, psutil, threadpoolctl | BSD-3-Clause |
| PyAudioWPatch | Apache-2.0 (includes PortAudio, MIT) |
| python-soxr (`soxr`) | LGPL-2.1-or-later (libsoxr) |
| python-docx | MIT |
| ONNX Runtime | MIT |
| platformdirs | MIT |
| PyAV (`av`, includes FFmpeg libraries) | BSD-3-Clause; bundled FFmpeg under LGPL |
| Hugging Face `huggingface_hub`, `tokenizers`, `transformers`, `accelerate` | Apache-2.0 |

Each package's licence file is installed with it, in `python\Lib\site-packages\<package>-<version>.dist-info\`.

## Models downloaded on first use (not in the installer)

Downloaded from Hugging Face into the user's Hugging Face cache the first time a profile needs them:

| Model | Used by | Licence (as published by its authors) |
|---|---|---|
| `Systran/faster-whisper-small` | Leve | MIT |
| `speechbrain/spkrec-ecapa-voxceleb` | speaker separation (all profiles) | Apache-2.0 |
| `openai/whisper-large-v3-turbo` | GPU | MIT |
| `dropbox-dash/faster-whisper-large-v3-turbo` (CTranslate2 conversion of `openai/whisper-large-v3-turbo`, revision `0a363e9161cbc7ed1431c9597a8ceaf0c4f78fcf`) | Preciso | MIT |
| `ggerganov/whisper.cpp`, file `ggml-large-v3-turbo-q8_0.bin` (ggml conversion of `openai/whisper-large-v3-turbo`, 8-bit, revision `5359861c739e955e79d9a303bcbc70fb988958b1`) | GPU Vulkan (experimental) | MIT |
