# rulespec-vn Agent Notes

This repo stores Viet Nam RuleSpec source registry materials, oracle references, and encoded policy rules. All encoded law lives under a single `vn/` namespace.

## Scope

- `vn/statutes/`: Vietnamese laws - Luat 04/2007/QH12 (PIT), Luat 13/2008/QH12 (VAT), Luat 57/2010/QH12 (EPT), Luat 58/2014/QH13 (social insurance), and other primary law needed for tax-benefit modeling.
- `vn/regulations/`: nghi dinh and circulars (Nghi dinh 20/2021/ND-CP social assistance, Nghi dinh 76/2024/ND-CP amendment, implementation decrees) made under the laws.
- `vn/policies/`: administratively set programme rules.
- `programs/`: declarative compose specs (one per jurisdiction/program/period).
- `data/coverage/`, `data/oracles/`: coverage backlog and comparison references. These are never legal authority.

## Do

- Start from the furthest upstream source: vanban.chinhphu.vn document pages / datafiles.chinhphu.vn signed scans and Cong Bao first, ministry circulars next, commercial mirrors never as primary - record the host in manifest metadata.
- Respect the capture notes (see README): pre-2014 portal pages are full-text HTML; newer signed scans are image-only (force_ocr, ocr_dpi 300, ocr_language vie - Vietnamese diacritics OCR cleanly at 300dpi); datafiles.chinhphu.vn serves file paths directly despite a 403 root.
- Add RuleSpec under `vn/statutes/`, `vn/regulations/`, or `vn/policies/` with companion `.test.yaml` files.
- Cite corpus paths from modules via `module.source_verification.corpus_citation_path` (or `corpus_citation_paths`).
- Use the VNMOD v3.5 policy window (2013-24) as the validation frame: PIT bands 5-35% over VND 5-80M monthly; SIC pension 8/14 + health 1.5/3 + unemployment 1/1; VAT 10% (0/5% lists); assistance standard VND 360,000 -> 500,000 from 07/2024. Indexed/annual values must be corpus-grounded, never invented.
- Keep exact oracle versions in `data/oracles/oracle-index.json`. The SOUTHMOD bundle is licensed and non-redistributable - never commit bundle bytes, dataset rows, or model XML.
- Sync `axiom-encode` and `.axiom/toolchain.toml` before substantial encoding runs.

## Do Not

- Use tax-firm alerts or commercial mirrors as the first legal source when a law or instrument governs the rule.
- Invent, round, or interpolate any Vietnamese monetary amount, rate band, or threshold. Every number must come verbatim from a captured official provision.
- Migrate VNMOD, EUROMOD/SOUTHMOD, or agency calculator code mechanically as RuleSpec.
- Add generated source payload dumps, formula artifacts, `parameters.yaml`, or standalone YAML fixtures outside allowed RuleSpec roots.
- Hand-copy statute text into RuleSpec without a corpus `citation_path`.
