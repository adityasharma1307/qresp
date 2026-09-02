# qknot

Hybrid post-quantum signing: Ed25519 + ML-DSA-87 in one bundle. Existing OpenSSF Model Signing verifiers still accept it. A signature made today stays attributable after classical algorithms fall.

Student research (CS F376, BITS Pilani Dubai). Not a product. [Disclaimer](DISCLAIMER.md).

## Why

A side-by-side hybrid is trivial to strip: delete the PQ field and a "every remaining signature is valid" verifier is happy. Both algorithms here sign a commitment to the *set* of algorithms, so dropping one is visible.

A cross-registry audit of Hugging Face, npm, and PyPI found **zero** post-quantum signatures. That's the motivation. Details: [qresp-pilot](https://github.com/adityasharma1307/qresp-pilot).

## Use

```bash
pip install qknot

qknot sign ./dist/myapp-1.0.0.tar.gz --out myapp.bundle.json \
    --keys-out keys.json --name myapp-1.0.0 --context myapp-release
qknot verify ./dist/myapp-1.0.0.tar.gz --bundle myapp.bundle.json \
    --context myapp-release
```

Python 3.10+. Tests: `docs/THREAT-MODEL.md`, `CONTRIBUTING.md`. Releases are self-signed; v0.1.1's tarball ships with a hybrid signature over its own bytes.

Supervisor: Dr. Tamizharasan Periyasamy. License: MIT.
