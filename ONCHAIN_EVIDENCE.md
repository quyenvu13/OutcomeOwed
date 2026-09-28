# Runtime evidence — OutcomeOwed IC

Network: GenLayer StudioNet, chain ID `61999`, Normal (Full Consensus).

Contract address: `0xABf95165E21499D74fbC59966368B09db9C90DA9`

Deployment transaction: `0xdf77edee6af1c25a1f266e9e52303d5eef3b4ede239417168129f022acc48ba4`

Author / deployer: `0x923a09d0D6e5C242e36C3c1D2071835917cC0bDF`

Other / counterparty: `0x76DD809f34e0B72d9339bc509e1E19FaFEB445c2`

Deployment observed: `ACCEPTED`, `GenVM SUCCESS`, result code `Return`, `FINALIZED`, return value `null`.

Every row requires the full transaction hash, lifecycle state, GenVM result, semantic output where applicable, and verified `get_undertaking` post-state. `FINALIZED` alone is insufficient.

| # | Role | Method / exact input | Expected | Tx / result / post-state |
|---:|---|---|---|---|
| 1 | author | `open_undertaking(other, "the Client", "The backlog will be cleared.")` | RESULT_OWED; RESULT; OPEN | PASS — `0xade8ad4dc49ac0f4e71afe8e41728bdc7e36b4522867f45fbaa96217de585301`; ACCEPTED/SUCCESS; RESULT_OWED; RESULT; OPEN |
| 2 | author | `log_entry(D3_ID, "Weekly work update.")` | rollback: `This undertaking is discharged by a claim, not by a log` | PASS — `0x6fc3bfd4dde5ab7a450078c3c8223e155001d22ae7b45d47a5ed8ab10cefe269`; ACCEPTED/ERROR; exact rollback message |
| 3 | author | `claim_discharge(D3_ID, "The backlog is cleared.")` | SUCCESS; CLAIMED | PASS — `0x838d6a535eded3e6ff96bd9da90b7ad8229bd8bc01452e1bc5edad0f8818fe68`; ACCEPTED/SUCCESS; latest-final read: CLAIMED; exact claim note |
| 4 | author | `open_undertaking(other, "the Client", "The backlog will be worked on daily.")` | EFFORT_OWED; EFFORT; RUNNING | PASS — `0xfb42b9e8a527f02a7792431f413b8b48f27acfda203eb56542063542c9a86f03`; ACCEPTED/SUCCESS; EFFORT_OWED; EFFORT; RUNNING; log_count=0 |
| 5 | author | `claim_discharge(E3_ID, "The work is complete.")` | rollback: `This is a standing obligation; add a log entry instead` | PASS — `0x37a3d71bf631694b7936b2a53b3b3cc02edb588f84997a6c4c99a7dd29d64482`; ACCEPTED/ERROR; exact rollback message |
| 6 | other | `log_entry(E3_ID, "Daily work observed.")` | SUCCESS; log_count=1; `log_by[1]=other`; RUNNING | PASS — `0x84454a92e9905bd1af32a53253c9517f002d23857ac2285f9d6895d4ae9aca38`; ACCEPTED/SUCCESS; RUNNING; log_count=1; entry 1 by other with exact note |
| 7 | author | `open_undertaking(other, "the Client", "We will apply every available method, and the licence will be approved.")` | RESULT_OWED | PASS — `0x1042874739715527b0099ce176e2dd324cfc6c6fd64a037b5e03c56798f9e273`; ACCEPTED/SUCCESS; latest-final read: RESULT_OWED; RESULT; OPEN |
| 8 | author | `open_undertaking(other, "the Client", "We will pursue the licence application diligently.")` | EFFORT_OWED | PASS — `0xdf61a40d7e4656073919060c1b06568c1d957c3182f163e90ae4d9b02fe91f81`; ACCEPTED/SUCCESS; latest-final read: EFFORT_OWED; EFFORT; RUNNING |

The decisive proof is opposite method availability in rows 2 and 5, successful writes in rows 3 and 6, and the paired semantic outcomes in rows 1/4 and 7/8. Simpler deterministic replay and authorization cases remain offline tests.

On 2026-09-28, all eight hashes were independently read from StudioNet as `FINALIZED` with `MAJORITY_AGREE`. Final state was read with the `latest-final` transaction variant. D3 is `CLAIMED`; E3 is `RUNNING` with `log_count=1` and entry 1 attributed to the other wallet; D4 is `RESULT/OPEN`; E4 is `EFFORT/RUNNING`.
