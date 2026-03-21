# xwjson

**Extended binary JSON.** MessagePack-based intermediate format that is ~10x faster than text JSON, preserves schema/format metadata, supports lazy loading and references ($ref, @href, *anchor), and powers conversions and transactions across the stack.

*Full feature tour, examples, and troubleshooting: [README_LONG.md](README_LONG.md).*

**Company:** eXonware.com · **Author:** eXonware Backend Team · **Email:** connect@exonware.com  
**Version:** See [version.py](src/exonware/xwjson/version.py) or PyPI. · **Updated:** See [version.py](src/exonware/xwjson/version.py) (`__date__`)

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
| **Binary** | MessagePack-based encoding; faster than text JSON. |
| **Lazy** | Defer parsing until access. |
| **References** | $ref, @href, *anchor preserved and resolved. |
| **Integration** | xwnode, xwschema; format metadata preserved. |
| **Transactions** | ACID; batch operations with dependency-aware parallel execution. |

---

## Docs and tests

- **Start:** [docs/INDEX.md](docs/INDEX.md) or [docs/](docs/).
- **Guides:** Basic/Advanced usage, Performance, Format conversion, Schema validation when present under docs/.
- **Tests:** Run from project root per project layout.

---

## License and links

MIT — see [LICENSE](LICENSE). **Homepage:** https://exonware.com · **Repository:** https://github.com/exonware/xwjson  

Contributing → CONTRIBUTING.md · Security → SECURITY.md (when present).

*Built with ❤️ by eXonware.com - Revolutionizing Python Development Since 2025*
