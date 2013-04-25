% *Merge* made by *octopus*
% git workflows

---

# Before we start {.alone}

<!-- This is not server-side git, or git for project maintainers -->

---

# Goals

- Not to dictate any specific workflow
- Know your tools well
- Think about how you communicate to a team, or a client, or a future developer
    - not just your present self

---

# Specific Goals

- Readable commit histories <!-- messages, tags -->
    - A form of documentation
- Isolating functional changes, without losing granularity
- Communicating the current state of development <!-- branches -->

<!-- Another level of communication to future developers -->

---

# Today's Theme

What you do in private is your own business.

1. Branch, stash, and commit freely.
2. Clean up after yourself.

---

## And a quick review...

- Working area, Staging (Index), Repository, Remotes
- Once committed, you are safe. __(Unless you're not.)__
- Read git's feedback messages
- Man pages; _Pro Git_

<!--code-->

    git help [command]

---

# Tools

- Command line

---

# Other Tools

- Visualizations: gitx, gitk, ...?
- Other tools **(I'm looking at you, github-for-mac)** are leaky
- Integrated Tools & APIs: Keep in mind when crafting commit messages

<!-- code -->

    Fix the foo in the blazz [#132]

---

# Config

- set your editor
- aliases
    - and tab completion
    - but don't rely completely on your env <!-- fucking "gs" -->

<!--code-->

    [alias]
    co = checkout

---

# Commands {.alone}

---

## Branch

...is the single most powerful feature of git, compared to even other DVCSs **(Don't believe the Hg Hype)**

- Local branching is cheap: go crazy <!-- it will improve your other  -->
- Shared feature branching (pushed to origin)
- Keeping a branch clean and deployable
    - `master` or `deploy`

---

## Branch

- So, do we think differently about web vs. iOS vs...?
    - Deployability
    - ignores
    - IDEs

---

## Branch

- remote (origin) branches; tracking
- Communicate deletions

<!-- -u == set-upstream -->

    git checkout -b mybranch
    git push -u origin mybranch 
    git checkout -t origin/yourbranch
    git push heroku dev:master
    git push origin :mybranch # DELETE

---

## Stash

- I think of stashes as temporary
- If I don't pop within an hour, I won't be using it
- One use case: moving to a new branch
- Naming can be helpful, but see above
- For persisted changes, I prefer `branch` + `commit`
- Tip: stash before `reset --hard`
- As always, pay attention to the branch you're on

---

## Stash

    git stash save [Your message here]
    git stash pop

    git stash list
    git stash show stash@{2}
    git stash drop stash@{2}

---

## Tag

- All releases should be tagged
- Other milestones (CoreData schema changes)
- Annotate: `-a`
- You can always tag later; change tags; etc. <!-- The one exception to rewriting history? -->

<!--code-->

    git tag -a v0.1.2 -m "Beta release with new foobars"
    git tag -a "CoreData Migration 1.1" ecacf50
    git push --tags

---

## Rebase

Rebasing is the tool that lets you enjoy frequent local commits without subjecting others to your insane commit histories.

- Goal: Readable histories
- Goal: isolation of changes for finding problems, regressions (e.g., bisect)

---

## Rebase

- NEVER rewrite history that has been pushed somewhere accessible to others
- `pull --rebase` obscures "true" history, but is cleaner
- Otherwise, *always* use `-i`

<!-- code -->

    git pull --rebase
    git rebase -i HEAD~~

---

## Rebase

More on granularity vs. clarity...

- Frequent commits to avoid conflicts early in project
- Changes that should happen alone
    - whitespace
    - move files

---

## Reflog

- A history of everything you've done
    - commits
    - checkouts
    - merges
    - rebases
    - (Note! Not stashes)

---

## Reflog

- This is often your recourse when something went wrong

<!-- code -->

    git reflog

---

## Bisect

- Goal: find regressions
- Binary search on functional changes
- Handy when tracking things down in other people's code

<!--code-->

    git bisect start
    git bisect [good|bad]
    git bisect reset

    git bisect run [command] # auto-find the bad commit

---

## Ignore

- `.gitignore` files are out there
- Generated or compiled files ...usually taken care of.
    - e.g., CSS, built files, `/bin`
- ENV (passwords, security)

---

## Ignore

- Design source files; usually stored outside the directory
- But may make sense to include,
    - as long as they're not part of the deployable slug
    - Perforce? Adobe? Dropbox?

---

# Comments {.alone}

---

## Commit Comments

- Short, direct single line
- Multiple lines (after space) if needed
- API integrations (commit hooks)

<!-- code -->

    git commit --amend

---

# Goals, rehashed

- Readable commit history
- Good commenting
- Rebase vs. merge
- Tradeoff between readability and granularity: this is an art

---

# Questions? {.alone}

---

# Rebase Demo {.alone}


<!-- @ Upstart Labs, 4/25/2013 -->
