# rotate-secret

Seamless API key rotation for Secrets Proxy. Update 1Password, re-encrypt with age, deploy to scout, restart proxy, verify — all in one command.

**⚠️ DEFAULTS TO DRY-RUN MODE.** Pass `--apply` to execute.

## Installation

```bash
git clone https://github.com/krustybot/rotate-secret.git
cd rotate-secret
chmod +x rotate-secret
sudo ln -s "$(pwd)/rotate-secret" /usr/local/bin/rotate-secret
```

## Requirements

- `op` — [1Password CLI](https://developer.1password.com/docs/cli/get-started/)
- `age` — `brew install age` (macOS) or `apt install age` (Linux)
- `ssh` — for deploying to scout
- `tailscale` — or SSH access to `scout.fable-court.ts.net:2222`

## Usage

```bash
# See what would happen (dry run)
rotate-secret fireworks

# Actually do it
rotate-secret fireworks --apply

# With pre-pasted key
pbpaste | rotate-secret fireworks --stdin --apply
```

## Services

- `fireworks`, `github`, `huggingface`, `repliers`, `runpod`
- `elevenlabs`, `gemini`, `goplaces`, `openai`

## Configuration

Create `~/.config/rotate-secret/config.sh` to override defaults:

```bash
AGE_PUBKEY="age14ypvy9kly6hgfap3ydpfxcwxnu6qnwg5e08e0aet0ywtagwm5gtqt34a4e"
SCOUT_HOST="scout.fable-court.ts.net"
SCOUT_SSH_PORT="2222"
```

## Workflow

1. Generate new key in service console (keep tab open)
2. Run `rotate-secret <service> --apply`
3. Script updates 1Password, deploys, restarts, verifies
4. **After success**, revoke old key in console

## Related

- [Secrets Proxy](https://github.com/krustybot/secrets-proxy) — The tokenizing proxy this script manages
