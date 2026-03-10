# Output Schema

Use this default column order unless the user provides a different template.

1. Type
2. Year
3. Name
4. Model
5. Lease price
6. Months
7. Due At sign
8. Down
9. APR
10. VIN
11. MSRP
12. Residual
13. Offer Expired Date
14. Lease Structure / Lessee Responsible Info
15. Model Details URL
16. Verification

## Verification Status Values

Use one of these labels in `Verification`:
- `Exact VIN/APR/MSRP match found on VDP`
- `Exact VIN VDP not found; model/APR pattern verified on nearest VDP`
- `Unverified (live site unavailable)`

## Deal Ranking Rule

When asked for "best deal based on Price and APR":
- Rank by lowest APR first.
- Break ties by lowest monthly lease price.
- If still tied, prefer lower due-at-signing.
