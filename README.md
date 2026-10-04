# artoolkit-nft-bench-results

Raw benchmark results of [artoolkit-nft-bench](https://github.com/webarkit/artoolkit-nft-bench). The code repository holds
the software, the result **tables** and an index, [`results/manifest.json`](https://github.com/webarkit/artoolkit-nft-bench/blob/main/results/manifest.json);
this repository holds the **raw data** behind those tables (per-frame poses and timings for every engine and configuration).
Why two repositories: [ADR-0001](https://github.com/webarkit/artoolkit-nft-bench/blob/main/docs/adr/0001-results-storage.md).

## Publications

<!-- publications:start -->
| publication | milestone | code release | SHA-256 | data release |
|---|---|---|---|---|
| phase-1 | M1 — Native baseline | v0.1.0 | `95e9c8724d6c221551f2b270affe27b9eb190c4c1bcaa930dd97ae267ae36dc6` | phase-1 |
<!-- publications:end -->

Each publication is a directory `<name>/` holding `<name>.tar.gz`, usually also attached to an immutable
[release](https://github.com/webarkit/artoolkit-nft-bench-results/releases) with the same name.

## Download and verify

```bash
gh release download phase-1 --repo webarkit/artoolkit-nft-bench-results
sha256sum phase-1.tar.gz          # must equal the SHA-256 above and in results/manifest.json
tar -xzf phase-1.tar.gz
```

Then score with the code repository at the matching release (`v0.1.0` for `phase-1`), after rebuilding the frame banks:

```bash
.venv/Scripts/python -m nftbench.score --bank banks/pinball-bench --result phase-1/native-pinball-bench-t1.json
```

## Rules

* **Append-only.** Each publication is one commit, made by `scripts/publish_results.py` in the code repository, which also scans
  every file for sensitive data (host names, user names, emails, absolute paths, tokens, IP/MAC addresses) and refuses to publish
  if any is found. Commits that only edit this README are not publications.
* **Data is never deleted or rewritten.** Force pushes and deletion of `main` are blocked by a ruleset; releases are immutable.
* **A wrong result is superseded, not removed:** publish a new archive under a new name and record the supersession in the manifest.

## License

LGPL-3.0-or-later, as the code repository.
