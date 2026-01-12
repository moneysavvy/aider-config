# Aider Configuration Repository

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Persistent configuration and settings for [Aider](https://github.com/paul-gauthier/aider) AI coding assistant. This repository ensures your Aider setup is version-controlled, backed up, and easily reproducible across different machines.

## 🚀 Quick Start

### 1. Clone this repository

```bash
# Clone to a safe location
git clone https://github.com/moneysavvy/aider-config.git ~/aider-config
cd ~/aider-config
```

### 2. Link configuration to your home directory

```bash
# Create symbolic link to home directory
ln -s ~/aider-config/.aider.conf.yml ~/.aider.conf.yml

# Or copy the file
cp .aider.conf.yml ~/.aider.conf.yml
```

### 3. Install Aider (if not already installed)

```bash
# Using uv tool (recommended - handles PATH automatically)
uv tool install --force --python python3.12 aider-chat@latest

# Or using pipx
pipx install aider-chat

# Or using pip in a venv (requires manual PATH setup)
pip install aider-chat

# If using pip install, add to your shell config (~/.zshrc or ~/.bashrc):
export PATH="$HOME/.venv/bin:$PATH"
```

### 4. Set up Ollama (for local LLM inference)

```bash
# Install Ollama from https://ollama.ai

# Pull the models specified in config
ollama pull qwen2.5-coder:latest
ollama pull qwen2.5-coder:7b
```

## 📁 Repository Structure

```
aider-config/
├── .aider.conf.yml      # Main Aider configuration file
├── .gitignore           # Python gitignore template
├── LICENSE              # MIT License
└── README.md            # This file
```

## ⚙️ Configuration Features

The `.aider.conf.yml` file includes:

- **Ollama Integration**: Configured to use local LLM models via Ollama
- **Model Settings**: Primary model (qwen2.5-coder) and editor model for smaller edits
- **Git Integration**: Auto-commits enabled with commit prompts
- **Code Quality**: Auto-linting with ruff
- **Performance**: Optimized token settings and caching
- **Developer Experience**: Pretty output, streaming responses, and diff display

## 🔧 Customization

Edit `.aider.conf.yml` to customize your setup:

### Change Models

```yaml
# Use different Ollama models
model: ollama/deepseek-coder-v2:latest
editor-model: ollama/codellama:7b

# Or use cloud APIs
model: openrouter/anthropic/claude-3.5-sonnet
```

### Add API Keys

Create a `.env` file in your project root (never commit this!):

```bash
# .env file
OPENROUTER_API_KEY=your_key_here
ANTHROPIC_API_KEY=your_key_here
```

## 🔄 Keeping Configuration Synced

### On your local machine:

```bash
cd ~/aider-config

# Pull latest changes
git pull origin main

# Make changes and commit
git add .aider.conf.yml
git commit -m "Update configuration"
git push origin main
```

### On a new machine:

```bash
# Clone and link
git clone https://github.com/moneysavvy/aider-config.git ~/aider-config
ln -s ~/aider-config/.aider.conf.yml ~/.aider.conf.yml
```

## 🛡️ Backup Strategy

1. **GitHub**: This repository serves as your primary backup
2. **Version Control**: All changes are tracked in Git history
3. **Multiple Machines**: Clone to multiple machines for redundancy
4. **Cloud Sync** (optional): Keep `~/aider-config` in Dropbox/iCloud for extra safety

## 📝 Project-Specific Configuration

You can also place `.aider.conf.yml` in your project root to override global settings:

```bash
cd /path/to/your/project
cp ~/aider-config/.aider.conf.yml .aider.conf.yml
# Edit for project-specific needs
```

Project-level configs override the global `~/.aider.conf.yml`.

## 🔗 Integration with Git

Aider will automatically use your Git configuration. Ensure Git is set up:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## 🐛 Troubleshooting

### Aider command not found
```bash
# Check if aider is in PATH
which aider

# If not found, find your aider installation
find ~ -maxdepth 5 -name "aider" -type f 2>/dev/null | grep bin

# Create symlink to a location already in PATH
ln -sf ~/.venv/bin/aider ~/bin/aider
# OR add to PATH in ~/.zshrc or ~/.bashrc:
export PATH="$HOME/.venv/bin:$PATH"
```

### --model flag not working (always uses same model)
```bash
# Check if environment variables are overriding settings
echo $AIDER_MODEL

# Check ~/.aider.env for hardcoded models
cat ~/.aider.env

# To allow --model flag to work, comment out AIDER_MODEL in ~/.aider.env
# And comment out model: line in ~/.aider.conf.yml
```

### Aider not finding config
```bash
# Check if symlink is correct
ls -la ~/.aider.conf.yml

# Verify Aider loads the config
aider --verbose
```

### Ollama connection issues
```bash
# Check if Ollama is running
ollama list

# Start Ollama service
ollama serve
```

### Model not found
```bash
# Pull the required models
ollama pull qwen2.5-coder:latest
ollama pull qwen2.5-coder:7b
```

## 📚 Resources

- [Aider Documentation](https://aider.chat/docs/)
- [Aider GitHub](https://github.com/paul-gauthier/aider)
- [Ollama Documentation](https://github.com/ollama/ollama)
- [Ollama Model Library](https://ollama.ai/library)

## 📄 License

MIT License - feel free to use and modify for your own needs.

## 🤝 Contributing

This is a personal configuration repository, but feel free to fork it and adapt it for your own use!

---

**Last Updated**: December 2025
