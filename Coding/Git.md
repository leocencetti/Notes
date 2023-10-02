# Rebase 

## `--onto` #git

The `--onto` flag can be used to specify which commit should be used as branching point. Given a git history like this:

```mermaid
%%{init: {'theme': 'neutral' } }%%
gitGraph
   commit id: "A"
   commit id: "B"
   commit id: "C"
   branch develop
   commit id: "D"
   commit id: "E"
   commit id: "H"
   commit id: "I"
   checkout main
   commit id: "F"
   commit id: "G"
```
We can rebase the history of the branch/ref `develop` such that commit `D` is substituted by commit `F` with the command:

```
git rebase --onto F D develop
```

This will result in an updated git history that looks like this:
```mermaid
%%{init: {'theme': 'neutral' } }%%
gitGraph
   commit id: "A"
   commit id: "B"
   commit id: "C"
   commit id: "F"
   branch develop
   commit id: "E'"
   commit id: "H'"
   commit id: "I'"
   checkout main
   commit id: "G"
```
> **Note**
> Commits `E`, `H`, and `I`, have been rewritten as  `E'`, `H'`, and `I'` and commit `D` has disappeared

> **Note**
> If the reference (`develop` in this example) is omitted, the current HEAD will be used instead

> **Note**
> Passing `I` as reference has a different result: the branch develop will remain intact, with a new detached HEAD being created at commit `I'`
## `--rebase-merges` #git

The `--rebase-merges` flag can be used to keep and rebase merges as well. Starting from a git history like this:

```mermaid
%%{init: {'theme': 'neutral' } }%%
gitGraph
   commit id: "A"
   commit id: "B"
   branch develop-1
   commit id: "C"
   branch develop-2
   commit id: "D"
   checkout develop-1
   commit id: "E"
   merge develop-2
   checkout main
   commit id: "F"
   commit id: "G"
```
Rebasing commit `B` in `develop-1` onto `F` in `main` with the `--rebase-merges` flag will give:

```mermaid
%%{init: {'theme': 'neutral' } }%%
gitGraph
   commit id: "A"
   commit id: "B"
   commit id: "F"
   branch develop-1
   commit id: "C"
   branch develop-2
   commit id: "D"
   checkout develop-1
   commit id: "E"
   merge develop-2
   checkout main
   commit id: "G"
```
