# What is the difference between 'cargo update' vs 'cargo update -p h2' command？ 

### Problem

When I exec `cargo update` in my project, the `h2` an be upgraded to the latest version：**h2 v0.3.10 -> v0.3.17**.
However, when I upgrade the `h2` crates  individually and execute the `cargo update -p h2` command, I can only upgrade from : **h2 v0.3.10 -> v0.3.12**.

What is the reason for this？I expect to upgrade to 0.3.17 by executing ` cargo update - p h2`, but in reality, it did not meet my expectations.

---

The part cargo tree output:
```diff
│...
└── actix-web v4.3.1
    ├── actix-codec v0.5.0
    │   ├── bitflags v1.3.2
    │   ├── bytes v1.2.1
    │   ├── futures-core v0.3.17
    │   ├── futures-sink v0.3.17
    │   ├── log v0.4.17
    │   │   └── cfg-if v1.0.0
    │   ├── memchr v2.4.1
    │   ├── pin-project-lite v0.2.7
    │   ├── tokio v1.26.0
    │   │   ├── bytes v1.2.1
    │   │   ├── libc v0.2.141
    │   │   ├── memchr v2.4.1
    │   │   ├── mio v0.8.4
    │   │   │   ├── libc v0.2.141
    │   │   │   └── log v0.4.17 (*)
    │   │   ├── parking_lot v0.12.1
    │   │   │   ├── lock_api v0.4.7
    │   │   │   │   └── scopeguard v1.1.0
    │   │   │   │   [build-dependencies]
    │   │   │   │   └── autocfg v1.1.0
    │   │   │   └── parking_lot_core v0.9.3
    │   │   │       ├── cfg-if v1.0.0
    │   │   │       ├── libc v0.2.141
    │   │   │       └── smallvec v1.7.0
    │   │   ├── pin-project-lite v0.2.7
    │   │   ├── signal-hook-registry v1.4.0
    │   │   │   └── libc v0.2.141
    │   │   └── socket2 v0.4.7
    │   │       └── libc v0.2.141
    │   │   [build-dependencies]
    │   │   └── autocfg v1.1.0
    │   └── tokio-util v0.7.0
    │       ├── bytes v1.2.1
    │       ├── futures-core v0.3.17
    │       ├── futures-sink v0.3.17
    │       ├── log v0.4.17 (*)
    │       ├── pin-project-lite v0.2.7
    │       └── tokio v1.26.0 (*)
    ├── actix-http v3.3.1
    │   ├── actix-codec v0.5.0 (*)
    │   ├── actix-rt v2.6.0
    │   │   ├── futures-core v0.3.17
    │   │   └── tokio v1.26.0 (*)
    │   ├── actix-service v2.0.2
    │   │   ├── futures-core v0.3.17
    │   │   ├── paste v1.0.6 (proc-macro)
    │   │   └── pin-project-lite v0.2.7
    │   ├── actix-utils v3.0.0
    │   │   ├── local-waker v0.1.2
    │   │   └── pin-project-lite v0.2.7
    │   ├── ahash v0.8.3
    │   │   ├── cfg-if v1.0.0
    │   │   ├── getrandom v0.2.9
    │   │   │   ├── cfg-if v1.0.0
    │   │   │   └── libc v0.2.141
    │   │   └── once_cell v1.13.1
    │   │   [build-dependencies]
    │   │   └── version_check v0.9.4
    │   ├── base64 v0.21.0
    │   ├── bitflags v1.3.2
    │   ├── brotli v3.3.3
    │   │   ├── alloc-no-stdlib v2.0.3
    │   │   ├── alloc-stdlib v0.2.1
    │   │   │   └── alloc-no-stdlib v2.0.3
    │   │   └── brotli-decompressor v2.3.2
    │   │       ├── alloc-no-stdlib v2.0.3
    │   │       └── alloc-stdlib v0.2.1 (*)
    │   ├── bytes v1.2.1
    │   ├── bytestring v1.0.0
    │   │   └── bytes v1.2.1
    │   ├── derive_more v0.99.16 (proc-macro)
    │   │   ├── convert_case v0.4.0
    │   │   ├── proc-macro2 v1.0.43
    │   │   │   └── unicode-ident v1.0.3
    │   │   ├── quote v1.0.10
    │   │   │   └── proc-macro2 v1.0.43 (*)
    │   │   └── syn v1.0.99
    │   │       ├── proc-macro2 v1.0.43 (*)
    │   │       ├── quote v1.0.10 (*)
    │   │       └── unicode-ident v1.0.3
    │   │   [build-dependencies]
    │   │   └── rustc_version v0.3.3
    │   │       └── semver v0.11.0
    │   │           └── semver-parser v0.10.2
    │   │               └── pest v2.1.3
    │   │                   └── ucd-trie v0.1.3
    │   ├── encoding_rs v0.8.29
    │   │   └── cfg-if v1.0.0
    │   ├── flate2 v1.0.22
    │   │   ├── cfg-if v1.0.0
    │   │   ├── crc32fast v1.2.1
    │   │   │   └── cfg-if v1.0.0
    │   │   ├── libc v0.2.141
    │   │   └── miniz_oxide v0.4.4
    │   │       └── adler v1.0.2
    │   │       [build-dependencies]
    │   │       └── autocfg v1.1.0
    │   ├── futures-core v0.3.17
+   │   ├── h2 v0.3.10
    │   │   ├── bytes v1.2.1
    │   │   ├── fnv v1.0.7
    │   │   ├── futures-core v0.3.17
    │   │   ├── futures-sink v0.3.17
    │   │   ├── futures-util v0.3.17
    │   │   │   ├── futures-core v0.3.17
    │   │   │   ├── futures-task v0.3.17
    │   │   │   ├── pin-project-lite v0.2.7
    │   │   │   └── pin-utils v0.1.0
    │   │   │   [build-dependencies]
    │   │   │   └── autocfg v1.1.0
    │   │   ├── http v0.2.9
    │   │   │   ├── bytes v1.2.1
    │   │   │   ├── fnv v1.0.7
    │   │   │   └── itoa v1.0.1
    │   │   ├── indexmap v1.7.0
    │   │   │   └── hashbrown v0.11.2
    │   │   │   [build-dependencies]
    │   │   │   └── autocfg v1.1.0
    │   │   ├── slab v0.4.5
    │   │   ├── tokio v1.26.0 (*)
    │   │   ├── tokio-util v0.6.9
    │   │   │   ├── bytes v1.2.1
    │   │   │   ├── futures-core v0.3.17
    │   │   │   ├── futures-sink v0.3.17
    │   │   │   ├── log v0.4.17 (*)
    │   │   │   ├── pin-project-lite v0.2.7
    │   │   │   └── tokio v1.26.0 (*)
    │   │   └── tracing v0.1.35
    │   │       ├── cfg-if v1.0.0
    │   │       ├── log v0.4.17 (*)
    │   │       ├── pin-project-lite v0.2.7
    │   │       └── tracing-core v0.1.30
    │   │           └── once_cell v1.13.1
    │   ├── http v0.2.9 (*)
    │   ├── httparse v1.8.0
    │   ├── httpdate v1.0.2
    │   ├── itoa v1.0.1
    │   ├── language-tags v0.3.2
    │   ├── local-channel v0.1.2
    │   │   ├── futures-core v0.3.17
    │   │   ├── futures-sink v0.3.17
    │   │   ├── futures-util v0.3.17 (*)
    │   │   └── local-waker v0.1.2
    │   ├── mime v0.3.16
    │   ├── percent-encoding v2.1.0
    │   ├── pin-project-lite v0.2.7
    │   ├── rand v0.8.4
    │   │   ├── libc v0.2.141
    │   │   ├── rand_chacha v0.3.1
    │   │   │   ├── ppv-lite86 v0.2.15
    │   │   │   └── rand_core v0.6.3
    │   │   │       └── getrandom v0.2.9 (*)
    │   │   └── rand_core v0.6.3 (*)
    │   ├── sha1 v0.10.4
    │   │   ├── cfg-if v1.0.0
    │   │   ├── cpufeatures v0.2.1
    │   │   └── digest v0.10.3
    │   │       ├── block-buffer v0.10.2
    │   │       │   └── generic-array v0.14.4
    │   │       │       └── typenum v1.14.0
    │   │       │       [build-dependencies]
    │   │       │       └── version_check v0.9.4
    │   │       └── crypto-common v0.1.3
    │   │           ├── generic-array v0.14.4 (*)
    │   │           └── typenum v1.14.0
    │   ├── smallvec v1.7.0
    │   ├── tokio v1.26.0 (*)
    │   ├── tokio-util v0.7.0 (*)
    │   ├── tracing v0.1.35 (*)
    │   └── zstd v0.12.3+zstd.1.5.2
    │       └── zstd-safe v6.0.5+zstd.1.5.4
    │           ├── libc v0.2.141
    │           └── zstd-sys v2.0.8+zstd.1.5.5
    │               └── libc v0.2.141
    │               [build-dependencies]
    │               ├── cc v1.0.72
    │               │   └── jobserver v0.1.24
    │               │       └── libc v0.2.141
    │               └── pkg-config v0.3.25
    ├── actix-macros v0.2.3 (proc-macro)
    │   ├── quote v1.0.10 (*)
    │   └── syn v1.0.99 (*)
    ├── actix-router v0.5.0
    │   ├── bytestring v1.0.0 (*)
    │   ├── firestorm v0.5.0
    │   ├── http v0.2.9 (*)
    │   ├── log v0.4.17 (*)
    │   ├── regex v1.7.1
    │   │   ├── aho-corasick v0.7.18
    │   │   │   └── memchr v2.4.1
    │   │   ├── memchr v2.4.1
    │   │   └── regex-syntax v0.6.28
    │   └── serde v1.0.147
    ├── actix-rt v2.6.0 (*)
    ├── actix-server v2.0.0
    │   ├── actix-rt v2.6.0 (*)
    │   ├── actix-service v2.0.2 (*)
    │   ├── actix-utils v3.0.0 (*)
    │   ├── futures-core v0.3.17
    │   ├── futures-util v0.3.17 (*)
    │   ├── log v0.4.17 (*)
    │   ├── mio v0.8.4 (*)
    │   ├── num_cpus v1.13.0
    │   │   └── libc v0.2.141
    │   ├── socket2 v0.4.7 (*)
    │   └── tokio v1.26.0 (*)
    ├── actix-service v2.0.2 (*)
    ├── actix-utils v3.0.0 (*)
    ├── actix-web-codegen v4.2.0 (proc-macro)
    │   ├── actix-router v0.5.0 (*)
    │   ├── proc-macro2 v1.0.43 (*)
    │   ├── quote v1.0.10 (*)
    │   └── syn v1.0.99 (*)
    ├── ahash v0.7.6
    │   ├── getrandom v0.2.9 (*)
    │   └── once_cell v1.13.1
    │   [build-dependencies]
    │   └── version_check v0.9.4
    ├── bytes v1.2.1
    ├── bytestring v1.0.0 (*)
    ├── cfg-if v1.0.0
    ├── cookie v0.16.0
    │   ├── percent-encoding v2.1.0
    │   └── time v0.3.14
    │       ├── itoa v1.0.1
    │       ├── libc v0.2.141
    │       ├── num_threads v0.1.3
    │       │   └── libc v0.2.141
    │       └── time-macros v0.2.4 (proc-macro)
    │   [build-dependencies]
    │   └── version_check v0.9.4
    ├── derive_more v0.99.16 (proc-macro) (*)
    ├── encoding_rs v0.8.29 (*)
    ├── futures-core v0.3.17
    ├── futures-util v0.3.17 (*)
    ├── http v0.2.9 (*)
    ├── itoa v1.0.1
    ├── language-tags v0.3.2
    ├── log v0.4.17 (*)
    ├── mime v0.3.16
    ├── once_cell v1.13.1
    ├── pin-project-lite v0.2.7
    ├── regex v1.7.1 (*)
    ├── serde v1.0.147
    ├── serde_json v1.0.70
    │   ├── itoa v0.4.8
    │   ├── ryu v1.0.5
    │   └── serde v1.0.147
    ├── serde_urlencoded v0.7.1
    │   ├── form_urlencoded v1.0.1
    │   │   ├── matches v0.1.9
    │   │   └── percent-encoding v2.1.0
    │   ├── itoa v1.0.1
    │   ├── ryu v1.0.5
    │   └── serde v1.0.147
    ├── smallvec v1.7.0
    ├── socket2 v0.4.7 (*)
    ├── time v0.3.14 (*)
    └── url v2.2.2
        ├── form_urlencoded v1.0.1 (*)
        ├── idna v0.2.3
        │   ├── matches v0.1.9
        │   ├── unicode-bidi v0.3.7
        │   └── unicode-normalization v0.1.19
        │       └── tinyvec v1.5.1
        │           └── tinyvec_macros v0.1.0
        ├── matches v0.1.9
        └── percent-encoding v2.1.0
│...
```

As of April 14, 2023, the latest version of H2 is [h2:0.3.17](https://crates.io/crates/h2/0.3.17)




### Steps

_No response_

### Possible Solution(s)

_No response_

### Notes

_No response_

### Version

```text
> cargo version --verbose 
cargo 1.68.2 (6feb7c9cf 2023-03-26)
release: 1.68.2
commit-hash: 6feb7c9cfc0c5604732dba75e4c3b2dbea38e8d8
commit-date: 2023-03-26
host: x86_64-apple-darwin
libgit2: 1.5.0 (sys:0.16.0 vendored)
libcurl: 7.86.0 (sys:0.4.59+curl-7.86.0 system ssl:(SecureTransport) LibreSSL/3.3.6)
os: Mac OS 13.2.1 [64-bit]
```

