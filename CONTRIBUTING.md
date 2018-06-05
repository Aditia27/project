# Contributing to project

We welcome contributions to project of any kind including documentation, themes,
organization, tutorials, blog posts, bug reports, issues, feature requests,
feature implementations, pull requests, answering questions on the forum,
helping to manage issues, etc.

The project community and maintainers are [very active](https://github.com/goprojectio/project/pulse/monthly) and helpful, and the project benefits greatly from this activity. We created a [step by step guide](https://goproject.io/tutorials/how-to-contribute-to-project/) if you're unfamiliar with GitHub or contributing to open source projects in general.

*Note that this repository only contains the actual source code of project. For **only** documentation-related pull requests / issues please refer to the [projectDocs](https://github.com/goprojectio/projectDocs) repository.*

*Changes to the codebase **and** related documentation, e.g. for a new feature, should still use a single pull request.*

## Table of Contents

* [Asking Support Questions](#asking-support-questions)
* [Reporting Issues](#reporting-issues)
* [Submitting Patches](#submitting-patches)
  * [Code Contribution Guidelines](#code-contribution-guidelines)
  * [Git Commit Message Guidelines](#git-commit-message-guidelines)
  * [Vendored Dependencies](#vendored-dependencies)
  * [Fetching the Sources From GitHub](#fetching-the-sources-from-github)
  * [Using Git Remotes](#using-git-remotes)
  * [Build project with Your Changes](#build-project-with-your-changes)
  * [Updating the project Sources](#updating-the-project-sources)

## Asking Support Questions

We have an active [discussion forum](https://discourse.goproject.io) where users and developers can ask questions.
Please don't use the GitHub issue tracker to ask questions.

## Reporting Issues

If you believe you have found a defect in project or its documentation, use
the GitHub [issue tracker](https://github.com/goprojectio/project/issues) to report
the problem to the project maintainers. If you're not sure if it's a bug or not,
start by asking in the [discussion forum](https://discourse.goproject.io).
When reporting the issue, please provide the version of project in use (`project
version`) and your operating system.

## Code Contribution

project has become a fully featured static site generator, so any new functionality must:

* be useful to many.
* fit naturally into _what project does best._
* strive not to break existing sites.
* close or update an open [project issue](https://github.com/goprojectio/project/issues)

If it is of some complexity, the contributor is expected to maintain and support the new future (answer questions on the forum, fix any bugs etc.).

It is recommended to open up a discussion on the [project Forum](https://discourse.goproject.io/) to get feedback on your idea before you begin. If you are submitting a complex feature, create a small design proposal on the [project issue tracker](https://github.com/goprojectio/project/issues) before you start.


**Bug fixes are, of course, always welcome.**



## Submitting Patches

The project project welcomes all contributors and contributions regardless of skill or experience level. If you are interested in helping with the project, we will help you with your contribution.

### Code Contribution Guidelines

Because we want to create the best possible product for our users and the best contribution experience for our developers, we have a set of guidelines which ensure that all contributions are acceptable. The guidelines are not intended as a filter or barrier to participation. If you are unfamiliar with the contribution process, the project team will help you and teach you how to bring your contribution in accordance with the guidelines.

To make the contribution process as seamless as possible, we ask for the following:

* Go ahead and fork the project and make your changes.  We encourage pull requests to allow for review and discussion of code changes.
* When you’re ready to create a pull request, be sure to:
    * Sign the [CLA](https://cla-assistant.io/goprojectio/project).
    * Have test cases for the new code. If you have questions about how to do this, please ask in your pull request.
    * Run `go fmt`.
    * Add documentation if you are adding new features or changing functionality.  The docs site lives in `/docs`.
    * Squash your commits into a single commit. `git rebase -i`. It’s okay to force update your pull request with `git push -f`.
    * Ensure that `mage check` succeeds. [Travis CI](https://travis-ci.org/goprojectio/project) (Linux and macOS) and [AppVeyor](https://ci.appveyor.com/project/goprojectio/project/branch/master) (Windows) will fail the build if `mage check` fails.
    * Follow the **Git Commit Message Guidelines** below.

### Git Commit Message Guidelines

This [blog article](http://chris.beams.io/posts/git-commit/) is a good resource for learning how to write good commit messages,
the most important part being that each commit message should have a title/subject in imperative mood starting with a capital letter and no trailing period:
*"Return error on wrong use of the Paginator"*, **NOT** *"returning some error."*

Also, if your commit references one or more GitHub issues, always end your commit message body with *See #1234* or *Fixes #1234*.
Replace *1234* with the GitHub issue ID. The last example will close the issue when the commit is merged into *master*.

Sometimes it makes sense to prefix the commit message with the package name (or docs folder) all lowercased ending with a colon.
That is fine, but the rest of the rules above apply.
So it is "tpl: Add emojify template func", not "tpl: add emojify template func.", and "docs: Document emoji", not "doc: document emoji."

Please use a short and descriptive branch name, e.g. **NOT** "patch-1". It's very common but creates a naming conflict each time when a submission is pulled for a review.

An example:

```text
tpl: Add custom index function

Add a custom index template function that deviates from the stdlib simply by not
returning an "index out of range" error if an array, slice or string index is
out of range.  Instead, we just return nil values.  This should help make the
new default function more useful for project users.

Fixes #1949
```

###  Fetching the Sources From GitHub

Due to the way Go handles package imports, the best approach for working on a
project fork is to use Git Remotes.  Here's a simple walk-through for getting
started:

1. Get the project source:

    ```bash
    go get -u -v -d github.com/goprojectio/project
    ```

1. Install Mage:

    ```bash
    go get github.com/magefile/mage
    ```

1. Change to the project source directory and fetch the dependencies:

    ```bash
    cd $HOME/go/src/github.com/goprojectio/project
    mage vendor
    ```

    Note that project uses [Go Dep](https://github.com/golang/dep) to vendor dependencies, rather than a simple `go get`. We don't commit the vendored packages themselves to the project git repository. The call to `mage vendor` takes care of all this for you.

1. Create a new branch for your changes (the branch name is arbitrary):

    ```bash
    git checkout -b iss1234
    ```

1. After making your changes, commit them to your new branch:

    ```bash
    git commit -a -v
    ```

1. Fork project in GitHub.

1. Add your fork as a new remote (the remote name, "fork" in this example, is arbitrary):

    ```bash
    git remote add fork git://github.com/USERNAME/project.git
    ```

1. Push the changes to your new remote:

    ```bash
    git push --set-upstream fork iss1234
    ```

1. You're now ready to submit a PR based upon the new branch in your forked repository.

### Building project with Your Changes

project uses [mage](https://github.com/magefile/mage) to sync vendor dependencies, build project, run the test suite and other things. You must run mage from the project directory.

```bash
cd $HOME/go/src/github.com/goprojectio/project
```

To build project: 

```bash
mage project
```

To install project in `$HOME/go/bin`:

```bash
mage install
```

To run the tests:

```bash
mage projectRace
mage -v check
```

To list all available commands along with descriptions:

```bash
mage -l
```

### Updating the project Sources

If you want to stay in sync with the project repository, you can easily pull down
the source changes, but you'll need to keep the vendored packages up-to-date as
well.

```bash
git pull
mage vendor
```
