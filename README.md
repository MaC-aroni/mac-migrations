# mac-migrations

**The MaC repo**: every migration Prayerwell Health runs is a `migration.yaml` here, reviewed
like any other code. MaC (Migration as Code) builds, rehearses and deploys what's merged.

## How a migration gets here

1. An engineer asks MaC to plan a migration, for example "Migrate ClaimsAdjudicationService to
   AWS".
2. MaC's agents read the company knowledge base in Confluence (standards, policies, service
   docs, approvers) and write the pipeline: the steps, their stages, the approvals with
   justifications, and citations to the docs each part came from.
3. It arrives here as a **pull request** in `migrations/<name>/migration.yaml`. CI checks it
   with MaC's validator.
4. **Engineers review it** and change anything they disagree with, including which steps'
   code the LLM may write (`codegen: llm`) and which the engineers write themselves.
5. Once merged, MaC can Build, Rehearse and Deploy it.

## Rules

- `main` is protected: changes only through a pull request with **one approving review**, and
  the `validate` check must pass.
- One folder per migration: `migrations/<name>/migration.yaml`.
- The spec format is `mac/v0.3`; see
  [MaC's runner docs](https://github.com/MaC-aroni/deployed-on-a-prayer/blob/main/docs/runner.md).
