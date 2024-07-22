# Choose Your Favorite String in Rust!

## Memory efficiency

| Type            | Crate                                      | Mutable | Clone    | Hash | Size[^1]         | SSO             |
| --------------- | ------------------------------------------ | ------- | -------- | ---- | ---------------- | --------------- |
| `String`        | std                                        | Yes     | O(n)     | O(n) | 24 bytes         | No              |
| `Box<str>`      | std                                        | No      | O(n)     | O(n) | 16 bytes + niche | No              |
| `Arc<str>`      | std                                        | No      | O(1)     | O(n) | 16 bytes + niche | No              |
| `FastStr`       | [faststr](https://docs.rs/faststr)         | No      | O(1)     | O(n) | 40 bytes + niche | 24 bytes[^2]    |
| `CompactString` | [compact_str](https://docs.rs/compact_str) | Yes     | O(n)     | O(n) | 24 bytes + niche | 23 bytes        |
| `SmolStr`       | [smol_str](https://docs.rs/smol_str)       | No      | O(1)     | O(n) | 24 bytes + niche | 22 bytes/WS[^3] |
| `Yarn`          | [byteyarn](https://docs.rs/byteyarn)       | No      | O(1)     | O(n) | 16 bytes + niche | 15 bytes        |
| `ArcStr`        | [arcstr](https://docs.rs/arcstr)           | No      | O(1)     | O(n) | 8 bytes + niche  | No              |
| `UStr`          | [ustr](https://docs.rs/ustr)               | No      | O(1)     | O(1) | 8 bytes + niche  | No              |
| `EcoString`     | [ecow](https://docs.rs/ecow)               | Yes     | O(1)[^4] | O(n) | 16 bytes         | 15 bytes        |

## Convention

| Type            | Crate                                      | From `String` | From `Box<str>` | From `Arc<str>` | From `&'static str` |
| --------------- | ------------------------------------------ | ------------- | --------------- | --------------- | ------------------- |
| `String`        | std                                        | -             | O(1)            | No              | O(n)                |
| `Box<str>`      | std                                        | O(n)          | -               | No              | O(n)                |
| `Arc<str>`      | std                                        | O(n)          | O(n)            | -               | O(n)                |
| `FastStr`       | [faststr](https://docs.rs/faststr)         | O(n)          | O(n)            | O(1)            | O(1)                |
| `CompactString` | [compact_str](https://docs.rs/compact_str) | O(1)          | O(1)            | No              | O(1)                |
| `SmolStr`       | [smol_str](https://docs.rs/smol_str)       | O(n)          | O(n)            | O(1)            | O(1)                |
| `Yarn`          | [byteyarn](https://docs.rs/byteyarn)       | O(n)          | O(1)            | No              | O(1)                |
| `ArcStr`        | [arcstr](https://docs.rs/arcstr)           | O(n)          | O(n)            | O(n)            | O(1)[^5]            |
| `UStr`          | [ustr](https://docs.rs/ustr)               | O(n)          | No              | No              | O(n)                |
| `EcoString`     | [ecow](https://docs.rs/ecow)               | O(n)          | No              | No              | O(n)                |

## Integration

| Type            | Crate                                      | no-std | MSRV | serde | bytes | rkyv |
| --------------- | ------------------------------------------ | ------ | ---- | ----- | ----- | ---- |
| `FastStr`       | [faststr](https://docs.rs/faststr)         | No     | 1.60 | Yes   | Yes   | No   |
| `CompactString` | [compact_str](https://docs.rs/compact_str) | Yes    | 1.60 | Yes   | Yes   | Yes  |
| `SmolStr`       | [smol_str](https://docs.rs/smol_str)       | Yes    | 1.60 | Yes   | No    | No   |
| `Yarn`          | [byteyarn](https://docs.rs/byteyarn)       | No     | 1.71 | No    | No    | No   |
| `ArcStr`        | [arcstr](https://docs.rs/arcstr)           | Yes    | 1.57 | Yes   | No    | No   |
| `UStr`          | [ustr](https://docs.rs/ustr)               | No     | 1.60 | Yes   | No    | No   |
| `EcoString`     | [ecow](https://docs.rs/ecow)               | Yes    | 1.65 | Yes   | No    | No   |

## Audit

| Type            | Crate                                      | Unsafe    | Dependencies[^6] | License                   |
| --------------- | ------------------------------------------ | --------- | ---------------- | ------------------------- |
| `FastStr`       | [faststr](https://docs.rs/faststr)         | UTF-8[^7] | 2                | MIT/Apache                |
| `CompactString` | [compact_str](https://docs.rs/compact_str) | Yes       | 6                | MIT                       |
| `SmolStr`       | [smol_str](https://docs.rs/smol_str)       | Yes       | 0                | MIT/Apache                |
| `Yarn`          | [byteyarn](https://docs.rs/byteyarn)       | Yes       | 1                | Apache 2.0                |
| `ArcStr`        | [arcstr](https://docs.rs/arcstr)           | Yes       | 0                | Apache-2.0 OR MIT OR Zlib |
| `UStr`          | [ustr](https://docs.rs/ustr)               | Yes       | 4                | BSD-2-Clause-Patent       |
| `EcoString`     | [ecow](https://docs.rs/ecow)               | Yes       | 0                | MIT/Apache                |

[^1]: based on x86_64
[^2]: not stable
[^3]: SSO is also available for consecutive newlines and spaces
[^4]: copy on write
[^5]: only available for literal
[^6]: optional or dev dependencies not counted
[^7]: only used in UTF-8 validation