# Contributing to Orbit

Thank you for your interest in contributing to Orbit! We welcome community contributions, whether they are bug reports, feature requests, or pull requests (PRs).

## 🛠️ How to Contribute

### 1. Reporting Bugs
If you find a bug, please open an issue on GitHub. Include:
- A clear, descriptive title.
- Steps to reproduce the issue.
- Your OS, Window Manager (e.g., Hyprland, Sway), and GTK4 version.
- Any relevant logs (run `orbit daemon` in a terminal to see standard output errors).

### 2. Suggesting Enhancements
Have an idea to make Orbit better? Open an issue! We love discussing new features. Try to explain:
- What the feature is.
- Why it would be useful to you and others.
- How you envision it working in the UI.

### 3. Submitting Pull Requests
If you want to write code and fix a bug or add a feature yourself:
1. **Fork** the repository.
2. **Clone** your fork locally.
3. **Create a branch** for your feature (`git checkout -b feature/my-new-feature`).
4. **Commit** your changes (`git commit -m 'Add some feature'`).
5. **Push** to the branch (`git push origin feature/my-new-feature`).
6. **Open a Pull Request** against the `main` branch.

## 🧑‍💻 Development Setup

Orbit is written in Rust and relies on GTK4 and DBus (NetworkManager and BlueZ).

### Prerequisites (Arch Linux)
To compile and test Orbit locally, you will need the standard Rust toolchain and GTK development libraries.

```bash
sudo pacman -S base-devel rustup git gtk4 gtk4-layer-shell pkgconf
rustup default stable
```

### Running Locally
You can run the frontend or daemon directly via Cargo during development:

```bash
# Run the background daemon to watch logs and errors
cargo run -- daemon

# In a separate terminal, trigger the UI to show
cargo run -- toggle
```

## 📐 Code Guidelines

- **Formatting:** We strictly use the standard Rust formatter. Always run `cargo fmt` before committing your code.
- **Linting:** Keep your code clean by ensuring `cargo clippy` does not produce any warnings.
- **Modularity:** UI components should remain modular (e.g., `src/ui/network_list.rs` handles only the network list). Do not pollute the main orchestrator (`window.rs`) with component-specific logic.
- **GTK CSS:** When adding new UI elements, always assign them a semantic CSS class (e.g., `.orbit-my-new-element`) using `.add_css_class()` so users can theme them via `style.css`.

We look forward to reviewing your contributions!
