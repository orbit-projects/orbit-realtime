# Orbit Realtime: architecture and boundaries

## Responsibility

`orbit-realtime` currently provides bounded Server-Sent Events framing over Orbit Core's native
ASGI streaming response. It does not add a web framework or a second ASGI server. It supports
Python 3.11 through 3.14 and is pre-alpha.

```bash
python -m pip install orbit-realtime
```

## Declared dependencies

The following dependency declarations come from the checked-in manifests. Optional groups and development dependencies are called out separately.

### `pyproject.toml`
- `orbit-core>=0.1.0a1,<0.2`
- Optional `dev` group: `pytest>=8,<10`, `pytest-asyncio>=0.24,<2`, `ruff>=0.8,<1`, `mypy>=1.13,<2`.

Declared dependencies do not mean that optional providers or services are bundled with this package.

## Implementation layout

Representative implementation files in this checkout:

- `src/orbit_realtime/__init__.py`
- `src/orbit_realtime/sse.py`

## Public contract and scope

The README does not contain a separately headed architecture section. Its responsibility statement above and the public source files define the implemented scope; this guide adds no behavior beyond that description.

## Boundary rules

Keep provider SDKs, credentials, transports, and provider-specific error translation in provider adapters. Keep reusable capability contracts in the matching capability package and lifecycle orchestration in Core. Apply the relevant layer for this repository and preserve the dependency direction shown above.


## Language implementations

The Python package integrates with Orbit Core's native ASGI response. The separately installable [Go implementation](https://github.com/orbit-projects/orbit-realtime-go) targets `net/http`, and [Rust implementation](https://github.com/orbit-projects/orbit-realtime-rust) implements `http-body`. Both use pull/write backpressure and bounded SSE frames without introducing a cross-process protocol. Provider-specific event sources and application authorization remain owned by the application or separately layered capability packages.
