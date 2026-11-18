# Agents Only portal: QA bug report and test suite (account creation, Identification step)

An independent QA write-up of a **blocking defect** I ran into as a real candidate while creating my account on the Agents Only portal (`https://agents.agentsonly.com/account-creation`). The repository includes a professional bug report, a test suite for the affected form section, and redacted evidence.

> **Disclaimer:** This is an independent portfolio project. I am not affiliated with Agents Only or Teleperformance, and this is not an official report from them. It documents a defect I hit while applying as a candidate. Everything here is based only on what I observed and captured, and no testing was done beyond normal use of the form as a candidate. All personal data has been removed or redacted from the evidence.

## Defect summary

| | |
|---|---|
| **Bug** | [BUG-001](bug-report/BUG-001.md): "Cartão de Cidadão" (Citizen Card) is always required, so foreign residents of Portugal cannot complete account creation |
| **Where** | Step 1 "Personal Info", "Identification" section |
| **Severity / Priority** | Blocker (for foreign residents) / High (suggested) |
| **Status** | Open: reported to the company's recruitment and support teams on 17 Nov 2026; unresolved as of 18 Nov 2026 |

In the "Identification" section, the "Cartão de Cidadão (Citizen Card)" field is **mandatory** even when "Residence Card (Número do Cartão/Título de Residência)" (the residence permit number) is filled in. The "Next" ("Próximo") button stays disabled. The "Country" field is locked to "Portugal", and the form offers no nationality field, no document-type option (for example a passport), and no help link. Foreign nationals living legally in Portugal with a residence permit and no Portuguese Citizen Card are therefore stuck at step 1.

**Expected:** the form accepts **either** a Cartão de Cidadão **or** a Residence Card number (exactly one of the two required), then enables "Next".

## Scope

- **In scope:** the "Identification" section of step 1 "Personal Info" in the account creation wizard: the "Cartão de Cidadão" and "Residence Card" fields, how they interact, the "Country" field, whether "Next" is enabled, the available help and document options, and basic accessibility.
- **Out of scope:** other steps of the wizard (Identity Verification, Document Upload, etc.), the backend/API, performance and security testing.

## Repository structure

```
.
├── README.md                                   # This file
├── bug-report/
│   └── BUG-001.md                              # Full bug report
├── test-suite/
│   ├── identification-test-suite.xlsx          # Test cases (formatted, with a summary sheet)
│   └── identification-test-suite.csv           # Same test cases as plain CSV
└── evidence/                                   # Redacted media only
    ├── identification-section-redacted.png
    ├── country-field-locked-redacted.png
    ├── identification-required-next-disabled-redacted.png
    └── screen-recording-redacted.mp4
```

## Test suite at a glance

[`test-suite/identification-test-suite.xlsx`](test-suite/identification-test-suite.xlsx) ([CSV](test-suite/identification-test-suite.csv)) contains **24 test cases**. They cover the "either/or" logic between "Cartão de Cidadão" and "Residence Card", the "Country" field, when "Next" is enabled, the missing nationality, document-type and help options, input validation and boundary values, and basic accessibility.

| Status | Count |
|---|---|
| Pass | 3 |
| Fail | 3 |
| Blocked | 0 |
| Not run | 18 |

Only cases whose outcome is visible in the captured evidence are marked Pass or Fail. Everything else is "Not run". All test data is fictitious.

## Tools used

- Manual exploratory testing as a real candidate (desktop browser)
- Screen recording and screenshots for evidence
- Spreadsheet-based test case design (Excel / CSV)
- FFmpeg and Pillow (Python) to redact personal data from the screenshots and video
- Markdown and Git / GitHub for documentation

## Author

[@viniciussilva2504](https://github.com/viniciussilva2504): Junior QA Analyst (TripleTen QA program graduate), based in Portugal.
