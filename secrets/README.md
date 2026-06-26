# secrets/

Local-only credentials. **Nothing real here is ever committed.**

`.gitignore` tracks only this `README.md` and `*.example` files; everything else in this folder
(`keys.env`, etc.) is ignored and stays on your machine.

## Use
1. `cp keys.env.example keys.env`
2. Put **real** keys in `keys.env` (gitignored).
3. Load before running tools that need them, e.g. a model router:
   - bash/git-bash: `set -a; source secrets/keys.env; set +a`

## Rules
- Never paste a key into chat, a tracked file, or a commit. If one leaks, **rotate it immediately**.
- See [../SECURITY.md](../SECURITY.md).
