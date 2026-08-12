# CJ Chanhnourack

Founder of [Centennial Defense Systems](https://centennialdefense.systems/) in Colorado Springs. I build audit-first software for tool-using AI systems.

The current wedge is governed agent-action evidence: make an action request, evaluate policy, allow or block it, record the decision, and let another person recompute the record.

## Start here: Deponent

[Deponent](https://github.com/cjchanh/deponent) is the public Python kernel.

```bash
python3 -m venv /tmp/deponent-eval
source /tmp/deponent-eval/bin/activate
python -m pip install deponent==0.1.1
python -c "import pathlib,tempfile; from deponent import Cell; root=tempfile.mkdtemp(); target=pathlib.Path(root,'blocked-example'); target.mkdir(); c=Cell(root,use_jail=False); print(c.act('write_file',{'path':'n.txt','content':'hi'}).output); print(c.act('run_cmd',{'cmd':'rm -rf ./blocked-example'}).output); print('target preserved:',target.exists()); print(c.verify())"
python -m deponent.badge verify --kernel deponent
```

Expected behavior: the write is allowed, the relative-path destructive fixture is blocked, `target preserved: True` confirms the disposable directory remains, and the two-entry ledger chain verifies. The fixture targets only a new subdirectory inside the temporary workspace, so a gate failure cannot target the host root.

## Related public work

- [GAK Conformance Standard](https://github.com/cjchanh/gak-conformance-standard) — testable language for governed-agent action gates. Published certifications are author-built; third-party verdicts are still zero.
- [Sworn](https://github.com/cjchanh/sworn) — commit-governance research. It is not part of the current validator path; a known zero-kernel boundary requires a security audit before promotion.
- [mildoc-lint](https://github.com/cjchanh/mildoc-lint) — evidence-oriented linting for military/technical documents. Public main CI is green at ec9d544 (https://github.com/cjchanh/mildoc-lint/actions/runs/31554837180).
- [fleet-watch](https://pypi.org/project/fleet-watch/) 0.2.0 is on PyPI. Public repo: https://github.com/cjchanh/fleet-watch (recovered/published 2026-08-12).
- [map-ruler](https://github.com/cjchanh/map-ruler) — deterministic map calibration. Public main CI is green at 127f789 (https://github.com/cjchanh/map-ruler/actions/runs/31554834611).

## What I will and will not claim

- Research prototypes, not security accreditations.
- Tamper-evident records, not tamper-proof systems.
- Public runnable evidence, not customers, deployment, awards, or production accreditation.
- Internal tests are not third-party validation.

I am looking for skeptical technical reruns. A useful response says whether the problem is real, whether the output would help, and what control is missing.

Contact: [contact@centennialdefense.systems](mailto:contact@centennialdefense.systems)
