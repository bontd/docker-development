We'd love your help making support the very best authentication & authorization
system library in PHP!

If you'd like to add new exported, please [open an issue][open-issue]
describing your proposal &mdash; discussing changes ahead of time makes
pull request review much smoother. In your issue, pull request, and any other
communications, please remember to treat your fellow contributors with
respect! We take our [code of conduct](CODE_OF_CONDUCT.md) seriously.

Note that you'll need to sign [xavia's Contributor License Agreement][cla]
before we can accept any of your contributions. If necessary, a bot will remind
you to accept the CLA when you open your pull request.

## Setup

[Fork][fork], then clone the repository:

```bash
git clone git@github.com:your_github_username/flash-development.git
cd flash-development
git remote add upstream https://github.com/xavia/flash-development.git
git fetch upstream
```

## Making Changes

Start by creating a new branch for your changes:

```bash
git checkout main
git fetch upstream
git rebase upstream/main
git checkout -b cool_new_feature
```

Make your changes, then ensure that `make fixer` and `make test` still pass. If
you're satisfied with your changes, push them to your fork.

```bash
git push origin cool_new_feature
```

Then use the GitHub UI to open a pull request.

At this point, you're waiting on us to review your changes. We _try_ to respond
to issues and pull requests within a few business days, and we may suggest some
improvements or alternatives. Once your changes are approved, one of the
project maintainers will merge them.

We're much more likely to approve your changes if you:

- Add tests for new functionality.
- Write a [good commit message][commit-message].
- Maintain backward compatibility.

[fork]: https://github.com/xavia/flash-development/fork

[open-issue]: https://github.com/xavia/flash-development/issues/new

[cla]: https://cla-assistant.io/xavia/flash-development

[commit-message]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
