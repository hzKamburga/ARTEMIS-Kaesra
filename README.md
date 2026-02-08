<h1 align="center">🏹 ARTEMIS-Kaesra</h1>
<p align="center"><strong>A</strong>utomated <strong>R</strong>ed <strong>T</strong>eaming <strong>E</strong>ngine with <strong>M</strong>ulti-agent <strong>I</strong>ntelligent <strong>S</strong>upervision - <strong>Kaesra Tech API Edition</strong></p>
<p align="center">ARTEMIS is an autonomous agent created by the <a href="https://trinity.cs.stanford.edu/">Stanford Trinity project</a> to automate vulnerability discovery.</p>
<p align="center">This fork integrates <a href="https://kaesra.tech">Kaesra Tech API</a> for all LLM calls.</p>

---

## 🚀 Quickstart (Linux)

### Prerequisites

Install `uv` if you haven't already:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Install the latest version of Rust (required for building):

```bash
# Remove old Rust if installed via apt
sudo apt remove rustc cargo
sudo apt install libssl-dev

# Install rustup (the official Rust toolchain installer)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Restart shell or source the environment
source ~/.cargo/env

# Install latest stable Rust
rustup install stable
rustup default stable
```

### Build Codex Binary

```bash
cargo build --release --manifest-path codex-rs/Cargo.toml
```

### Setup Python Environment

```bash
uv sync
source .venv/bin/activate
```

### Environment Configuration

Copy the example configuration and add your API keys:

```bash
cp .env.example .env
# Edit .env with your Kaesra API key
```

Required environment variables:
- `KAESRA_API_KEY` - Your Kaesra Tech API key
- `KAESRA_BASE_URL` - API endpoint (default: `https://api-kaesra-tech.vercel.app/v1`)

Optional model configuration:
- `KAESRA_SUPERVISOR_MODEL` - Supervisor model (default: `openai-gpt-5.2`)
- `KAESRA_SUMMARIZATION_MODEL` - Summarization model (default: `anthropic-claude-sonnet-3.7`)
- `KAESRA_ROUTER_MODEL` - Router model (default: `anthropic-claude-sonnet-3.7`)
- `KAESRA_TODO_GENERATOR_MODEL` - TODO generator model (default: `google-gemini-3-pro-preview`)
- `KAESRA_PROMPT_GENERATOR_MODEL` - Prompt generator model (default: `google-gemini-3-pro-preview`)
- `KAESRA_AVAILABLE_MODELS` - Available models for switching (comma-separated)

### Quick Test Run

Try a simple CTF challenge to verify everything works:

```bash
python -m supervisor.supervisor \
  --config-file configs/tests/ctf_easy.yaml \
  --benchmark-mode \
  --duration 10 \
  --skip-todos
```

This runs a 10-minute test on an easy CTF challenge in benchmark mode (no triage process).

---

## 🔧 Kaesra Tech API Configuration

### Default Models

| Component | Default Model |
|-----------|---------------|
| Supervisor | `openai-gpt-5.2` |
| Summarization | `anthropic-claude-sonnet-3.7` |
| Router | `anthropic-claude-sonnet-3.7` |
| TODO Generator | `google-gemini-3-pro-preview` |
| Prompt Generator | `google-gemini-3-pro-preview` |
| Web Search | `openai-gpt-5.2` |

### Example .env File

```bash
KAESRA_API_KEY="ksrt_live_your_api_key_here"
KAESRA_BASE_URL="https://api-kaesra-tech.vercel.app/v1"

KAESRA_SUPERVISOR_MODEL=openai-gpt-5.2
KAESRA_SUMMARIZATION_MODEL=anthropic-claude-sonnet-3.7
KAESRA_ROUTER_MODEL=anthropic-claude-sonnet-3.7
KAESRA_TODO_GENERATOR_MODEL=google-gemini-3-pro-preview
KAESRA_PROMPT_GENERATOR_MODEL=google-gemini-3-pro-preview
KAESRA_WEB_SEARCH_MODEL=openai-gpt-5.2

KAESRA_AVAILABLE_MODELS=openai-gpt-5.2,anthropic-claude-sonnet-3.7,google-gemini-3-pro-preview
```

---

## 🐳 Docker

### Docker Quickstart

Build the Docker image:

```bash
docker build -t artemis-kaesra .
```

### Running with Docker

```bash
docker run -it \
  --env-file .env \
  -v $(pwd)/logs:/app/logs \
  artemis-kaesra \
  python -m supervisor.supervisor \
    --config-file configs/tests/ctf_easy.yaml \
    --benchmark-mode \
    --duration 10 \
    --skip-todos
```

---

## 📁 Project Structure

```
ARTEMIS/
├── supervisor/              # Python supervisor code
│   ├── orchestration/       # Orchestrator, router, prompt generator
│   ├── triage/             # Triage manager
│   ├── prompts/            # System prompts
│   └── submissions/        # Submission handlers
├── codex-rs/               # Rust codex binary source
├── configs/                # Configuration files
├── docs/                   # Documentation
└── .env.example            # Environment variables template
```

---

## 🔗 Links

- **Original Project**: [Stanford-Trinity/ARTEMIS](https://github.com/Stanford-Trinity/ARTEMIS)
- **Kaesra Tech**: [https://kaesra.tech](https://kaesra.tech)
- **API Documentation**: [https://api-kaesra-tech.vercel.app](https://api-kaesra-tech.vercel.app)

---

## 📜 License

This repository is licensed under the [Apache-2.0 License](LICENSE).

This project uses [OpenAI Codex](https://github.com/openai/codex) as a base, forked from [commit c221eab](https://github.com/openai/codex/commit/c221eab0b5cad59ce3dafebf7ca630f217263cc6).
