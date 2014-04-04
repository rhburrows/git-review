# git-review

A script to help with reviewing a series of commits in a git
repository. Using the script you can step through each commit,
reviewing the commit messages, the diffs, and the state of the
repository at each point along the way.

## Installation

Download the `git-review` script (or clone the repository), make it
executable and place it in your path.

## Usage

`git-review` operates on the concept of review sessions. To start a
session invoke the command with either a starting commit or a range of
commits. If no ending commit is specified the review will continue
until the current `HEAD`

    git review abcde00..00edcba

Once the review session has started several more `git-review` commands
become available. At each point along the way the working directory
will be updated to the status after the current commit.

* `git review next`  - steps to the next commit in the review
* `git review prev`  - steps back to the previous commit in the review
* `git review diff`  - shows the diff for the current commit
* `git review abort` - cancel the current review session and returns
  the repository to the state before beginning the review

## Motivation

I wrote this tool for a couple primary use cases:

1. Reviewing commits to a repository since I last looked at it. In
this case its as simple as starting `git review` with the first of the
commits to review and run until it is up-to-date.

2. Reading through a repository or a branch from its beginning to get
a better understanding of how its organized and the project works.
I've wanted to spend more time reading code and I find that replaying
how it was built can help understanding.

## Current Limitations

At the moment there are a number of bugs/limitations of this script.

- It only really works with linear history, I haven't dealt with
  branching yet
- It can get stuck if navigating history with dead-ends (e.g. a
  temporary branch that was later deleted)
- If you try to start a review while it a review it doesn't prevent it
  and git abort will no longer work properly
