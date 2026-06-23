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

# MedAgentSim: Self-Evolving Multi-Agent Simulations for Realistic Clinical Interactions
<div align="center">
  <img src="assets/Tom_Moreno_scaled_10x_pngcrushed.jpg" alt="MedAgentSim Logo" width="100"/>
  <p><i>An open-source framework for simulating realistic doctor-patient interactions</i></p>
</div>
<a href="https://arxiv.org/abs/2503.22678">
  <img src="https://img.shields.io/badge/📝-Paper-blue" height="25">
</a>
<a href="https://www.youtube.com/watch?v=0qmC0ovWcr4">
  <img src="https://img.shields.io/badge/🎥-Video-red" height="25">
</a>
<a href="https://github.com/MAXNORM8650/MedAgentSim/graphs/contributors">
  <img src="https://img.shields.io/github/contributors/MAXNORM8650/MedAgentSim" height="25">
</a>
<a href="https://github.com/MAXNORM8650/MedAgentSim/stargazers">
  <img src="https://img.shields.io/github/stars/MAXNORM8650/MedAgentSim" height="25">
</a>
<a href="https://github.com/MAXNORM8650/MedAgentSim/network/members">
  <img src="https://img.shields.io/github/forks/MAXNORM8650/MedAgentSim" height="25">
</a>
<a href="https://github.com/MAXNORM8650/MedAgentSim/issues">
  <img src="https://img.shields.io/github/issues/MAXNORM8650/MedAgentSim" height="25">
</a>
<a href="https://github.com/MAXNORM8650/MedAgentSim/blob/main/LICENSE">
  <img src="https://img.shields.io/github/license/MAXNORM8650/MedAgentSim" height="25">
</a>
<a href="https://medagentsim.netlify.app/">
  <img src="https://img.shields.io/badge/🌐-Website-green" height="25">
</a>
<a href="https://www.python.org/downloads/">
  <img src="https://img.shields.io/badge/python-3.10+-blue.svg" height="25">
</a>
<a href="https://huggingface.co/datasets/ItsMaxNorm/MedAgentSim-datasets">
  <img src="https://img.shields.io/badge/HuggingFace-Datasets-orange" height="25">
</a>

## 📣 Recent Updates

* [13/05/2025] 🎉 Our paper **MedAgentSim: Self-Evolving Multi-Agent Simulations for Realistic Clinical Interactions** has been accepted early at **MICCAI 2025**.
* [31/03/2025] 🔥 We release **MedAgentSim: Self-Evolving Multi-Agent Simulations for Realistic Clinical Interactions**.

## 🔍 Overview

MedAgentSim is an open-source simulated hospital environment designed to evaluate and enhance large language model (LLM) performance in dynamic diagnostic settings. Unlike prior approaches, our framework requires doctor agents to actively engage with patients through multi-turn conversations, requesting relevant medical examinations and imaging results to mimic real-world diagnostic processes.

Key features:
- **Multi-Agent Architecture**: Doctor, patient, and measurement agents interact in a realistic clinical setting
- **Self-Improvement Mechanisms**: Models iteratively refine their diagnostic strategies through experience
- **Experience Replay**: Past successful diagnoses inform future cases through knowledge retrieval
- **Visual Game Simulation**: Built with Phaser for an intuitive, interactive environment
- **Multi-Modal Capabilities**: Integration with vision language models for medical image interpretation

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

### Running the Simulation

```bash
# Start the server
python -m medsim.server

# In a separate terminal, launch the client
python -u -m medsim.simulate \
  --doctor_llm meta-llama/Llama-3.2-3B-Instruct \
  --patient_llm meta-llama/Llama-3.2-3B-Instruct \
  --measurement_llm meta-llama/Llama-3.2-3B-Instruct \
  --moderator_llm meta-llama/Llama-3.2-3B-Instruct
```

Visit `http://localhost:8000/simulator_home` in your browser. Make sure to keep that tab open and active during the simulation.

### Host models using vLLM

```bash
vllm serve unsloth/Llama-3.2-11B-Vision-Instruct-unsloth-bnb-4bit \
  --dtype auto \
  --quantization bitsandbytes \
  --load_format bitsandbytes \
  --tensor-parallel-size 4 \
  --max-model-len 8192 \
  --limit-mm-per-prompt image=1

vllm serve meta-llama/Llama-3.2-3B-Instruct --tensor-parallel-size 4
vllm serve unsloth/Llama-3.3-70B-Instruct-bnb-4bit --quantization bitsandbytes --load_format bitsandbytes
```

## 🏥 Simulation Modes

MedAgentSim supports three core interaction modes:

1. **Generation Mode**: Patient agent autonomously creates cases, generating illnesses, symptoms, and test results
2. **Dataset Mode**: Patient responses derived from predefined medical datasets
3. **Control Mode**: Human users can control either the doctor or patient agent for real-time interaction

## 🧠 Model Support

- **Open-Source Models**: LLaMA 3.3, Mistral, Mixtral, Qwen2
- **Vision-Language Models**: LLaVA 1.5, QwenVL
- **Custom Models**: Integrate your own models following our documentation

## 📊 Benchmarks

| Benchmark | Description | #Cases |
|-----------|-------------|--------|
| NEJM | Complex real-world cases | 15 |
| NEJM Extended | Additional complex cases | 120 |
| MedQA | Simulated diagnostic scenarios | 106 |
| MedQA Extended | Extended diagnostic scenarios | 214 |
| MIMIC-IV | Real-world clinical cases | 288 |

## 🧩 Project Structure

```
MedAgentSim/
├── assets/
├── datasets/
├── docs/
├── medsim/
│   ├── configs/
│   ├── core/
│   ├── server/
│   ├── simulate/
│   ├── utils/
├── Simulacra/
├── MedPromptSimulate/
├── examples/
├── tests/
├── requirements.txt
├── LICENSE
└── README.md
```

## Datasets
```bash
from datasets import load_dataset

# Load all files
ds = load_dataset("ItsMaxNorm/MedAgentSim-datasets")

# Load a specific file
ds = load_dataset("ItsMaxNorm/MedAgentSim-datasets", data_files="medqa_v1.parquet")

# Access the data
print(ds["train"][0])
```

## 👥 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md).

## 📄 License

Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0).

## 📚 Citation

```bibtex
@inproceedings{almansooriandkumarMedAgentSim,
  title={Self-Evolving Multi-Agent Simulations for Realistic Clinical Interactions},
  author={Mohammad Almansoori and Komal Kumar and Hisham Cholakkal},
  booktitle={International Conference on Medical Image Computing and Computer-Assisted Intervention},
  year={2025}
}
```

## 🙏 Acknowledgements

Thanks to AgentClinic, Microsoft PromptBase, Generative Agents, and MBZUAI for support.

---
## Star History Chart
[![Star History Chart](https://api.star-history.com/svg?repos=MAXNORM8650/MedAgentSim&type=date&legend=top-left)](https://www.star-history.com/#MAXNORM8650/MedAgentSim&type=date&legend=top-left)
