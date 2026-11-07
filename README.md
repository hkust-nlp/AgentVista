<div align="center">
  <img src="docs/logo.png" alt="Logo" width="300">
  <h1 align="center">AgentVista: Evaluating Multimodal Agents in<br>Ultra-Challenging Realistic Visual Scenarios</h1>

  <a href="https://arxiv.org/abs/2602.23166">
    <img src="https://img.shields.io/badge/paper-A42C25?style=for-the-badge&logo=arxiv&logoColor=white" alt="Paper">
  </a>
  <a href="https://github.com/hkust-nlp/AgentVista">
    <img src="https://img.shields.io/badge/AgentVista-000000?style=for-the-badge&logo=github&logoColor=white" alt="GitHub">
  </a>
  <a href="https://huggingface.co/datasets/Warrieryes/AgentVista">
    <img src="https://img.shields.io/badge/AgentVista_Dataset-fcd022?style=for-the-badge&logo=huggingface&logoColor=000" alt="Hugging Face">
  </a>
  <a href="https://agentvista-bench.github.io/">
    <img src="https://img.shields.io/badge/Webpage-blue?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Webpage">
  </a>
</div>

---

> *Real-world multimodal agents solve multi-step workflows grounded in visual evidence.*

**AgentVista** is the first benchmark that evaluates multimodal agents on realistic, ultra-challenging visual scenarios requiring long-horizon hybrid tool use. It spans **25 sub-domains** across **7 categories** with **209** expert-curated tasks. Even the best model, **GPT-5.6-Sol**, achieves only **35.4%** overall accuracy. This repository provides a **lightweight yet general agent framework** for reproducible evaluation.


<div align="center">
  <img src="docs/data_examples.png" alt="AgentVista Examples" width="800">
  <br>
  <em>Sampled AgentVista examples from each domain. Each query is grounded in complex, real-world visual scenes and is designed to elicit agentic tool use with multi-step reasoning toward a unique, verifiable answer.</em>
</div>

---

## News

- **[2026/11]** AgentVista is accepted to NeurIPS 2026. The main results are updated with two new frontier models, GPT-5.6-Sol and GPT-6.1-Sol.
- **[2026/02]** AgentVista benchmark, evaluation codebase, and dataset are publicly released.

---

## What is AgentVista?

AgentVista is a benchmark designed to evaluate generalist multimodal agents on **diverse, realistic, and ultra-challenging tasks**. It contains **209 tasks** spanning 25 sub-domains across 7 categories:

| Category | Examples |
|---|---|
| **Commerce** | Product matching, price comparison, nutritional constraint checking |
| **Geography** | Route planning, landmark identification, map-based reasoning |
| **Entertainment** | Media analysis, event identification |
| **Technology** | Hardware troubleshooting, technical diagram interpretation |
| **Society** | Policy lookup, news verification |
| **Academics** | Scientific figure analysis, formula derivation |
| **Culture** | Art identification, cultural artifact matching |

Each task is grounded in detail-rich visual states (daily photos, screenshots, technical diagrams) and requires **multi-step reasoning with interleaved tool use** -- the agent must repeatedly ground visual cues, retrieve external information, and verify intermediate decisions to arrive at a unique, verifiable answer.

### Key Features

- **Vision-centric tasks with realistic images** -- key evidence must come from the visual input, not textual shortcuts.
- **Natural interleaved hybrid tool use** -- solutions mix visual tools and text-based tools across at least two tool categories.
- **Easy to verify and stable over time** -- concise target answers in deterministic formats (number, entity name, short description).
- **Expert-curated with rigorous quality control** -- each instance undergoes agent-centric filtering, expert finalization, execution filtering, and two-round verification.


---

## Benchmark Statistics

| Statistic | Value |
|---|---|
| Total queries | 209 |
| Total images | 307 |
| Primary categories | 7 |
| Secondary categories | 25 |
| Average query length | 408.2 characters |
| Average answer length | 42.0 characters |
| Single-image queries | 152 (72.7%) |
| Multi-image queries | 57 (27.3%) |

---

## Tool Environment

AgentVista provides four tools covering common multimodal agent workflows:

| Tool | Description |
|---|---|
| **`web_search`** | Retrieve web pages via Serper.dev Google Search API |
| **`image_search`** | Text-to-image search and reverse image search via Serper.dev |
| **`visit`** | Open a URL and extract its main textual content (Trafilatura + Jina API fallback) |
| **`code_interpreter`** | Execute Python code in a stateful Jupyter kernel for image processing, arithmetic, structured extraction, and general programming |

All tools are exposed with detailed descriptions and structured inputs/outputs so the model can decide autonomously when and how to call each tool.

---

## Main Results

Performance on AgentVista (accuracy %). Domain abbreviations: **Comm.** (Commerce), **Geog.** (Geography), **Ent.** (Entertainment), **Tech.** (Technology), **Soc.** (Society), **Acad.** (Academics), **Cult.** (Culture).

| Model | Comm. | Geog. | Ent. | Tech. | Soc. | Acad. | Cult. | Single | Multi | **Overall** | Avg Turns |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| GPT-5.6-Sol | 23.81 | 23.08 | 23.08 | 50.00 | 48.00 | **66.67** | **46.67** | **32.89** | **42.11** | **35.41** | 5.48 |
| GPT-6.1-Sol | 23.81 | 23.08 | 20.51 | **55.88** | **52.00** | 46.67 | 40.00 | 32.24 | 40.35 | 34.45 | 5.18 |
| GPT-5.4 | **30.95** | **30.77** | 15.38 | 52.94 | 40.00 | 33.33 | 26.67 | 30.26 | 38.60 | 32.54 | 3.68 |
| Claude-Opus-4.6 | 21.43 | 23.08 | **28.21** | 47.06 | 36.00 | 33.33 | 26.67 | 28.29 | 35.09 | 30.14 | 7.75 |
| Gemini-3.1-Pro | 21.43 | 25.64 | 23.08 | 44.12 | 28.00 | 33.33 | 40.00 | 25.66 | 38.60 | 29.19 | 6.09 |
| Gemini-3-Pro | 16.67 | 28.21 | 23.08 | 32.35 | 32.00 | 40.00 | 40.00 | 23.68 | 38.60 | 27.75 | 6.67 |
| GPT-5.2 | 21.43 | 20.51 | 23.08 | 38.24 | 28.00 | 33.33 | 20.00 | 24.34 | 29.82 | 25.84 | 13.85 |
| GPT-5 | 23.81 | 23.08 | 15.38 | 35.29 | 28.00 | 26.67 | 26.67 | 24.34 | 26.32 | 24.88 | 12.67 |
| GPT-5.1 | 23.81 | 15.38 | 17.95 | 26.47 | 24.00 | 40.00 | 40.00 | 20.39 | 33.33 | 23.92 | 17.14 |
| Claude-Sonnet-4.6 | 19.05 | 25.64 | 10.26 | 20.59 | 44.00 | 40.00 | 26.67 | 22.37 | 28.07 | 23.92 | 12.91 |
| Gemini-3-Flash | 16.67 | 20.51 | 12.82 | 29.41 | 28.00 | 40.00 | 20.00 | 19.08 | 29.82 | 22.01 | 7.78 |
| o3 | 21.43 | 17.95 | 10.26 | 23.53 | 44.00 | 26.67 | 13.33 | 19.08 | 28.07 | 21.53 | 13.18 |
| Claude-Opus-4.1 | 11.90 | 23.08 | 12.82 | 29.41 | 20.00 | 26.67 | 13.33 | 17.11 | 24.56 | 19.14 | 7.28 |
| Claude-Sonnet-4.5 | 11.90 | 23.08 | 10.26 | 26.47 | 24.00 | 20.00 | 13.33 | 17.76 | 19.30 | 18.18 | 9.99 |
| Claude-Opus-4 | 19.05 | 15.38 | 7.69 | 26.47 | 24.00 | 20.00 | 6.67 | 12.50 | 29.82 | 17.22 | 6.89 |
| Grok-4 | 11.90 | 23.08 | 10.26 | 20.59 | 28.00 | 0.00 | 0.00 | 14.47 | 17.54 | 15.31 | 16.44 |
| Claude-Sonnet-4 | 9.52 | 17.95 | 5.13 | 29.41 | 16.00 | 20.00 | 6.67 | 11.84 | 22.81 | 14.83 | 5.37 |
| o4-mini | 2.38 | 10.26 | 5.13 | 8.82 | 12.00 | 13.33 | 0.00 | 7.24 | 7.02 | 7.18 | 1.89 |

**Key Takeaways:**
- AgentVista is **ultra-challenging**: the best model (GPT-5.6-Sol) achieves only 35.41% overall accuracy.
- Performance varies across domains, revealing complementary strengths among model families.
- Multi-image inputs are not uniformly harder -- additional views often provide complementary evidence.
- A sizable gap exists between open-source (Qwen3-VL-235B at 13.88%) and closed-source models, highlighting room for improvement in open-source multimodal agents.

---

## Dataset

The AgentVista benchmark dataset is hosted on Hugging Face. Download it before running evaluation:

```bash
pip install huggingface_hub
huggingface-cli download Warrieryes/AgentVista --repo-type dataset --local-dir ./datasets

```

The dataset includes task queries (JSON) and associated images. After downloading, your directory structure should look like:

```
datasets/
  val.json                   # Evaluation queries with ground truth
  <image files>              # Referenced images
```

For more details, visit the dataset page: [https://huggingface.co/datasets/Warrieryes/AgentVista](https://huggingface.co/datasets/Warrieryes/AgentVista)

---

## Installation

### Prerequisites

- Python 3.10+
- A reasoning model API key (OpenAI, OpenRouter, or compatible endpoint)
- A [Serper.dev](https://serper.dev) API key for web/image search
- A [Jina](https://jina.ai) API key for webpage content extraction (optional but recommended)

### Setup

```bash
# Clone the repository
git clone https://github.com/hkust-nlp/AgentVista-Bench.git
cd AgentVista-Bench

# (Recommended) Create a clean Conda environment
conda create -n agentvista python=3.10
conda activate agentvista

# Install dependencies
pip install -r requirements.txt
```

### Environment Variables

All API keys are provided via environment variables. **Never hardcode credentials.**

```bash
# Required: Reasoning model
export REASONING_MODEL_NAME="openai/gpt-4o"          # or any supported model identifier
export REASONING_API_KEY="your-api-key"
export REASONING_END_POINT="https://openrouter.ai/api/v1/chat/completions"

# Required: Search tools
export SERPAPI_KEY="your-serper-api-key"
export JINA_API_KEY="your-jina-api-key"

# Optional: Verifier for automatic accuracy scoring (requires ground truth)
export VERIFIER_MODEL_NAME="openai/gpt-4.1"
export VERIFIER_API_KEY="your-verifier-api-key"
export VERIFIER_END_POINT="https://openrouter.ai/api/v1/chat/completions"

# Optional: Control which tools are enabled (default: all)
export ENABLED_TOOLS="web_search,image_search,visit,code_interpreter"
```

---

## How to Run

### Quick Start

The simplest way to run the agent:

```bash
# 1. Set environment variables (see above)
# 2. Run the evaluation script
bash run.sh
```

### Running Directly with Python

For more control, call `infer.py` directly:

```bash
python infer.py \
  --input-file /path/to/val.json \
  --image-folder /path/to/images \
  --output-dir /path/to/output \
  --max-turns 30 \
  --max-images 100 \
  --max-total-tokens 65536 \
  --skip-completed
```

### Data Format

- **Input**: A JSON or JSONL file where each item contains:
  - `question_id` or `doc_id` -- unique identifier
  - `problem` or `question` -- the task query
  - `images` (optional) -- list of image paths relative to the image folder
  - `solution` (optional) -- ground truth answer for automatic scoring

- **Images**: A single folder containing all referenced images.


### Output Structure

Results are written to `--output-dir` with the following structure:

```
output/
  results.jsonl              # Aggregated results
  summary_metrics.json       # Overall accuracy and statistics
  <question_id>/
    traj.jsonl               # Full agent trajectory (turns, tool calls, responses)
    metrics.json             # Per-sample accuracy and analysis
```

---

## Project Structure

```
agenvista/
  infer.py                   # Main inference entry point
  run.sh                     # Convenience script to launch evaluation
  requirements.txt           # Python dependencies
  configs/
    tool_configs.yaml        # Tool-specific configuration
    prompt_loader.py         # Inference prompt loader
  prompts/
    inference_prompts.yaml   # System and turn prompts
  engine/
    api/
      api_caller.py          # LLM API caller with retry and fallback
      api_model_caller.py    # Model-level orchestration
      api_processors.py      # Single-sample processing pipeline
      api_tool_handler.py    # Tool dispatch and execution
  tools/
    base.py                  # Abstract base class for tools
    tool_registry.py         # Tool registration and retrieval
    web_search.py            # Web search via Serper.dev
    image_search.py          # Image search (text-to-image + reverse)
    visit.py                 # Webpage content extraction
    code_interpreter.py      # Python code execution via Jupyter kernel
  search/
    tree.py                  # Search tree for reasoning state management
  utils/
    context_utils.py         # Token estimation and image processing
    function_call_parser.py  # Parse API responses for tool calls
    result_utils.py          # Result writing and summary statistics
    tool_schema_builder.py   # Build OpenAI-compatible tool schemas
    general_qa_tool.py       # QA verifier for accuracy scoring
```

---

## Citation

If you find AgentVista useful, please cite our paper:

```bibtex
@article{su2026agentvista,
  title={AgentVista: Evaluating Multimodal Agents in Ultra-Challenging Realistic Visual Scenarios},
  author={Su, Zhaochen and Gao, Jincheng and Guo, Hangyu and Liu, Zhenhua and Zhang, Lueyang and Geng, Xinyu and Huang, Shijue and Xia, Peng and Jiang, Guanyu and Wang, Cheng and others},
  journal={arXiv preprint arXiv:2602.23166},
  year={2026}
}
```

