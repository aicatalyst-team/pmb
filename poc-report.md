# PoC Report: PMB (Personal Memory Brain)

## Executive Summary

PMB was successfully deployed as a containerized dashboard service on OpenShift. The local-first persistent memory system for AI agents features a built-in web dashboard with event timeline, entity graph, and recall debugger. All four validation scenarios passed, confirming that the dashboard server, workspace initialization, and API endpoints function correctly in a container environment.

**Result: SUCCESS** - All 4/4 test scenarios passed.

## Project Analysis

| Attribute | Value |
|-----------|-------|
| **Project** | PMB (Personal Memory Brain) |
| **Source** | https://github.com/oleksiijko/pmb |
| **Fork** | https://github.com/aicatalyst-team/pmb |
| **License** | Apache-2.0 |
| **Language** | Python |
| **Category** | RAG / Memory / MCP |
| **Stars** | 61 |

### Key Technologies
- sentence-transformers (embedding)
- LanceDB (vector search)
- BM25 (text ranking)
- FastMCP (MCP protocol server)
- stdlib HTTP server (dashboard)

## Test Results

| Test | Result | Latency | Output |
|------|--------|---------|--------|
| Dashboard root (/) | PASS | 20ms | Full HTML dashboard with PMB title |
| API stats (/api/stats) | PASS | 10ms | Workspace stats JSON with graph metrics |
| API events (/api/events) | PASS | <1ms | Empty array (new workspace) |
| API entities (/api/entities) | PASS | <1ms | Empty array (new workspace) |

## Build Notes

- Used CPU-only PyTorch to avoid 2GB+ CUDA dependencies
- Source ownership fix needed for OpenShift build pod (USER 0 chown before pip install)
- 3 build retries total (editable install permission, source ownership, OOM from CUDA)

## Artifact Links
- **Fork**: https://github.com/aicatalyst-team/pmb
- **Image**: quay.io/aicatalyst/pmb-dashboard:latest
- **Manifests**: [autopoc-artifacts branch](https://github.com/aicatalyst-team/pmb/tree/autopoc-artifacts/kubernetes)
