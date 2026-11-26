# Vignettes plugins

The plugins of [Vignettes](https://vignettes.io), `vignettes-decks` and `vignettes-themes`, are published from the repository [ShallowRed/vignettes](https://github.com/ShallowRed/vignettes/tree/main/plugins). This repository is archived.

Both repositories declare the Claude Code marketplace `vignettes`. To install the plugins from the repository of Vignettes, in Claude Code:

```text
/plugin marketplace remove vignettes
/plugin marketplace add ShallowRed/vignettes
/plugin install vignettes-decks@vignettes
```

For the other agents, with GitHub CLI:

```bash
gh skill install ShallowRed/vignettes writing-decks --agent codex --scope user
```
