# workflows

This repository contains workflows that can be reused in other repositories.

## Contributing

You can add a new workflow by creating a new file in `.github/workflows`.

The file must be prefixed with one of:
- `checking_` if the workflow's main responsibility is verification (runs linting / checks formatting / runs tests)
- `doing_` if the workflow's main responsibility is to execute some action (build a container / deploy / interact with GitHub)
- `NO_REUSE_` if the workflows is to be used only in this repository

**Testing**

To test your workflow, you should use `git mark-experimental` to mark your current commit with the `experimental` tag.

> [!CAUTION]
> If multiple folks are adding workflows, the `experimental` tag might be moved out from under you.
> In that case, just create your own tag. And don't forget to clean up afterward, please.

Then, you can refer to the workflow in the repo you intend to use it. For example,

```yaml
close_issue:
    needs: fast-forward-merge
    permissions:
        issues: write
        contents: write
    uses: thetechcollective/workflows/.github/workflows/doing_close_issue.yml@experimental # <---- Note the experimental ref
    with:
        user_name: "GitHub Action: ready"
        user_email: "tt-ready@thetechcollective.dev"
```

**Stabilizing**

When you are done with testing the workflow, you should
1. deliver the changes to `main`
2. `git sweep`
3. `git mark-stable`
4. Use the `stable` reference instead of the experimental reference in your repo

> [!NOTE]
> If you do not pin your actions to the stable tag, you are risking other folks' experiments messing with your actions.
