# VSCode Rust Extensions
- rust-analyzer (change Rust-analyzer › Check: Command to clippy )
- codeLLDB
- Even Better TOML
- Error Lens
- Todo Tree  (add todo! macro to the regex)
- Dependi (replace crates)
- Tabnine (to try)

# VSCode Settings
- Change settings to have formatOnSave
```json
    "rust-analyzer.check.command": "clippy",
    "[rust]": {
        "editor.defaultFormatter": "rust-lang.rust-analyzer", 
        "editor.formatOnSave": true 
    }   
```

- Enable livereaload
```
cargo watch -q -c -w src/ -x 'run -q'
```

- Enable GitHub CI


# Crates
- [serde](https://serde.rs/), [serde_json](https://github.com/serde-rs/json)
- [thiserror](https://github.com/dtolnay/thiserror)
- [anyhow](https://github.com/dtolnay/anyhow)
- [tokio](https://tokio.rs/)  
> see also [blessed](https://blessed.rs/crates)
- [rustubble - Beautifull components for your terminal.](https://github.com/warpy-ai/rustubble)

# Rust Pattern
- Type state
- Interior mutability
- RAII 
- Builder


# Code completions with GitHub Copilot in VS Code
> see [Copilot Code completions](https://code.visualstudio.com/docs/copilot/ai-powered-suggestions)  
> watch [Copilot Best Practices](https://www.youtube.com/watch?v=2q0BoioYSxQ&t=90s)


# To Read
- https://docs.rs/specta/latest/specta/
- https://github.com/1Password/typeshare
- https://github.com/Aleph-Alpha/ts-rs
- https://youtu.be/BU1LYFkpJuk?si=hNgSRlxxGFGzCFHu





