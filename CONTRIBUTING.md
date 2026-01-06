# Contributing to BSG JavaScript/TypeScript SDK

## READ-ONLY REPOSITORY

**This is a READ-ONLY repository!**

This repository is automatically generated and synchronized from a private monorepo. All code here is auto-generated from OpenAPI specifications.

## How to Contribute

### For BSG Team Members

1. **DO NOT** make any changes directly to this repository
2. **DO NOT** create pull requests to this repository
3. **DO NOT** push any commits to this repository

All changes must be made through the private monorepo:

```
github.com/bsgworld/bsg-sdk (private)
         ↓
   GitHub Actions
         ↓
github.com/bsgworld/js-sdk (this repo)
```

### Workflow

1. Clone the private repo: `git clone git@github.com:bsgworld/bsg-sdk.git`
2. Make changes to OpenAPI specs or templates
3. Generate SDK: `./generator/generate-sdk.sh typescript`
4. Commit and push to private repo
5. Create a tag: `git tag js-v1.0.0 && git push origin main --tags`
6. GitHub Actions will automatically sync to this public repo

### For External Contributors

If you found a bug or want to suggest an improvement:

1. Open an issue in this repository describing the problem
2. Our team will review and implement the fix in the private repo
3. Changes will be automatically synchronized here with the next release

## Questions?

Contact us at support@bsg.world
