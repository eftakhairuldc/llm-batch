# llm-batch

Batch prompt runner with real rate limiting and retries

## Getting started

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
```

## Usage

```bash
python batch.py prompts.jsonl -o answers.jsonl --workers 4 --rpm 300
```

## Highlights

- Failures go to a sidecar file with error type, message and status
- Idempotent: ids already in the output are skipped on a rerun
- A bad input line is logged and skipped, never fatal
- JSONL in, JSONL out: the input is streamed line by line
- Progress, token counts and a cost estimate on stderr
- Real rate limiting: sliding windows on requests/min and tokens/min
- 4xx fails fast; 429 and 5xx retry with jittered backoff
- Per-row overrides for model, system, temperature and max_tokens

## Project structure

```text
├── .github/
│   └── workflows/
│       └── ci.yml
├── docs/
│   ├── configuration.md
│   ├── development.md
│   ├── roadmap.md
│   ├── tradeoffs.md
│   └── usage.md
├── examples/
│   └── quickstart.md
├── tests/
│   └── test_smoke.py
├── .gitignore
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── batch.py
├── prompts.sample.jsonl
└── requirements.txt
```

## FAQ

**Is this production ready?**  
It works for my use case; review the code before relying on it.

**Why no framework?**  
The stdlib covers what this project needs.

## License

MIT. Do whatever you want.
