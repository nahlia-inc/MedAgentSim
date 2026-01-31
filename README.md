## 🚀 Quick Start

### Prerequisites

- **OS**: macOS or Linux
- **Python**: 3.10+ (tested with 3.10)
- **Conda**: Miniconda or Anaconda (recommended on macOS)

> ⚠️ **Important (macOS users)**  
> PyTorch **must be installed via conda**, not pip. Do **not** run `pip install --upgrade torch` on macOS — it will break the environment.

```bash
# Clone your fork (recommended)
# git clone https://github.com/<your-org>/MedAgentSim.git
# cd MedAgentSim

# Create and activate the environment
conda env create -f environment.yml
conda activate mgent

# Install PyTorch via conda (macOS-safe)
conda install -y pytorch torchvision torchaudio -c pytorch

# Install MedAgentSim in editable mode
pip install -e .

# Install Python dependencies
pip install -r requirements.txt

# Optional: exact reproducibility
# pip install -r requirements.lock.txt

# Install LLM SDKs and utilities
pip install -U openai replicate anthropic groq accelerate

# Legacy requirement (do not upgrade)
pip install "django==2.2"

# Verify environment integrity
pip check
```

> ✅ If `pip check` reports **"No broken requirements found"**, your environment is correctly installed.
> If not, please open an issue with your OS, Python version, and full error output.
