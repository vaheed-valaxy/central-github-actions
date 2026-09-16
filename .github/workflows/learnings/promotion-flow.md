## DEV -->  QA
```text
                    DEV
                     │
                     │ read digest
                     ▼
              Verify DEV ECR
                     │
                     ▼
             Copy exact digest
                  DEV → QA
                     │
                     ▼
             Verify QA digest
                     │
                     ▼
       ┌─────────────────────────────┐
       │ Does open PR exist?         │
       └──────────────┬──────────────┘
                      │
            ┌─────────┴─────────┐
            │                   │
           NO                  YES
            │                   │
            ▼                   ▼
      Create stable       Checkout existing
        branch              stable branch
            │                   │
            └─────────┬─────────┘
                      ▼
              Update QA digest
                      │
                      ▼
               Commit change
                      │
                      ▼
                  Push branch
                      │
                      ▼
          Create PR only if needed
```
