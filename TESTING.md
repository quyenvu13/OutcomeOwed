# Testing status — final

## ĐÃ TỰ CHẠY

- Kill-set gate: PASS — 10 cases, zero separating token/bigram.
- Rubric overlap gate: PASS — zero shared content word; rubric also matches the locked block byte-for-byte.
- Production-source unit suite: PASS — 22 tests, including all nine deterministic negative categories.
- ID/parity suite: PASS — 17 tests, including Python whitespace U+001C–U+001F, U+0085, extended Unicode spaces, code-point length, and Keccak ID equality.
- GenVM linter: PASS — return code 0; four non-blocking view return-annotation warnings.
- Source gate: PASS — header/API/write-surface/fail-safe checks, return code 0.
- Clean `npm ci`: PASS — return code 0.
- `npm run build`: PASS — return code 0.
- `npm test`: PASS — kill-set gate, 22 production-source tests, and 17 ID/parity tests, return code 0.
- Clean ZIP reinstallation: PASS — unpacked archive, fresh `npm ci`, source gate, 22 production tests, 17 parity tests, and linter all returned code 0.
- Calldata probe: PASS — all 10 locked semantic cases were accepted by `eth_estimateGas` against `0xABf95165E21499D74fbC59966368B09db9C90DA9`; return code 0. This proves payload reception only.
- Deployment: PASS — transaction `0xdf77edee6af1c25a1f266e9e52303d5eef3b4ede239417168129f022acc48ba4` shows Accepted, GenVM SUCCESS, Return, and Finalized.
- Semantic runtime: PASS — all eight signed StudioNet transactions are `FINALIZED` with `MAJORITY_AGREE`; D3/E3 and D4/E4 received the intended opposite verdicts.
- Opposite record-shape teeth: PASS — RESULT rejected `log_entry` and accepted `claim_discharge`; EFFORT rejected `claim_discharge` and accepted a counterparty `log_entry`.
- Final-state readback: PASS — D3 is `CLAIMED`; E3 is `RUNNING` with one attributed log; D4 is `RESULT/OPEN`; E4 is `EFFORT/RUNNING` on `latest-final` state.
- Frozen source parity: PASS — Studio-returned source and packaged source have canonical SHA-256 `41e8ed9e10d1486e003c9fcede2f94a1b7a3b9894924f54cac1ddec847e6543d`; their only byte-level difference is CRLF versus LF line endings.

## Live proof summary

- Network: StudioNet `61999`, Normal (Full Consensus)
- Contract: `0xABf95165E21499D74fbC59966368B09db9C90DA9`
- Author: `0x923a09d0D6e5C242e36C3c1D2071835917cC0bDF`
- Other side: `0x76DD809f34e0B72d9339bc509e1E19FaFEB445c2`
- Full transaction hashes and exact post-states: `ONCHAIN_EVIDENCE.md`

## What this run does NOT prove

This proof establishes the tested on-chain behavior; it does not prove that an off-chain promise was actually performed, that the named second wallet belongs to a different person, or that future validators will classify every possible text identically. The contract intentionally records claims and observations rather than proving real-world performance.
