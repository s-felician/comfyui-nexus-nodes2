# Public ComfyUI node handoff slot 2

This is a **reusable delivery repository**, not permanently an OpenAI-API-specific repository. Future handoffs may use this same slot for a different custom node package. Always install by a reviewed **fixed commit SHA** and do not update an installed pack to a different payload.

## Current payload (2026-10-14)

A minimal compatibility patch of the existing ComfyUI custom nodes from **[hekmon/comfyui-openai-api](https://github.com/hekmon/comfyui-openai-api)**, pinned to upstream commit `efb68c42291ae77df665423e02d6885a3f556bd1` (package 2.0.1).

The original author is **Edouard Hur**. The included `LICENSE` contains the unchanged original **MIT** copyright and permission notice. This public handoff repository is not affiliated with or endorsed by the upstream author.

**Only two upstream files are modified:**
- `pyproject.toml`: fixes the invalid dependency specifier `openai>=2.7.1<3.0.0` to `openai>=2.7.1,<3.0.0`.
- `completions.py`: adds a conservative no-retry guard rejecting zero/multiple choices, non-`stop` finish, missing/empty assistant message, and refusal before using an incomplete VLM response.

All other runtime files, including the upstream `LICENSE` and `requirements.txt`, are byte-for-byte unchanged from the pinned upstream commit. The `requirements.txt` remains upstream's **unbounded** requirements, so an automatic dependency installation can affect existing packages. Check the running ComfyUI environment and get explicit approval for any Python dependency changes; do not run a broad repair/update.

## Installation notes

This package uses the **ComfyUI V3 custom-node API** and needs a compatible ComfyUI core plus `openai>=2.7.1,<3.0.0`. The original client input includes a generic public API default. **Explicitly configure and verify a permitted local endpoint before sending any image**, with no automatic cloud fallback. Never commit API keys or private endpoint URLs to this public repository.

Use Artokun MCP `install_custom_node` with `source:"git"`, a **fixed commit SHA** and ComfyUI-Manager permissions. Publishing files is **not authorization** to install, pip-upgrade, restart, send VLM requests, or render. Confirm `OAIAPI_Client` and `OAIAPI_ChatCompletion` actually appear in `/object_info` after a separately approved restart.

## Runtime SHA-256

```text
a5065dd94b43a3160ab4cd2b551f8bde398df119548306df5c3e9df2f1af26b9  LICENSE
d6c23025e95477720bc4f4cd44bffbb4c0b3c70402eeab21718fa2e5cd1e1cb3  __init__.py
8457fc45c7752e9521a2f524b2b54dc0afb7771ddd7dc76b067a444668a27f4d  client.py
4a83d8bde2a4e37ce785c25fba9fdae7c3986b0faf0dd8decf330fa953c74a67  completions.py
ce4d883be9f341e37c37ab962928c9c1926d2ab5b43c30349f6d9fb6e2ed5f52  iotypes.py
5a584c32b82a18202b15c7c4d4efa076c49e5a462189ec2348cbc9f655592976  options.py
c0a1ab0aa08038ac69b476170f3ba823af28ec98fd6254df2a9aba035a0c1f17  pyproject.toml
11bc44db6d74c415455400d3d3fdd35e2efeed1b45afe24df9b09d867e2058b6  requirements.txt
```
