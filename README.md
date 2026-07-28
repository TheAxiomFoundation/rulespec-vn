# rulespec-vn

Viet Nam RuleSpec source registry.

This repository targets the Vietnamese tax-benefit surface simulated by VNMOD (the SOUTHMOD tax-benefit microsimulation model for Viet Nam, UNU-WIDER; v3.5, policy years 2013-24): personal income tax under Luat 04/2007/QH12 (seven progressive bands of 5/10/15/20/25/30/35 percent over monthly taxable-income thresholds of VND 5/10/18/32/52/80 million; deduction levels set by later instruments - tranche-2), social insurance contributions under Luat 58/2014/QH13 (2024 headline splits: pension 8 percent employee / 14 percent employer; health 1.5/3; unemployment 1/1; sick-and-maternity 3 employer; work-injury 0.5 employer), VAT under Luat 13/2008/QH12 (10 percent standard with 0 and 5 percent lists), the environmental protection tax on fuels under Luat 57/2010/QH12 (per-litre levies adjusted by UBTVQH resolutions - tranche-2), and social assistance under Nghi dinh 20/2021/ND-CP (baseline standard support rate VND 360,000/month) as amended by Nghi dinh 76/2024/ND-CP (VND 500,000/month from 01/07/2024).

All encoded law lives under a single `vn/` namespace. The validation frame is VNMOD v3.5 (report CR-VNMOD-v3.5, Tables 2.3-2.9).

## Source Priority

Policy must come from the furthest upstream available source: the Government official-documents portal (vanban.chinhphu.vn document pages and the digitally signed scans on datafiles.chinhphu.vn) and Cong Bao texts first, ministry circulars next, commercial mirrors (thuvienphapluat, luatvietnam) never as primary. Portal notes: pre-2014 laws are full-text HTML document pages; newer instruments are image-only signed scans (capture with force_ocr, ocr_language vie); datafiles.chinhphu.vn 403s on its root but serves file paths directly.

## Corpus binding

`.axiom/toolchain.toml` pins the immutable signed corpus release this repository consumes (`vn-rulespec-2026-07-24`). The shared validate workflow verifies the release object signature, content hash, and waiver-set hash on every push.

## Layout

- `vn/statutes/`, `vn/regulations/`, `vn/policies/`: encoded RuleSpec modules with mandatory companion `.test.yaml` files.
- `programs/`: declarative compose specs (one per jurisdiction/program/period).
- `data/oracles/`, `data/coverage/`: comparison-oracle references and the VNMOD instrument map. Never legal authority.

## Parity program

Tracked on issue #1: tranche-2 captures (PIT amendment Luat 26/2012/QH13 + deduction Resolution 954/2020/UBTVQH14; VAT amendment 31/2013/QH13 + the 2022-24 8-percent reduction resolutions; EPT schedule Resolutions 579/2018 etc.; SST Luat 27/2008/QH12; Decree 136/2013 predecessor amounts; COVID-19 support instruments) and VNMOD parity tests per instrument.

## Listing gates

This repo carries `app_visibility = "experimental"` in `.axiom/registry.toml` and stays out of app surfaces until:

1. The encoded surface covers the flagship calculation (personal income tax gross-to-net for a formal employee) end to end with companion tests.
2. Oracle parity suites exist and pass against VNMOD for the encoded surface.
3. Citation paths are stable (instrument-number form, Luat 04/2007/QH12 style, against the Cong Bao and vanban.chinhphu.vn official prints).
