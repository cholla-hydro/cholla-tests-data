# CHOLLA Tests Data

This repository contains the test data used by Cholla's tests and is intended to
function as a submodule of the primary
[Cholla repository](https://github.com/cholla-hydro/cholla).

## Dependencies

- Git LFS, tested with v3.1.2

## Usage

Since this repo just contains data that the Cholla tests use it should be cloned
as a submodule to Cholla. This section is not a complete introduction to Git LFS
or submodules, please see the Atlassian tutorials for more details. Throughout
this section I will often refer to Cholla as the "parent" repo and
cholla-tests-data as the "submodule" so that the discussion is more general.

- [Git LFS Tutorial](https://www.atlassian.com/git/tutorials/git-lfs)
- [Git Submodules Tutorial](https://www.atlassian.com/git/tutorials/git-submodule)

### Git LFS Notes

Git LFS works by only downloading LFS files when they're checked out, so when
you clone you only get the current version of those files rather than their
entire histories.

Note that git garbage collection is not automatically run on LFS files. If you
wish to run garbaga collection for old LFS files run `git lfs prune`

### Cloning

```bash
# Clone Cholla with SSH
$ git clone git@github.com:cholla-hydro/cholla.git

# cd into cholla
$ cd cholla

# Initialize and clone the submodule
$ git submodule update --init
```

### Pulling

```bash
# Option 1: Pull Cholla and update the submodule. I recommend a git alias for
# the pull command
$ cd cholla
$ git pull --recurse-submodule

# Option 2: Pull the parent(Cholla) repo and submodule seperately
$ cd cholla
$ git pull  # just pulls Cholla
# Update the submodule to the version that the parent points at. Note that this
# will put the submodule in a detached head state. You can checkout a branch in
# the submodule if you want
$ git submodule update
```

### Editing and Making New Commits to the Data Submodule

```bash
# Make sure to checkout the branch in the submodule. By default Git only
# clones/checks out the specific commit that the parent repo points to
$ cd cholla/cholla-tests-data
$ git checkout *branch-name*

# In the submodule directory make your changes, commit, and push them just as
# you would normally
$ git add *files*
$ git commit
$ git push

# To point the parent (Cholla) repo at the right version of the data submodule
# cd into cholla and commit the submodule. Note that this will just change which
# commit in the submodule the parent repo points at, it will not commit the
# contents of the submodule into the parent repo
$ cd ../
$ git add cholla-test-data
$ git commit
$ git push
```
