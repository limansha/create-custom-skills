# Shared agent skills

Skills in this repository follow the Agent Skills layout and can be installed from GitHub with the Skills CLI.

## Available skills

- `python-code-review`: reviews Python code for correctness, security, reliability, maintainability, and test gaps.

## Install for supported agents

The Skills CLI supports multiple coding assistants. Install this repository with:

```bash
npx skills add https://github.com/limansha/create-custom-skills
```

The CLI discovers `SKILL.md` files under `skills/` and installs them in the appropriate location for the selected or detected agent. The skill is not limited to OpenCode.

You can also use the repository owner and name instead of the full URL:

```bash
npx skills add limansha/create-custom-skills
```

Use the owner and repository name for your own fork or organization.

## Layout

```text
skills/
└── python-code-review/
    ├── SKILL.md
    └── references/
```

Each published skill must have a matching lowercase hyphenated directory and `SKILL.md` file.
