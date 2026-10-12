# Same Operation, Different Permission: Evaluating Whether Guardrails Honor Authorization

Anonymous ACL submission

## Quick Start

```bash
pip install -r requirements.txt
export OPENAI_API_KEY="YOUR_API_KEY"
# Optional: use an OpenAI-compatible endpoint
# export OPENAI_BASE_URL="http://localhost:8000/v1"
python eval.py --dataset Egbertjing/authorizationpairs --model YOUR_MODEL --limit 10
```

Remove `--limit 10` to evaluate all 160 language test cases. Use `--track native`
for native-policy cases or `--track all` for both tracks. Predictions are saved to
`predictions.jsonl`.

## Scores

- **Accuracy:** valid decisions matching the reference, divided by all cases.
- **Authorized approval rate:** lawful requests receiving a valid `ALLOW`.
- **Unauthorized approval rate:** forbidden requests receiving a valid `ALLOW`.
- **Invalid rate:** API errors, non-stop terminations or non-label responses.
- **Contrast success:** all decisions correct within a complete group containing
  both reference labels. Groups truncated by `--limit` are excluded.

Scores evaluate authorization decisions. Rates are fractions, and missing
denominators produce `null`.
