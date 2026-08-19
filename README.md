# CJ Chanhnourack

Founder of Centennial Defense Systems in Colorado Springs. I build audit-first software for
tool-using AI systems.

The thesis, everywhere: **it doesn't answer — it testifies.** Every product below ships with a
way to verify the claim yourself: a hash to check, a verifier to run, a ledger to recompute.

## Ships you can buy today

**[Archivist Sort](https://sort.archivist.tools/)** — Mac file cleanup that can't delete
anything: scan → review → approve → quarantine → checksummed receipt → byte-verified rollback.
Notarized, $29 one-time, no subscription, no telemetry — and the artifact SHA-256 is printed on
the page so you can verify the download before you ever open it:

```
shasum -a 256 Archivist-Sort.dmg
# be0bccba86ac465a6109c810b00fe227f3d88653bd122f170c7443254c36fe38
```

It ships with an MCP server for agent fleets: read tools (scan, census, duplicate evidence, plan
preview) mutate nothing; every mutation goes to a checksummed quarantine — never a delete — and
is byte-reversible with rollback. The safety model is recovery, not prevention: Sort gates and
receipts its own actions so an agent's mistake through Sort is always recoverable and auditable.
It does not sandbox your agent's other tools — which is exactly why quarantine-and-rollback, not a
gate, is what protects you.

## Break this, get named credit

**[The Testify Challenge](https://github.com/cjchanh/aaap-challenge)** — our attestation format,
public, with a standing invitation: make a changed or unsafe packet still pass the verifier and
your name goes in the repo. 54 commissioned attack cases are published in-tree — two passes broke
earlier versions (every break fixed and credited), the third survived clean. The record is the
marketing.

## Start here (runnable in two minutes): Deponent

[Deponent](https://github.com/cjchanh/deponent) is the public Python kernel for governed
agent-action evidence: make an action request, evaluate policy, allow or block it, record the
decision, and let another person recompute the record.

```
python3 -m venv /tmp/deponent-eval
source /tmp/deponent-eval/bin/activate
python -m pip install deponent==0.1.1
python -c "import pathlib,tempfile; from deponent import Cell; root=tempfile.mkdtemp(); target=pathlib.Path(root,'blocked-example'); target.mkdir(); c=Cell(root,use_jail=False); print(c.act('write_file',{'path':'n.txt','content':'hi'}).output); print(c.act('run_cmd',{'cmd':'rm -rf ./blocked-example'}).output); print('target preserved:',target.exists()); print(c.verify())"
python -m deponent.badge verify --kernel deponent
```

Expected behavior: the write is allowed, the relative-path destructive fixture is blocked,
`target preserved: True` confirms the disposable directory remains, and the two-entry ledger
chain verifies. The fixture targets only a new subdirectory inside the temporary workspace, so a
gate failure cannot target the host root.

## Related public work

- [GAK Conformance Standard](https://github.com/cjchanh/gak-conformance-standard) — testable
  language for governed-agent action gates. Published certifications are author-built;
  third-party verdicts are still zero.
- [Sworn](https://github.com/cjchanh/sworn) — commit-governance research. Not part of the current
  validator path; a known zero-kernel boundary requires a security audit before promotion.
- [mildoc-lint](https://github.com/cjchanh/mildoc-lint) — evidence-oriented linting for
  military/technical documents. Public main CI is green at ec9d544
  (https://github.com/cjchanh/mildoc-lint/actions/runs/31554837180).
- [fleet-watch](https://github.com/cjchanh/fleet-watch) — process governance for agent fleets on
  one machine; 0.2.0 on PyPI (`pipx install fleet-watch`).
- [map-ruler](https://github.com/cjchanh/map-ruler) — deterministic map calibration. Public main
  CI is green at 127f789 (https://github.com/cjchanh/map-ruler/actions/runs/31554834611).

## What I will and will not claim

- Research prototypes, not security accreditations.
- Tamper-evident records, not tamper-proof systems.
- Public runnable evidence, not customers, deployment, awards, or production accreditation.
- Internal tests are not third-party validation.

I am looking for skeptical technical reruns. A useful response says whether the problem is real,
whether the output would help, and what control is missing.

Contact: contact@centennialdefense.systems
