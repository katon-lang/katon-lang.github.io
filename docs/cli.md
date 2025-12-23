When you install Katon, it also comes with the official CLI—a powerful tool designed to manage the lifecycle of your Katon projects from initialization to verification.

The Katon CLI allows you to:

1. Scaffold Katon projects: Quickly generate a standardized project structure.

2. Verify Lemmas: Manually trigger formal verification of your logic, designed to be integrated into CI/CD pipelines.

3. Transpile Code: Convert Katon source code into memory-safe Rust code (Experimental).

## Create a New Katon Project

To start a new project, use the `new` command followed by your desired project name:

```bash
katon new myproject
```
This command initializes a new directory named `myproject` with the following standardized boilerplate:

### Project Structure

- `src/`: The core directory for your source code.

- `src/myproject.ktn`: The entry point for your Katon project. This file is automatically named after your project and is where you begin defining your lemmas and logic.

- `config.toml`: Contains project metadata, including the package name, version, and author information under the `[package]` header.

- `.gitignore`: Pre-configured to ignore build artifacts and the `/target` directory to keep your repository clean.

- `README.md`: A basic Markdown file generated with your project title, ready for your documentation.

**VERIFY LEMMA & TRANSPILATION COMING SOON!**