# Contributing

We want to make contributing to MarvinDocs as easy and transparent as possible. We appreciate your support in improving the documentation for HPC Marvin.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Branching Strategy](#branching-strategy)
3. [Testing](#testing)
4. [Opening a Pull Request (PR)](#opening-a-pull-request)
5. [Additional Resources](#additional-resources)

---

## Getting Started

1. Fork the repository on GitHub.

2. Clone your fork to your local machine:

```bash
git clone https://github.com/cnpem/MarvinDocs.git
cd MarvinDocs
```

3. Ensure that you are on the dev branch:

```bash
git checkout dev
```

4. Install any necessary dependencies and tools required for the documentation (e.g., `cargo install mdbook`).

## Branching Strategy

All contributions should be made on the dev branch. This allows us to test and review changes before merging them into the main documentation.

* Main branch (main): This contains the production version of the documentation.
* Development branch (dev): This is where all changes should be made before they are thoroughly tested and merged into main.

## Testing

Before submitting a Pull Request, your contribution must pass `mdbook.yml` action defined in the workflow.

1. Ensure your changes are working locally.
2. Trigger the automated tests in the GitHub Actions workflow by pushing your changes to the dev branch.
3. Wait for the workflow to complete. You can check the status of your tests under the Actions tab in the repository.
4. Only contributions that pass the tests will be considered for merging.

## Opening a Pull Request

Once your changes have been successfully tested, open a Pull Request (PR) from dev branch to the main branch. Ensure that you:
* Provide a meaningful title and description.
* Link any relevant issues that your PR addresses (if applicable).

## Additional Resources

* mdBook Documentation: https://rust-lang.github.io/mdBook/
* mdBook-catppuccin Documentation: https://github.com/catppuccin/mdBook

Thank you for contributing to MarvinDocs!
