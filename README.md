<img src="assets/logo.png" width="112" height="112" alt="Blyx penguin matching an ordered chain of release tags to an applied log.">

# VersionChain

Validate an applied migration log against a strictly increasing release manifest. This Blyx library is part of the databases and migrations collection.

A version number can match even when a previous migration changed. Check the applied prefix and recorded fingerprints before planning the next step. [Flyway, schema history table](https://documentation.red-gate.com/flyway/flyway-concepts/migrations/flyway-schema-history-table)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-versionchain.git
cd blyx-versionchain
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-versionchain) · [Package page](https://www.blyx-lang.space/packages/versionchain) · [Handbook](https://doc.blyx-lang.space/guide/bittern)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-versionchain.git vendor/versionchain
```

```blyx
use vendor::versionchain::versionchain;

fn main() {
    let available = [1, 4, 8];
    let applied = [1, 4];
    let result = versionchain_prefix(available, applied);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
2
1
8
```

## API

`versionchain_prefix(available, applied)`

Returns [applied prefix length, pending count, next version or -1]. Every applied version must match the corresponding release entry. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| available | Vector of values, each a nonnegative exact integer |
| applied | Vector of values, each a nonnegative exact integer |

## In use

[Bittern](https://github.com/Rahulchaube1/blyx-bittern) uses this module to plan the next migration only after history, fingerprints and dirty state agree.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-versionchain/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). Read the [artwork notice](assets/NOTICE.txt) for credits.

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
