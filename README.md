# Shared agent skills

Skills in this repository follow the Agent Skills layout and can be installed from GitHub with the Skills CLI.

## Available skills

- `python-code-review`: reviews Python code for correctness, security, reliability, maintainability, and test gaps.

## Install

Install the repository with:

```bash
npx skills add https://github.com/limansha/create-custom-skills
```

The CLI discovers `SKILL.md` files under `skills/` and installs them for supported agents, including OpenCode.

To use the source directly with OpenCode, point the project configuration at the skills directory:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "skills": {
    "paths": ["./skills"]
  }
}
```

## Layout

```text
skills/
└── python-code-review/
    ├── SKILL.md
    └── references/
```

Each published skill must have a matching lowercase hyphenated directory and `SKILL.md` file.
