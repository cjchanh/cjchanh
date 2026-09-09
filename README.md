# CJ Chanhnourack

Founder of Centennial Defense Systems in Colorado Springs. I build software
for tool-using AI systems that you can check yourself.

Every product below ships with a way to verify the claim: a hash to check,
a verifier to run, a ledger to recompute.

## Ships you can buy today

**[Archivist Sort](https://sort.archivist.tools/)** — Mac file cleanup that can't delete
anything: scan → review → approve → quarantine → checksummed record → byte-verified rollback.
Notarized, $29 one-time, no subscription, no telemetry — and the artifact SHA-256 is printed on
the page so you can verify the download before you ever open it:

```
shasum -a 256 Archivist-Sort.dmg
# compare with the SHA-256 printed on https://sort.archivist.tools/download.html
# (v2.3.0 as of 2026-09-04: 74f9147bcb8e2f3b69167e57f0d9cb544bf5e9527b9a13d38400555417a73d1a)
```

The download page is the source of truth for the current hash; this README records one dated
value and will lag a release.

It ships with an MCP server for agent fleets: read tools (scan, census, duplicate evidence, plan
preview) mutate nothing; every mutation goes to a checksummed quarantine — never a delete — and
is byte-reversible with rollback. The safety model is recovery, not prevention: Sort checks and
records its own actions so an agent's mistake through Sort is always recoverable and auditable.
It does not sandbox your agent's other tools — which is exactly why quarantine-and-rollback, not a
gate, is what protects you.

## Break this, get named credit

**[The AAAP Challenge](https://github.com/cjchanh/aaap-challenge)** — a public attestation
format with a standing invitation: make a changed or unsafe packet still pass the verifier and
your name goes in the repo. 54 commissioned attack cases are published in-tree — two passes broke
earlier versions (every break fixed and credited), the third survived clean. The record is the
marketing.

## Three public kernels

**[Deponent](https://github.com/cjchanh/deponent)** — Python kernel for agent-action evidence:
make an action request, evaluate policy, allow or block it, record the decision, and let another
person recompute the record. Refuses destructive commands that leave the workspace.

```
python3 -m venv /tmp/deponent-eval
source /tmp/deponent-eval/bin/activate
python -m pip install deponent==0.1.2
python -c "import pathlib,tempfile; from deponent import Cell; root=tempfile.mkdtemp(); target=pathlib.Path(root,'blocked-example'); target.mkdir(); c=Cell(root,use_jail=False); print(c.act('write_file',{'path':'n.txt','content':'hi'}).output); print(c.act('run_cmd',{'cmd':'rm -rf ./blocked-example'}).output); print('target preserved:',target.exists()); print(c.verify())"
python -m deponent.badge verify --kernel deponent
```

Expected behavior: the write is allowed, the relative-path destructive fixture is blocked,
`target preserved: True` confirms the disposable directory remains, and the two-entry ledger
chain verifies. The fixture targets only a new subdirectory inside the temporary workspace, so a
gate failure cannot target the host root.

**[Sworn](https://github.com/cjchanh/sworn)** — commit-check research. Not on the current
validator path; a known kernel boundary needs a security review before promotion. Refuses to
claim a bypassable local hook is the enforceable check.

**[fleet-watch](https://github.com/cjchanh/fleet-watch)** — process control for agent fleets on
one machine; 0.2.0 on PyPI (`pipx install fleet-watch`). Refuses a second exclusive writer on
the same repo.

## Outside check

The only outside verification so far is a 2026-09-05 red-team of the public surface
([report](docs/redteam-2026-09-05.md)). Closing commits:

- D-1 glued-flag path escape — [b18ff68](https://github.com/cjchanh/deponent/commit/b18ff685e6e2468f65abfb32d10568a70f8157bf) → [e1a2bf1](https://github.com/cjchanh/deponent/commit/e1a2bf1b88d8429e42c44b0d4a2316c4841f754f)
- C1 interpreter deny-by-default — [353f91b](https://github.com/cjchanh/deponent/commit/353f91b7b46e1d84ffc7ff7dc23131f0c479ff9c)
- F-1 / F-2 exclusive-lease race + subdirectory bypass — [8774f89](https://github.com/cjchanh/fleet-watch/commit/8774f89a6907bafc512dd366cc420eda40d04898) + [743dfde](https://github.com/cjchanh/fleet-watch/commit/743dfde407463ff71e9dd21f532de04f43fb6608)
- L-1 stale release manifest — [53c5aa3](https://github.com/cjchanh/longmemeval-evidence/commit/53c5aa3cffed96b621fb9ef7bd054d8d0685a6c1) + [f581ce6](https://github.com/cjchanh/longmemeval-evidence/commit/f581ce60efeb4aa59485a959962d00e0ab774a3c)

## What I will and will not claim

- Research prototypes, not security accreditations.
- Tamper-evident records, not tamper-proof systems.
- Public runnable evidence, not customers, deployment, awards, or production accreditation.
- Internal tests are not third-party validation.

I am looking for skeptical technical reruns. A useful response says whether the problem is real,
whether the output would help, and what control is missing.

Contact: contact@centennialdefense.systems
