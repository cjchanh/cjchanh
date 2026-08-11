# CJ Chanhnourack

Founder of [Centennial Defense Systems](https://centennialdefense.systems/) in Colorado Springs. I build audit-first software for tool-using AI systems.

The current wedge is governed agent-action evidence: make an action request, evaluate policy, allow or block it, record the decision, and let another person recompute the record.

## Start here: Deponent

[Deponent](https://github.com/cjchanh/deponent) is the public Python kernel.

```bash
python3 -m venv /tmp/deponent-eval
source /tmp/deponent-eval/bin/activate
python -m pip install deponent==0.1.0
python -c "import tempfile; from deponent import Cell; c=Cell(tempfile.mkdtemp(), use_jail=False); print(c.act('write_file',{'path':'n.txt','content':'hi'}).output); print(c.act('run_cmd',{'cmd':'rm -rf /'}).output); print(c.verify())"
python -m deponent.badge verify --kernel deponent
```

Expected behavior: the write is allowed, the destructive fixture is blocked, and the two-entry ledger chain verifies.

## Related public work

- [GAK Conformance Standard](https://github.com/cjchanh/gak-conformance-standard) — testable language for governed-agent action gates. Published certifications are author-built; third-party verdicts are still zero.
- [Sworn](https://github.com/cjchanh/sworn) — commit-governance research. It is not part of the current validator path; a known zero-kernel boundary requires a security audit before promotion.
- [mildoc-lint](https://github.com/cjchanh/mildoc-lint) — evidence-oriented linting for military/technical documents. Its package test fix is public; the current public CI lint gate is not green.
- [map-ruler](https://github.com/cjchanh/map-ruler) — deterministic map calibration. README setup is portable; current public CI still has a plot-dependency failure.

## What I will and will not claim

- Research prototypes, not security accreditations.
- Tamper-evident records, not tamper-proof systems.
- Public runnable evidence, not customers, deployment, awards, or production accreditation.
- Internal tests are not third-party validation.

I am looking for skeptical technical reruns. A useful response says whether the problem is real, whether the output would help, and what control is missing.

Contact: [contact@centennialdefense.systems](mailto:contact@centennialdefense.systems)
