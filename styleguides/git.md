# `git styleguide`

Version control is a must in web development nowadays. These are a set of Git best practices we adopt at AMARO to make our development process easier.

## Table of contents

- `.gitignore`
- Branches
  - The one branch to rule them all
  - Testing branches
  - Naming conventions
  - Deleting branches
  - Feature branches
- Commit messages
  - General rules
  - Language
  - Tense
  - Emojis
    - Emoji commit list
- Releases
- Files
- Pull requests
  - Good practices
  - Title
  - Description
  - Size
  - Comments

## `.gitignore`

- The `.gitignore` is a config file where we specify which files should **not** be included in version control.
- We should have one `.gitignore` file in then root directory, rather than multiple accross all directories.
- Common best practices include ignoring cache, logs and binary data.
- Images should only be added when it's really necessary as they make the project big and too hard to clone.
- Third party development dependencies libraries are normally ignored too. That's why `/node_modules` is ignored by default.
- IDE project files should be added to the `.gitignore` file.

## Branches

### The one branch to rule them all

- The main branch is `master`. No direct changes are accepted into `master`.
- The only way to update `master` is from an approved _pull-request_.

### Testing branches

In the `AECP` project we use a 3 step process to test our builds.

- `test`: This is used for experimental stuff. The remote is: [test.amaro.com](http://test.amaro.com)
- `dev`: This is the main development branch. The remote is: [dev.amaro.com](http://dev.amaro.com)
- `beta`: This is the final testing environment. The remote is: [beta.amaro.com](http://beta.amaro.com)

### Naming conventions

- Choose short and descriptive names.
- Use dashes to separate words.
- Identifiers from the _issue tracker_ system are also good candidates for use.

### Deleting branches

- Delete your branch from the upstream repository after it's merged (unless there is a specific reason not to).

    # Delete a remote branch
    git branch -D old-feature-branch
    git push <remote> :old-feature-branch

### Feature branches

- If you're working on a big feature, do it in a new branch to avoid merge problems when pulling work from remote.

    # Working in a new branch
    ~ (dev) git checkout -b my-new-feature
      ... Do stuff here
    ~ (dev) git add -A
    ~ (dev) git commit -m "Technical bla bla bla"

## Commit messages

### General rules

- Always commit your work.
- Each commit should be a single logical change. Don't make several logical changes in one commit, it's hard to keep track of them.
- Commit early and often. Small, self-contained commits are easier to understand and revert when something goes wrong.
- Commits should be ordered logically. For example, if commit X depends on changes done in commit Y, then commit Y should come before commit X.
- Split your commit message in title and description. Keep your commit title under 72 characters.

### Language

- Every commit message, pull-request title or issue discussion must be in **english**.

> **Reason:** As we work in a multicultural environment, it is good to document in english as we make it easier for everyone to understand and collaborate.

### Tense

- Do not use past or present continuous tenses for commit messages, those should written using imperative present.

    Add feature xpto.

> **Reason:** This is a recommendation from [Git itself](http://git.kernel.org/cgit/git/git.git/tree/Documentation/SubmittingPatches?id=HEAD#n111).

### Emojis

- As the world gets more collaborative and social, several services are starting to use emojis in a professional way.
- Tools we use daily, like Slack, Asana and Bitbucket already support them.
- Use emojis to start the message when it's applicable (Ref.: [Atom contributing guidelines](https://github.com/atom/atom/blob/master/CONTRIBUTING.md)).

#### Emoji commit list

- :art: `:art:`: When improving format/structure of the code.
- :racehorse: `:racehorse:`:When improving performance
- :books: `:books:`: When writing docs
- :bug: `:bug:`: When fixing a bug
- :station: `:station:`: When fixing merge problems
- :fire: `:fire:`: When removing code or files
- :arrow_up: `:arrow_up:`: When upgrading dependencies
- :arrow_down: `:arrow_down:`: When downgrading dependencies
- :shirt: `:shirt:`: When removing linter warnings
- :atm: `:atm:`: When adding automation tasks
- :lipstick: `:lipstick:`: When improving UI/cosmetics
- :construction: `:construction:`: WIP (Work in progress)
- :gem: `:gem:`: New release
- :sparkles: `:sparkles:`: When introducing new features
- :apple: `:apple:`: When fixing something on iOS/Mac OS X
- :checkered_flag: `:checkered_flag:`: When fixing something on Windows
- :penguin: `:penguin:`: When fixing something on Linux
- :white_check_mark: `:white_check_mark:`: When adding tests
- :wrench: `:wrench:`: When updating config settings

## Releases

- Until we have an automated process the `CHANGELOG.md` file **must** be updated manually before each new release.
- When releasing a new version, use the appropriate Semver number ID and write a commit message in the following format:

    git commit -m ":gem: Release vX.Y.Z"

### Major releases

- Major releases are done when a new part of the app is added to the platform (Cart, Minha Conta, Checkout, etc)

### Minor Releases

- Minor releases are done when a new component is added to the platform (Header, Footer, Newsletter Signup Box, etc).

### Patch releases

- Patch releases are done very often when upgrading a new component, fixing a bug or adding tests to an existing component.

## Files

- Do **not** commit big files and binaries unless they **are required**. Big files lead to big git history and it will be a pain for others to use the repo.
- Whenever possible use image sprites. If you can't upload the image to our server using the [AMARO ADM](https://amaro.com/adm/cms/files/upload).

## Pull-Requests

### Good practices

- Never edit your `master` branch directly.
- **None _pull-requests_ with changes on `master` will be accepted.**
- Always push your changes to the corresponding branch on `origin`.
- Before pushing your branch, update it with the latest changes from `origin`. This reduces drastically the complexity of merging conflicts.

### Title

- Make clear what you're fixing with this PR.
- Keep it under one line length (72 characters max).
- Rules for writing good git commit messages applies here.

### Description

- Use the description to clarify any doubts about the bug, when/where it happened and how it was fixed.
- Be clear, there's no need to write a book in the description, but you're not paying for every character typed.

### Size

- To make code reviews easier, it's highly recommended that you avoid massive PR's.
- If you're working on a big feature, do some effort to break it into smaller pieces that can be merged into `dev` (and, of course, don't break it).
- Commit often inside your PR to keep your code easy to understand.
- If the feature's commit history gets messy, use [interactive rebase](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase-i/) to remove or squash unnecessary commits.

### Comments

- Comments must be done in english.
- Code reviewers must leave a comment before approving or merging a PR.
- Each comment must have, at least, one of the following tags:
    - `Required`: Something that must be fixed before merge.
    - `Nice to have`: It would be good to include this now rather than later.
    - `Question`: What does this do?
    - `Approved`: Everything seems to be ok. Approved for merge.
