## DEV -->  QA Promotion Flow
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
               ┌──────┴──────┐
               │             │
         No existing PR   Existing PR
               │             │
               ▼             ▼
          gh pr create   gh pr edit
               │             │
               └──────┬──────┘
                      ▼
               Same stable PR
         
```
```text
One service
    ↓
One stable branch
    ↓
One open PR
    ↓
New DEV image
    ↓
Update same branch
    ↓
Update same PR
```

**If PR #1 is still open:**  
```text
Image A → PR #1
Image B → same branch → PR #1 updated to B
Image C → same branch → PR #1 updated to C
```

**If PR #1 has already been merged:**  
```text
Image D → same stable branch recreated from main → PR #2
```

