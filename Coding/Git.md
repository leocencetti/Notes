## Rebase `--onto`
### Before
```mermaid
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
### Command
```
git rebase --onto F D develop
```

In words, that is:

_rebase the history of the ref `develop` such that the children of commit `D` are based onto commit `F`_

> **Note**
> If the reference (`develop` in this example) is omitted, the current HEAD will be used instead

> **Note**
> Passing `I` as reference has a different result: the branch develop will remain intact, with a new detached HEAD being created at commit `I'`
### After
```mermaid
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
> Note that commits `E`, `H`, and `I`, have been rewritten as  `E'`, `H'`, and `I'`

