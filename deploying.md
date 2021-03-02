# Releasing

_Note that the terms `publish` and `release` can be used interchangeably._

### What contributors have to do:
When you make a change to a component's source code (not stories, specs, or docs), before merging your branch you should run `yarn changeset`. This will prompt you to:
- indicate if changes were patch/minor/major for each modified package
- enter a release message

This generates a new file (`/.changeset/some-random-name.md`) that contains the list of packages that were modified and the scope of their changes (patch/minor/major).

The file should be committed and pushed.

### What PR reviewers have to do:

Reviewers should confirm the author ran `yarn changeset` -- that is, the PR includes `/.changeset/some-random-name.md`.

If it does not exist, there is a "Github Action" bot [https://github.com/apps/changeset-bot] running on the Paprika repo that looks for this file.  The bot will add a message to the PR with a link that generates such a file. The reviewer should click the link, confirm the scope (patch/minor/major) and create the file.



### CI:

#### Pre-release on Semaphore
  - runs every 6 hours (8am, 2pm, 8pm, 2am)
  - runs `.semaphore/pre-release.yml` script, which:
    1. runs `yarn changeset pre enter next` (enters "pre-release" mode, where versions are appended with `next`)
    2. runs `yarn changeset version` (which reads `/.changeset/*.md` and for each changed package: updates the version in package.json, updates its changelog.md)
    3. runs `git add .` and `git commit`
    4. runs `yarn changeset publish` (which publishes changed packages to npmjs.org, deletes `/.changeset/*.md`)
    5. pushes the changes to master
  
If any changes are merged to master while step 2 or 3 is in progress, step 5 will fail.  A Paprika administrator would need to pull the latest master and manually do the steps above in order to do a release.

#### Release on Semaphore
  - runs once a week (Saturday at noon?)
  - runs `.semaphore/release.yml` script, which:
    1. runs `yarn changeset pre exit` (exits "pre-release" mode, so versions are _not_ appended with `next`)
    2. runs `yarn changeset version` (which reads `/.changeset/*.md` and for each changed package: updates the version in package.json, updates its changelog.md)
    3. runs `git add .` and `git commit`
    4. runs `yarn changeset publish` (which publishes changed packages to npmjs.org, deletes `/.changeset/*.md`)
    5. pushes the changes to master

If any changes are merged to master while step 2 or 3 is in progress, step 5 will fail.  A Paprika administrator would need to pull the latest master and manually do the steps above in order to do a release.

### How all these tools help

#### If we used nothing
  - it would be very slow and tedious to develop and release:
    - when you ran `yarn install`, each package would have its own `node_modules` folder with its own dependencies (even if there are duplicates across packages). This is very slow when developing.
    - imagine you are working on Paprika and you update the `<Button />`, then you worked on the `<OverflowMenu />` (which uses the `<Button />`).  To see the new `<Button />` in the `<OverflowMenu />`, you would have to update the Button's version in `OverflowMenu/package.json`
    - when releasing you would have to manually bump the versions in `Button/package.json` (and optionally every package that used the `<Button />`) and `OverflowMenu/package.json` (and optionally every package that used the `<OverflowMenu />`)
 

#### Yarn Workspaces
> Yarn Workspaces make it easier to develop on a repo with multiple packages.
 
When you run `yarn install`, all dependencies are installed in the _root_ `node_modules` folder, making it run much faster (*except if a package used a different version of a component, in which case it used its own `node_modules` folder).
  

#### Lerna
> Lerna transpiles ES6 with Babel and makes it easier to bump package versions.  It can also generate changelogs and publish, but we are using Changeset for this now.

  - link packages in a monorepo (`lerna bootstrap`), i.e. for each package:
    - runs `npm install` (installs 3rd-party dependencies)
    - runs `npm run prepublish` (generates changelogs)
    - runs `npm run prepare` (re-creates `/lib`, generates `readme.md`, generates type definitions, runs `pretranspile` step for each package -- e.g. the `<L10n />` component uses this step to convert translations from `.yml` to `.js`)
  - bumps changed package versions (since last release to npmjs.org) and releases (`lerna publish --from-package`)


#### Changeset
> Changeset is just the name of a command line tool that: bumps package versions, updates package changelogs and releases all modified packages to npmjs.org.

1. Before merging your code, you run `yarn changeset` to automatically create a file in the `/.changesets` folder.  Each file will contain:
- a list of packages
- if the package had a patch/minor/major change
- some text that is used for the release notes

2. When releasing your packages, you run `yarn changeset version` which:
- reads all of the files in `/.changesets`
- sensibly updates each packages version in package.json (e.g. if one commit to a component did a "patch" update, and another did a "minor" commit, it will only bump the "minor" version -- not both)
- updates its `changelog.md`

3. Then run `yarn changeset publish` which:
- publishes to npmjs.org
- deletes `/.changesets`
You should then commit these changes (so the updated versions and changelogs are merged).


