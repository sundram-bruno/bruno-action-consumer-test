# bruno-action-consumer-test

End-to-end consumer test for the [`sundram-bruno/bruno-run-action`](https://github.com/sundram-bruno/bruno-run-action) composite action.

Validates that the action behaves correctly when used the way a real Marketplace consumer would use it:
- `uses: sundram-bruno/bruno-run-action@main`
- Real network calls to `httpbin.org` (not a local mock)
- All three reporters (`--reporter-junit`, `--reporter-html`, `--reporter-json`) requested in `command`
- Outputs (`exit-code`, `passed`, `failed`, `total`, `duration-ms`, `report-{junit,json,html}`) asserted
- Reports uploaded as a workflow artifact

## Layout

```
.
├── .github/workflows/api-tests.yml   ← workflow that consumes the action
└── bruno/                            ← collection root passed via working-directory
    ├── bruno.json
    ├── environments/ci.bru           ← baseUrl: https://httpbin.org
    ├── get.bru                       ← GET /get + query-string echo
    └── headers.bru                   ← GET /headers + custom header round-trip
```

## Triggers

- Push to `main` → workflow runs
- PR to `main` → workflow runs
- Manual dispatch via Actions tab

## Disposable

Delete this repo once the upstream `usebruno/bruno-run-action` is published to Marketplace.
