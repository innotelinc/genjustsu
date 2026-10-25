# TEIN AI in the Innotel Platform Stack

**Role: CodeOps** — Open-source AI workflows, built from composable nodes.

Part of the [Innotel Platform Stack](https://github.com/innotelinc/innotel-platform-stack).
The canonical definition of the stack, its shared layers and their owners lives
there; this file records only what TEIN AI does inside it.

## Boundaries

### Owns

- the workflow editor and runtime
- the node library
- workflow import and export

### Consumes

- an OpenAI-compatible model gateway
- Cerulean (Authentik SSO, DNS, TLS)
- NPM Edge (public host)

### Does not own

- the model providers
- identity (Authentik)
- secrets (Cerulean Vault)

## Service map

| Component | Technology | Job |
| --- | --- | --- |
| TEIN AI | Node.js / TypeScript | Open-source AI workflows, built from composable nodes. |
| Identity | Cerulean Authentik | Sign-in and role claims, where the repo has a UI |
| Secrets | Cerulean Vault (KV v2) | Production credentials, referenced as `vault://` |
| Trust | Cerulean | DNS, TLS and the public hostname |
| Edge | NPM Edge | The public route in front of the service |

## In the ecosystem

- **Identity** comes from Cerulean Authentik; this repo holds no second account
  table and no password of its own.
- **Secrets** come from Cerulean Vault. `.env` is local only and is never
  committed; a `vault://` reference is resolved by the deployment.
- **Trust and edge** are Cerulean's and NPM Edge's. This repo does not write DNS
  records or call the NPM API directly.
- **Storage, billing and telephony** belong to ONYX, Magnate and Zeus
  respectively; TEIN AI consumes them only where the boundaries above say
  so.

## See also

- [README](../README.md)
- [Innotel Platform Stack](https://github.com/innotelinc/innotel-platform-stack)
