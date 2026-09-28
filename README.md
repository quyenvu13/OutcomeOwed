# OutcomeOwed

OutcomeOwed is a GenLayer Intelligent Contract for StudioNet `61999` / py-genlayer `v0.2`. It performs one narrow semantic classification when an undertaking is opened:

Deployed contract: `0xABf95165E21499D74fbC59966368B09db9C90DA9`  
Deployment tx: `0xdf77edee6af1c25a1f266e9e52303d5eef3b4ede239417168129f022acc48ba4`

- `RESULT_OWED`: a closed two-slot record. The author may claim discharge once; the named other side may rebut once; the record then settles.
- `EFFORT_OWED`: a two-sided running log. Either named side may append entries, but nobody can claim completion and the record never reaches a completed state.

All authorization, identifiers, limits, one-time guards, record writes, and state transitions are deterministic. Only `open_undertaking` invokes semantic consensus. The eight-transaction StudioNet proof path passed and every transaction is finalized.

## How to try it

1. Open the deployed contract in GenLayer Studio using Normal (Full Consensus).
2. Use two wallets: `author` and `other`. Neither address is hardcoded.
3. Inspect the completed eight-transaction proof in `ONCHAIN_EVIDENCE.md`.
4. Read each post-state with `get_undertaking`; use `get_log_entry` or `get_log` for effort records.

The live proof includes GenVM results, semantic outcomes, opposite rollback paths, successful writes, and final-state reads. It does not rely on `FINALIZED` alone.

## Verification package

This minimal folder contains only the submission-facing files. The separate full archive contains the executable 22-test production suite, 17 parity tests, kill-set gate, source gate, GenVM lint setup, and clean-install verification commands.

## Honest limitations

1. The contract holds no money and enforces nothing off-chain. It only determines the record shape and who may write which facts into it.
2. `claim_discharge` and `log_entry` are self-reports; they do not prove the underlying work happened. Their value is the enforced shape and permanent on-chain attribution beside the other side's rights.
3. A false `RESULT_OWED` is the principal risk: an effort obligation could be sealed by one discharge claim. The fail-safe is `EFFORT_OWED`, and every result record reserves one rebuttal for the named other side.
4. A false `EFFORT_OWED` never closes even if the work is complete. That burden intentionally falls on the author of ambiguous text.
5. The author supplies the other-side wallet. The contract prevents self-naming but cannot prove that a second address belongs to a different person.
6. Effort logs have a storage cap of 30 entries. A full log remains `RUNNING`; it simply stops accepting new entries.

## No escrow

OutcomeOwed has no payable method, transfer path, token balance, or escrow function.
