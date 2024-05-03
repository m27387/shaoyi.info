---
title: "The Git Cheatsheet"
date: 2024-04-30
description: "Git cheatsheets I found on the Internet."
# slug: "cheatsheet"
tags: ["hugo", "git", "github", "cheatsheet"]
series: ["Jumped on the Hugo bandwagon"]
series_order: 8
---

This is an intergration for the Git cheatsheets I found on the Internet. Also there will be some shortcodes and markdown practices. I use [Mermaid](https://mermaid.js.org/syntax/gitgraph.html#base-theme), a JavaScript based diagramming and charting tool that renders Markdown-inspired text definitions to create and modify diagrams dynamically, to visualize how exactly Git work. Mermaid is also a built-in shortcode of [Blowfish](https://github.com/nunocoracao/blowfish) theme.

## Cheatsheet from [GitHub](https://education.github.com/git-cheat-sheet-education.pdf)
### Before Start
There are GUI applications from GitHub for both [Windows](https://windows.github.com) and [macOS](https://mac.github.com). For CLI, users can use [Homebrew](https://formulae.brew.sh/formula/git) to install Git easily on the macOS system. For the record, I switched from [Sublime Text](https://www.sublimetext.com/) to [VS Code](https://code.visualstudio.com/), which works perfectlly well for me.
### Hop on
Git is all about [version control](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control). Developer should set up the name and email for later recognition. Also set up the line coloring for easy reviewing.
{{< highlight terminfo>}}
git config --global user.name "[firstname lastname]"
git config --global user.email "[valid-email]"
git config --global color.ui auto
{{< /highlight >}}

### Initialization
The first step at this phase is to establish a local repository for your project by ``git init``. It is always better to stand on the shoulders of the giants by using ``git clone [url]`` to copy a sound project and modify it.

### Staging

## Git Diagram
{{< mermaid>}}
%%{init: { 'logLevel': 'debug', 'theme': 'forest' } }%%
      gitGraph TB:
        commit
        branch hotfix
        checkout hotfix
        commit
        branch develop
        checkout develop
        commit id:"ash" tag:"abc"
        branch featureB
        checkout featureB
        commit type:HIGHLIGHT
        checkout main
        checkout hotfix
        commit type:NORMAL
        checkout develop
        commit type:REVERSE
        checkout featureB
        commit
        checkout main
        merge hotfix
        checkout featureB
        commit
        checkout develop
        branch featureA
        commit
        checkout develop
        merge hotfix
        checkout featureA
        commit
        checkout featureB
        commit
        checkout develop
        merge featureA
        branch release
        checkout release
        commit
        checkout main
        commit
        checkout release
        merge main
        checkout develop
        merge release
{{< /mermaid>}}

## Flowchart by [Cerphippo](https://medium.com/@myitcerts995/git-cheat-sheet-guys-f26e2d96732c)
{{< mermaid >}}
flowchart BT
  subgraph Local
    direction LR
    subgraph id1[Working directory]
    end
    subgraph id4[ ]
      subgraph Staging
      end
      subgraph Stash
      end
    end
    subgraph id5[ ]
    direction TB
      subgraph id2[Remote branch tracking]
      end
      subgraph id3[Local repository]
      end
    end
  end
  subgraph Remote
  end
  
  id2[Remote branch tracking] ==git merge==> id1[Working directory]
  Remote ==git fetch==>id2[Remote branch tracking]
  Staging ==git reset==> id1[Working directory]
  Remote ==git pull==> id1[Working directory]
  id1[Working directory] ==git add==> Staging
  Staging ==gti commit==> id3[local repository]
  id3[local repository] ==git push==> Remote
  id1[Working directory] ==git stash==> Stash
  Stash ==git stash apply==> id1[Working directory]
  Stash ==git stash pop==> id1[Working directory]

{{< /mermaid >}}