# exonware-xwjson (long version)

**Extended Binary JSON Format** — Single Version of Truth for All Format Conversions.

*This is the long version (full feature tour, examples, troubleshooting). Short overview: [README.md](README.md).*

---

**Company:** eXonware.com  
**Author:** eXonware Backend Team  
**Email:** connect@exonware.com  
**Version:** 0.0.1.0

---

## What is xwjson?

**xwjson** is an extended binary JSON format that serves as the **single version of truth** for all format conversions. It is a **separate library** that extends xwsystem serialization, **exactly like XWFormats**.

### The Problem We Solve

Modern applications require serialization solutions that:
- Use text formats — Slow JSON/YAML parsing for large files
- Lack reference support — No cross-references between data
- Lose format metadata — YAML anchors, XML namespaces lost in conversion
- No transaction support — No ACID guarantees for data operations
- Slow batch operations — Sequential processing of multiple files

### The xwjson Solution

- **Binary-first design** — MessagePack-based encoding (10x faster than JSON)
- **Lazy loading** — Defer parsing until access for better performance
- **Reference support** — All format-specific references ($ref JSON, @href XML, *anchor YAML)
- **xwnode integration** — Dependency graphs, graph operations, topological sort
- **xwschema integration** — Schema validation with fast compiled schemas
- **Format metadata preservation** — YAML anchors, XML namespaces, TOML tables preserved
- **Universal intermediate format** — Single source of truth for all conversions
- **Async-first architecture** — All operations async by default
- **Transaction support** — ACID guarantees with zero performance penalty
- **Smart batch operations** — Dependency-aware, parallel execution (4-5x faster)

---

## Quick Start

### Installation

```bash
# Install with all dependencies
pip install exonware-xwjson[full]

# Or minimal install (dependencies required separately)
pip install exonware-xwjson
```

### Basic Usage

```python
from exonware.xwjson import XWJSONSerializer

# Create serializer
serializer = XWJSONSerializer()

# Async (default, recommended, fastest)
data = await serializer.load_file_async("data.xwjson")
await serializer.save_file_async(data, "output.xwjson")

# Sync (wrapper, for compatibility)
data = serializer.load_file("data.xwjson")
serializer.save_file(data, "output.xwjson")
```

### Using the Facade API

```python
from exonware.xwjson import XWJSON

# Create XWJSON instance
xwjson = XWJSON()

# Save and load
await xwjson.save(data, "data.xwjson")
loaded = await xwjson.load("data.xwjson")

# Encode/decode to bytes
encoded = xwjson.encode(data)
decoded = xwjson.decode(encoded)
```

---

## Key Features

### 1. Binary-First Design

10x faster than JSON text serialization:

```python
from exonware.xwjson import XWJSONSerializer

serializer = XWJSONSerializer()
await serializer.save_file_async(data, "data.xwjson")  # Fast binary format
```

### 2. Lazy Loading

Defer parsing until access for better performance:

```python
# Lazy loading: parse only when accessed
data = await serializer.load_file_async("large_file.xwjson", lazy=True)
print(data["users"][0]["name"])  # Only this part is parsed
```

### 3. Reference Support

All format-specific references automatically resolved:

```python
# JSON $ref, XML @href, YAML *anchor all supported
data = await serializer.load_file_async("data_with_refs.xwjson")
# References automatically resolved
```

### 4. Transaction Support

ACID transactions with zero performance penalty:

```python
async with serializer.transaction():
    data = await serializer.load_file_async("data.xwjson")
    data["count"] += 1
    await serializer.save_file_async(data, "data.xwjson")
    # Commits automatically, or rolls back on error
```

### 5. Smart Batch Operations

Dependency-aware batch operations with parallel execution (4-5x faster):

```python
from exonware.xwjson.operations import XWJSONDataOperations

ops = XWJSONDataOperations()
await ops.batch_save(files, data_list)  # 4-5x faster than sequential
```

### 6. Format Conversion

Universal intermediate format for all conversions:

```python
# Convert between any formats via XWJSON
# JSON → XWJSON → YAML → XWJSON → XML
# All metadata preserved during conversion
```

---

## Documentation

### Usage Guides (see docs/ and docs/_archive/)

- **Basic Usage** — docs/_archive/GUIDE_BASIC_USAGE.md
- **Advanced Usage** — docs/_archive/GUIDE_ADVANCED_USAGE.md
- **Performance** — docs/_archive/GUIDE_PERFORMANCE.md
- **Format Conversion** — docs/_archive/GUIDE_FORMAT_CONVERSION.md
- **Schema Validation** — docs/_archive/GUIDE_SCHEMA_VALIDATION.md

### Examples

See `examples/` directory: basic_serialization, lazy_loading, references, transactions, batch_operations, format_conversion, schema_validation, performance, xwnode_integration.

### API Reference

- [REF_15_API.md](docs/REF_15_API.md) — Full API reference
- [REF_22_PROJECT.md](docs/REF_22_PROJECT.md) — Project status and milestones
- [GUIDE_01_USAGE.md](docs/GUIDE_01_USAGE.md) — Usage guide

---

## Performance

### Benchmarks

- **Serialization:** 10x faster than JSON text
- **Lazy loading:** Parse only when accessed
- **Batch operations:** 4-5x faster with parallel execution
- **Path operations:** Access specific data without loading entire file

See docs/_archive/GUIDE_PERFORMANCE.md for detailed benchmarks and optimization tips.

---

## Troubleshooting

### Common Issues

**Q: File not found error**  
A: Ensure the file path is correct and the file exists. Use absolute paths if needed.

**Q: Schema validation error**  
A: Check your schema definition and data structure. Ensure all required fields are present.

**Q: Performance issues with large files**  
A: Enable lazy loading and use path operations instead of loading entire files.

**Q: Reference resolution errors**  
A: Ensure all referenced files are accessible and references are correctly formatted.

### Getting Help

- Check the [documentation](docs/) for detailed guides
- See [examples](examples/) for usage patterns
- Report issues at: connect@exonware.com

---

## Innovation: Where does this package fit?

**Tier 2 — Significant innovation (novel combination)**

**xwjson — Extended Binary JSON with ACID + Lazy Loading**

Binary JSON (MessagePack-based) with 4-tier lazy loading, ACID transactions via WAL, dependency-aware batch operations, and universal reference support ($ref, @href, *anchors) across ALL formats.

JSON/YAML/MessagePack = no transactions; this has full WAL + rollback. Path-based atomic updates; hybrid parser (msgspec/orjson) per operation.

**Verdict:** This specific combination doesn't exist elsewhere. Part of the eXonware story — vertical integration across 20+ packages.

---

## License

MIT License

---

**Company:** eXonware.com  
**Author:** eXonware Backend Team  
**Email:** connect@exonware.com
