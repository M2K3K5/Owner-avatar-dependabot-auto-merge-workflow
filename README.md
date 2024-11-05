# Dependabot Auto Merge

This repository is designed for users who do not want to set up branch protection rules in GitHub but still want to automatically merge Dependabot pull requests. This is particularly useful for small projects where maintaining branch protection rules might be overkill.

## Features

- **Automatic Merging**: Automatically merges Dependabot pull requests that do not involve major version updates.
- **Customizable Pipeline**: Allows insertion of custom code between the pipeline steps for tasks such as checking compilation or running tests.

## Usage

1. **Copy the GitHub Actions Workflow**: Copy the [auto-merge.yml](.github/workflows/auto-merge.yml) workflow file to your repository. This file sets up the GitHub Actions to automatically merge Dependabot pull requests. Refer to the guide section below for adding custom pipeline code.
2. **Edit the Dependabot Configuration**: Configure Dependabot to check for updates in your project dependencies. See the [dependabot.yml](.github/dependabot.yml) file for an example configuration. Refer to the guide section below for setting up the package ecosystem.
3. **Allow GitHub Actions to Approve Pull Requests**: In your repository settings, navigate to `Settings` > `Actions` > `General` and enable the option `Allow GitHub Actions to create and approve pull requests`.
## Guide

### Setting Up Package Ecosystem

You can specify the package ecosystem for your project, such as Maven for Java, npm for Node.js, or Cargo for Rust. For more details, refer to the [Dependabot configuration options guide](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file#package-ecosystem).

### Customization

You can insert custom steps in the pipeline to perform additional checks, such as building your project or running tests. This ensures that only pull requests that pass these checks are automatically merged.

To add custom code, insert your steps between the `----` marks in the [auto-merge.yml](.github/workflows/auto-merge.yml) file.

```yaml
# CUSTOM STEPS START -----------------------------------------------------

# Example: Build and test Rust code
- uses: actions/checkout@v4

- name: Build
  run: cargo build --verbose

- name: Run tests
  run: cargo test --verbose

# CUSTOM STEPS END -------------------------------------------------------
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
