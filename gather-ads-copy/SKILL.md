---
name: gather-ads-copy
description: Gather and verify dealership specials into ad-ready copy data. Use when a user asks to collect promo terms from a dealer specials page, choose top models by inventory and deal quality, validate terms against vehicle detail pages (VDPs), and deliver structured output such as CSV rows for ad operations.
---

# Gather Ads Copy

## Overview

Collect specials from dealer websites, select the required models using explicit ranking rules, verify promotional terms against model detail pages, and output clean ad-copy data in table or CSV format.

## Workflow

1. Identify source inputs.
- Confirm the specials URL.
- Load any local reference files the user provided (CSV templates, screenshots, prior exports).
- Preserve requested output format and column order.

2. Extract candidate specials.
- Capture, per model: year, make/name, trim/model, lease-from monthly amount, term months, due-at-signing/down payment, APR, VIN, MSRP, residual, offer expiration, and disclaimer text.
- Keep the direct specials card URL and candidate VDP URL for each row.

3. Rank and select models.
- If the user asks for top 5 with split logic, apply:
- Select 4 distinct models with the highest inventory.
- Select 1 additional distinct model with the best deal based on lowest APR, then lowest monthly lease price as tie-breaker.
- Never duplicate a model in the final five.

4. Verify against model detail pages (VDPs).
- Prefer exact VIN match between specials and VDP.
- If exact VIN is unavailable, verify closest same-model VDP and mark verification status clearly.
- Confirm APR, MSRP, and trim consistency where possible.
- Record any mismatch or missing field explicitly; do not silently fill unknown values.

5. Normalize values for output.
- Use consistent currency formatting (`$X,XXX`) and numeric APR (`0.0`, `2.9`).
- Store dates in ISO format (`YYYY-MM-DD`) unless user asks otherwise.
- Keep legal/disclaimer language concise but complete for lease structure and lessee responsibility.

6. Deliver output.
- Provide a concise summary of selection logic used.
- Provide final data as CSV-ready rows in requested file name and location.
- Include source URLs used for verification.

## Quality Rules

- Use exact values from source pages; avoid inferred values unless required.
- When inference is unavoidable, label it explicitly as inferred.
- Keep one row per selected model.
- Keep output auditable: include verification note and model details URL.

## Fast Fallbacks

If live site access is unavailable:
- Use provided local references (prior CSV/image) as seed data.
- Mark each row as `Unverified (live site unavailable)` unless independently validated.
- Continue producing the requested file format so downstream ad ops can proceed.

## Reference Files

- Output schema and recommended columns: `references/output-schema.md`
