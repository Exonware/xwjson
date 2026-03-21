# XWJSON Test Suite

## Overview

Comprehensive test suite for XWJSON following GUIDE_TEST.md 4-layer hierarchical structure.

## Test Structure

```
tests/
├── 0.core/                    # Core tests (20% for 80% value)
│   ├── test_import.py         # Import and basic functionality
│   └── test_basic_encoding.py # Basic encode/decode round-trip
├── 1.unit/                    # Unit tests (component tests)
│   ├── formats_tests/
│   │   └── binary_tests/
│   │       └── xwjson_tests/
│   │           ├── test_encoder.py      # Encoder/decoder tests
│   │           ├── test_serializer.py  # Serializer tests
│   │           ├── test_references.py   # Reference resolution
│   │           ├── test_lazy.py         # Lazy loading
│   │           └── test_dependency_graph.py # Dependency graph
│   └── operations_tests/
│       └── test_xwjson_ops.py # Data operations
├── 2.integration/            # Integration tests (scenario tests)
│   └── scenarios/
│       ├── test_stress_large_files.py      # Large file handling
│       ├── test_stress_concurrent.py       # Concurrent operations
│       ├── test_stress_memory.py           # Memory efficiency
│       ├── test_stress_xwnode_caching.py   # xwnode caching
│       ├── test_stress_xwnode_indexing.py  # xwnode indexing
│       ├── test_stress_transactions.py     # Transaction stress
│       ├── test_stress_queries.py          # Query stress
│       ├── test_stress_batch_operations.py # Batch operations
│       ├── test_stress_references.py       # Reference stress
│       ├── test_stress_schema_validation.py # Schema validation
│       ├── test_stress_lazy_loading.py     # Lazy loading stress
│       └── test_xwnode_integration.py      # xwnode integration
└── 3.advance/                 # Advance tests (production excellence)
    ├── test_security.py       # Security excellence (Priority #1)
    ├── test_usability.py      # Usability excellence (Priority #2)
    ├── test_maintainability.py # Maintainability excellence (Priority #3)
    ├── test_performance.py    # Performance excellence (Priority #4)
    └── test_extensibility.py # Extensibility excellence (Priority #5)
```

## Running Tests

### Run All Tests
```bash
python tests/runner.py
```

### Run by Layer
```bash
# Core tests
pytest tests/0.core/ -v

# Unit tests
pytest tests/1.unit/ -v

# Integration tests
pytest tests/2.integration/ -v

# Advance tests
pytest tests/3.advance/ -v
```

### Run by Marker
```bash
# Performance tests
pytest -m xwjson_performance -v

# Security tests
pytest -m xwjson_security -v

# Lazy loading tests
pytest -m xwjson_lazy -v

# Reference tests
pytest -m xwjson_references -v
```

## Test Coverage

### Core Tests (0.core)
- ✅ Import and instantiation
- ✅ Basic encode/decode round-trip
- ✅ Various data types
- ✅ Metadata support
- ✅ Magic bytes validation
- ✅ File operations

### Unit Tests (1.unit)
- ✅ Encoder/decoder (hybrid parser: orjson/msgspec)
- ✅ Serializer (all methods)
- ✅ Reference resolution (JSON, XML, YAML, TOML)
- ✅ Lazy loading (file, serialization, node, reference)
- ✅ Dependency graph (conflicts, topological sort)
- ✅ Data operations (read, write, update, delete, query)

### Integration Tests (2.integration)
- ✅ Large file handling (10GB+)
- ✅ Concurrent operations (1000+ concurrent)
- ✅ Memory efficiency (lazy loading, streaming)
- ✅ xwnode caching (LRU_CACHE strategy)
- ✅ xwnode indexing (HASH_MAP strategy)
- ✅ Transactions (ACID, concurrent, rollback)
- ✅ Queries (JSONPath, SQL, complex queries)
- ✅ Batch operations (dependency resolution, parallel execution)
- ✅ Reference resolution (circular detection, caching)
- ✅ Schema validation (compiled schemas, performance)
- ✅ Lazy loading (memory efficiency, large files)

### Advance Tests (3.advance)
- ✅ Security (path traversal, input validation, circular detection)
- ✅ Usability (API intuitiveness, error messages)
- ✅ Maintainability (code quality, modularity, type hints)
- ✅ Performance (encoding/decoding speed, query performance)
- ✅ Extensibility (plugin system, subclassing)

## Stress Tests

All stress tests are designed to push XWJSON to its limits:

- **Large Files**: 10GB+ files, 100000+ items
- **Concurrent Operations**: 1000+ concurrent reads/writes
- **Memory Efficiency**: Lazy loading, streaming, memory-mapped I/O
- **Performance**: Encoding/decoding speed, query performance, batch operations
- **xwnode Integration**: Caching (LRU_CACHE), indexing (HASH_MAP), paging

## xwnode Integration

Tests leverage xwnode strategies for optimal performance:

- **Caching**: `NodeMode.LRU_CACHE` for query result caching (10-50x faster)
- **Indexing**: `NodeMode.HASH_MAP` for O(1) lookups
- **Paging**: Index-based paging with xwnode hash maps
- **Graph Operations**: Dependency resolution using xwnode graph strategies

## Test Markers

- `@pytest.mark.xwjson_core` - Core tests
- `@pytest.mark.xwjson_unit` - Unit tests
- `@pytest.mark.xwjson_integration` - Integration tests
- `@pytest.mark.xwjson_advance` - Advance tests
- `@pytest.mark.xwjson_performance` - Performance tests
- `@pytest.mark.xwjson_security` - Security tests
- `@pytest.mark.xwjson_lazy` - Lazy loading tests
- `@pytest.mark.xwjson_references` - Reference tests
- `@pytest.mark.xwjson_serialization` - Serialization tests

## Requirements

Tests require:
- `exonware-xwnode` (for caching, indexing, paging)
- `exonware-xwschema` (for schema validation)
- `exonware-xwquery` (optional, for advanced queries)
- `pytest` and `pytest-asyncio`

Install with:
```bash
pip install exonware-xwjson[full]
```
