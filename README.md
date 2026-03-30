# xwjson

**Binary JSON for real workloads.** MessagePack-based `.xwjson` is ~10x faster than text JSON on typical benchmarks, keeps schema and format metadata, supports lazy loading and references (`$ref`, `@href`, `*anchor`), and underpins conversions and transactions across the stack.

*Longer tour, examples, and troubleshooting: [README_LONG.md](README_LONG.md).*

**Company:** eXonware.com · **Author:** eXonware Backend Team · **Email:** connect@exonware.com  

[![Status](https://img.shields.io/badge/status-beta-blue.svg)](https://exonware.com)
[![Python](https://img.shields.io/badge/python-3.12%2B-blue.svg)](https://www.python.org)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

---

## Install

```bash
pip install exonware-xwjson
# Full (optional)
pip install exonware-xwjson[full]
```

---

## Quick start

```python
from exonware.xwjson import XWJSONSerializer

serializer = XWJSONSerializer()
# Async (recommended)
data = await serializer.load_file_async("data.xwjson")
await serializer.save_file_async(data, "output.xwjson")
# Sync
data = serializer.load_file("data.xwjson")
serializer.save_file(data, "output.xwjson")
```

See [docs/](docs/) for REF_*, guides, and examples.

---

## What you get

| Area | What's in it |
|------|----------------|
| **Binary** | MessagePack-based encoding; faster than text JSON for typical loads. |
| **Lazy** | Parse on access when you ask for it. |
| **References** | `$ref`, `@href`, `*anchor` preserved and resolved. |
| **Integration** | xwnode, xwschema; format metadata carried through. |
| **Transactions** | ACID-style batches with dependency-aware parallel work. |

---

## Docs and tests

- **Start:** [docs/INDEX.md](docs/INDEX.md) or [docs/](docs/).
- **Guides:** Basic/advanced usage, performance, conversion, schema validation under `docs/` when present.
- **Tests:** From repo root, follow this package's runner or pytest layout.

---

## License and links

MIT - see [LICENSE](LICENSE). **Homepage:** https://exonware.com · **Repository:** https://github.com/exonware/xwjson  
Version: 0.9.0.8 | Updated: 30-Mar-2026

*Built with ❤️ by eXonware.com - Revolutionizing Python Development Since 2025*
