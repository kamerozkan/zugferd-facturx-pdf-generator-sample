> **Release status:** The Actor is private and publication is pending. The
intended Store URL is
[zugferd-facturx-pdf-generator](https://apify.com/kamerozkan/zugferd-facturx-pdf-generator), but this link
must not be treated as evidence that the Actor is publicly available.

# ZUGFeRD and Factur-X PDF Generator: JSON Examples and Dataset Schema

![Release](https://img.shields.io/badge/release-private%20pending-orange)
![Examples](https://img.shields.io/badge/examples-3%20paired%20local%20runs-2f855a)
![Schema](https://img.shields.io/badge/schema-Actor%20dataset-4c1)
![Price](https://img.shields.io/badge/planned%20PPE-%240.01-blue)
![License](https://img.shields.io/badge/license-MIT-blue)

Generate a visible ZUGFeRD 2.5 and Factur-X 1.09 EN 16931 PDF/A-3 invoice with embedded CII XML from structured JSON.

This flat sample repository contains three paired JSON inputs and outputs,
the exact Actor input and dataset schema snapshots, and a standard JSON Schema
for one dataset row. The examples were generated and technically evaluated by
the local release engine. They are not copied from a live Apify run.

Search topics: ZUGFeRD generator, Factur-X generator, PDF/A-3 invoice API, embedded CII XML, ZUGFeRD 2.5, Factur-X 1.09.

## What the generator does

1. Accepts one `invoice` object or an `invoices` batch of up to 100.
2. Parses monetary values from decimal strings, never binary JSON floats.
3. Calculates line, tax, and payable totals with decimal arithmetic.
4. Generates a visible Factur-X and ZUGFeRD EN 16931 PDF/A-3 invoice.
5. Runs Mustangproject 2.24.0 ZUGFeRD 2.5 rules plus veraPDF 1.30.2 PDF/A-3 validation.
6. Delivers only an artifact accepted by the complete pinned local preflight.
7. Returns SHA-256, byte count, versions, findings, and explicit scope limits.

## Three paired examples

| # | Scenario | Input JSON | Output JSON | Generated artifact SHA-256 |
|---:|---|---|---|---|
| 1 | Standard consulting service invoice | [input](01_standard_service_input.json) | [output](01_standard_service_output.json) | `95d5754a06a49a4676e141a5ab95ac56a8243b0e512d56469c59538dd2e63ea9` |
| 2 | Multi-line professional services invoice | [input](02_multi_line_input.json) | [output](02_multi_line_output.json) | `3e41fca33a3adb6d5b441affaf1e158170c36da12bd62abe3487d9bf1614d0bc` |
| 3 | Recurring service invoice | [input](03_recurring_service_input.json) | [output](03_recurring_service_output.json) | `99047dd43e16edc0c4f59ddbcbc94bb28d9890c964dfcc31ecd22613931bed23` |

Every output is a schema-valid production-row projection created from a real
local `GenerationResult`. The added `sampleProvenance` object is a repository
annotation. It makes explicit that no Apify run, Store publication, or customer
charge occurred.

## Input contract

- Use exactly one of `invoice` or `invoices`.
- Supply quantities, prices, and tax rates as JSON strings such as `"19.00"`.
- Use ISO `YYYY-MM-DD` dates, ISO 4217 currency codes, ISO country codes, and
  UNECE unit codes.
- Each seller and buyer needs a tax, VAT, or registration identifier.
- The complete snapshot is [`actor_input_schema.json`](actor_input_schema.json).

## Dataset output contract

The production result row separates processing from technical conformance:

| `processingStatus` | `conformanceStatus` | Meaning |
|---|---|---|
| `SUCCEEDED` | `ACCEPTED` | Generation and every pinned local technical layer passed |
| `SUCCEEDED` | `REJECTED` | Generation completed but at least one required technical rule failed |
| `FAILED` | `NOT_EVALUATED` | Input, engine, storage, budget, or runtime failure prevented a decision |

Schema files:

- [`actor_dataset_schema.json`](actor_dataset_schema.json) is the complete Apify
  Actor dataset schema snapshot.
- [`dataset_record.schema.json`](dataset_record.schema.json) is the Actor
  schema's `fields` contract as standalone JSON Schema.
- [`VALIDATION_REPORT.json`](VALIDATION_REPORT.json) records local generation,
  JSON parsing, input-schema, dataset-schema, and artifact-hash checks.

## Pay-per-event contract

The intended release price is exactly **$0.01 per `invoice-generated` event**.
One event applies only after one invoice passes the pinned validation stack and
its artifact and evidence have been delivered. Invalid input, rejected
artifacts, storage failure, and budget refusal are not intended to charge that
event.

The Actor is private and its release is pending, so this is not a claim about a
currently public Store offer. Check the
[Store page](https://apify.com/kamerozkan/zugferd-facturx-pdf-generator) for the current price,
build, limits, and publication state when it becomes public.

## Evidence boundaries

`ACCEPTED` means pinned offline technical preflight only. It does not mean:

- transmitted to Peppol, KSeF, SdI, a tax authority, or a recipient;
- accepted, registered, cleared, or assigned an official network identifier;
- digitally signed, archived, paid, booked, or legally approved;
- semantically identical to source data outside the supported input contract.

The output keeps these boundaries explicit with `transmitted: false`,
`acceptedByNetwork: null`, `networkIdentifier: null`, `signed: false`, and
`archived: false`.

## E-invoice generator family

All five repositories use one normalized invoice-intent model and product-specific
serializers and validators. The sibling links below are intended public GitHub
locations and may return 404 while publication is pending.

| Generator | Intended GitHub repository | Intended Apify Store URL |
|---|---|---|
| XRechnung Invoice Generator | [sample repository](https://github.com/kamerozkan/xrechnung-invoice-generator-sample) | [release-pending Actor](https://apify.com/kamerozkan/xrechnung-invoice-generator) |
| Peppol UBL Invoice Generator | [sample repository](https://github.com/kamerozkan/peppol-ubl-invoice-generator-sample) | [release-pending Actor](https://apify.com/kamerozkan/peppol-ubl-invoice-generator) |
| ZUGFeRD and Factur-X PDF Generator | [sample repository](https://github.com/kamerozkan/zugferd-facturx-pdf-generator-sample) | [release-pending Actor](https://apify.com/kamerozkan/zugferd-facturx-pdf-generator) |
| FatturaPA Invoice Generator | [sample repository](https://github.com/kamerozkan/fatturapa-invoice-generator-sample) | [release-pending Actor](https://apify.com/kamerozkan/fatturapa-invoice-generator) |
| KSeF FA(3) Invoice Generator | [sample repository](https://github.com/kamerozkan/ksef-fa-invoice-generator-sample) | [release-pending Actor](https://apify.com/kamerozkan/ksef-fa-invoice-generator) |

## Data and license

Read [`DATA_NOTICE.md`](DATA_NOTICE.md) before using the fixtures. All invoice
values are synthetic. The MIT License covers this repository's original
documentation, JSON fixtures, and schema packaging. It does not relicense
standards, validator software, specifications, names, marks, or third-party
rulesets.

Standard: `ZUGFeRD / Factur-X` `2.5 / 1.09`  
Pinned ruleset: `Mustang 2.24.0 ZF_250 plus veraPDF 1.30.2`
