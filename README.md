# workflows
Reusable, callable workflows


Run the following to include the `.gitconfig``

```bash
git config --local --get include.path | grep -e ../.gitconfig >/dev/null 2>&1 || git config --local --add include.path ../.gitconfig
```