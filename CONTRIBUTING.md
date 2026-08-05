# Contributing

We appreciate contributions from the community. Please review and follow the guidelines below.

## Getting Started

1. Review our [Engineering Standards](https://github.com/OxyHQ/engineering) for code quality expectations and conventions.
2. Read our [Code of Conduct](./CODE_OF_CONDUCT.md).
3. Browse [good first issues](https://github.com/search?q=org%3AOxyHQ+is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22&type=issues) across the organisation, or the issue tracker of the repository you want to work on.

## Code and Copy Reviews

All submissions, including submissions by project members, require review. We use GitHub pull requests for this purpose. Consult [GitHub Help](https://help.github.com/articles/about-pull-requests/) for more information on using pull requests.

## Report an Issue

Report all issues through GitHub Issues using the [Report a Bug](https://github.com/OxyHQ/.github/issues/new?template=bug_report.yml) template.

To help resolve your issue as quickly as possible, read the template and provide all the requested information.

## File a Feature Request

We welcome all feature requests, whether it's to add new functionality to an existing extension or to offer an idea for a brand new extension.

File your feature request through GitHub Issues using the [Feature Request template](https://github.com/OxyHQ/.github/issues/new?template=feature_request.yml).

## Create a Pull Request

When making pull requests to the repository, follow these guidelines:

- Before creating a pull request, file a GitHub Issue so that maintainers and the community can discuss the problem and potential solutions before you spend time on an implementation.
- In your PR's description, link to any related issues or pull requests to give reviewers the full context of your change.
- Follow the [Engineering Standards](https://github.com/OxyHQ/engineering) for code quality, naming conventions, and testing.
- Keep PRs focused: one logical change per PR.
- Ensure your changes do not introduce security vulnerabilities.

### Features

Before creating pull requests for new features, first file a GitHub Issue describing the reasoning and motivation for the feature. This gives maintainers and the community the opportunity to provide feedback on your idea before implementing it.

## Developer Setup

Every repository carries an `AGENTS.md` holding the standards it inherits, plus a `CLAUDE.md` whose only line imports it. Both are read directly by Claude Code, Codex, Cursor and Copilot, so there is nothing to install.

To adopt them in a new repository:

```bash
curl -O https://raw.githubusercontent.com/OxyHQ/engineering/main/AGENTS.md
curl -O https://raw.githubusercontent.com/OxyHQ/engineering/main/CLAUDE.md
```

Commit both at the repository root and add your project specific rules below the standards. See the [engineering repo](https://github.com/OxyHQ/engineering) for how the layering works.

## License

By contributing to Oxy, you agree that your contributions will be licensed under its license specified in the repository you are contributing to.
