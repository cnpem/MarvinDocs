# Contributing

We want to make contributing to MarvinDocs as easy and transparent as possible. We appreciate your support in improving the documentation for HPC Marvin.

## How to contribute?

To contribute to MarvinDocs, you will need to install [Rust](https://www.rust-lang.org/):

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Next, install [mdbook](https://github.com/rust-lang/mdBook).:

```bash
cargo install mdbook
```

Then, clone the repository:

```bash
git clone https://github.com/cnpem/MarvinDocs
cd MarvinDocs
```

Finally, start the local server:

```bash
mdbook serve --hostname 0.0.0.0 
```

Access the documentation at `http://localhost:3000` and make any necessary changes.

> [!IMPORTANT]  
> All changes should be made in the `dev` branch. This allows us to test and review changes before merging them into the `main` documentation.
> `main` branch is the production version of the documentation.
> `dev` branch is where all changes should be made before they are thoroughly tested and merged into `main`.

## Additional Resources

* mdBook Documentation: https://rust-lang.github.io/mdBook/

Thank you for contributing to MarvinDocs!
