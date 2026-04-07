# 🌅 The AI Daily Update Agent

Welcome! If you're here, you probably want to turn your chaotic morning inbox into a beautiful, curated daily briefing without doing any manual work. You are in the right place.

This guide is written for everyone—even if you've never used a command line before. We will walk through this step-by-step.

## 🤔 What is this?
This is a "Skill" for the Gemini AI. Once installed, you can simply ask your AI to read your recent emails and calendar, figure out what's urgent, and email you a beautifully designed summary. It acts like your personal Chief of Staff.

---

## 🛒 Phase 1: Gather Your "Ingredients"
*Complete this checklist before you touch any code.*

- [ ] **1. Download Node.js**
  - Go to [nodejs.org](https://nodejs.org/) and download the **"LTS"** (Long Term Support) version.
  - If asked which version to download:
    - 🍎 **Newer Macs (M1/M2/M3):** Choose **ARM64**
    - 🍎 **Older Macs (Intel) / 🪟 Windows:** Choose **x64**
  - Run the installer and click "Next" through the defaults. This is the "engine" that runs the app.

- [ ] **2. Get your Gemini API Key**
  - Go to [Google AI Studio](https://aistudio.google.com/app/apikey).
  - Click **"Create API Key"**.
  - **Copy this key**; we will paste it into the app in the next phase.

- [ ] **3. Get your Google Cloud Credentials**
  *This allows the AI to securely read your email. Follow these exact clicks:*
  1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
  2. **Select a Project** (top left) ➔ **New Project** ➔ Name it "AI Inbox Recap" ➔ **Create**.
  3. Search bar (top): Type **"Gmail API"** ➔ Click it ➔ **Enable**.
  4. Sidebar (left): **OAuth consent screen**.
      - Choose **External** ➔ **Create**.
      - Fill in **App Name** (e.g., "My Recap") and your email. Skip everything else.
      - Scroll to **"Test Users"** ➔ **Add Users** ➔ **Add your own Gmail address** (Crucial: the app won't let you log in without this!). ➔ **Save**.
  5. Sidebar (left): **Credentials**.
      - **+ Create Credentials** (top) ➔ **OAuth client ID**.
      - Application type: **Desktop App** ➔ Name it "Inbox App" ➔ **Create**.
  6. A box will pop up. Click **Download JSON**.
  7. **Crucial:** Find that file in your Downloads and rename it exactly to: `credentials.json`.

---

## 🛠️ Phase 2: Installation (One-Time Setup)

### Step 1: Open your Terminal
- 🍎 **Mac:** Press `Command + Space`, type **Terminal**, and press `Enter`.
- 🪟 **Windows:** Open Start, type **PowerShell**, and press `Enter`.

### Step 2: Install the Gemini CLI
Paste this into your Terminal and press `Enter`:
```bash
npm install -g @google/gemini-cli
```

> ⚠️ **If you get a "Permission Denied" error**, run this instead:
> ```bash
> sudo npm install -g @google/gemini-cli
> ```
> 🔐 **Password Warning:** After typing a `sudo` command, your Terminal will ask for your computer password. You will not see any characters as you type — not even stars. This is normal! Just type your password and press `Enter`.

> ❌ **"npm: command not found"?** You missed the Node.js installation in Phase 1. Go back and complete that step first, then return here.

### Step 3: Download the Code
Paste this into your Terminal and hit `Enter`:
```bash
curl -L https://github.com/mina-genee/AI-Daily-Inbox-Recap/archive/refs/heads/main.zip -o ai-daily-update.zip && unzip ai-daily-update.zip && cd AI-Daily-Inbox-Recap-main
```

### Step 4: Add Your Ingredients
1. **The Credentials:** Drag your `credentials.json` file directly into the `AI-Daily-Inbox-Recap-main` folder.

    > ❌ **"Missing Credentials" error later?** Make sure `credentials.json` is inside the project folder — not still sitting in your Downloads!

2. **The API Key:** Paste this into your terminal (replace `PASTE_YOUR_KEY_HERE` with your key from Phase 1, Step 2):
```bash
    echo "GEMINI_API_KEY=PASTE_YOUR_KEY_HERE" > .env
```

    > ❌ **"Missing API Key" error later?** This means the key wasn't saved correctly. Re-run the command above, making sure you replaced `PASTE_YOUR_KEY_HERE` with your actual key before pressing `Enter`.

### Step 5: Install the Skill
Paste this into your Terminal:
```bash
gemini skills install ./ --scope user
```

> ❌ **"gemini: command not found"?** Your computer hasn't registered the installation yet. Close your Terminal window, open a fresh one, and try this step again.

---

## 📬 Phase 3: How to Actually Use It!

1. Open your **Terminal**.
2. Type `gemini` and press `Enter`.
3. Now just talk to the AI! Type: **"Run my AI Daily Update."**

**First-Time Login:**
- A browser window will pop up. Log in with your Gmail.
- You will see a "Google hasn't verified this app" screen. Click **Advanced** ➔ **Go to [App Name] (unsafe)**. (This is safe; it's *your* private app!)
- Copy the code Google gives you, paste it back into your terminal, and hit `Enter`.

---

## 🎨 Make it Yours (No coding required)

- **Change the Rules:** Open `config.yaml` in any text editor (like Notepad). Under the `rules` section, just type what you want the AI to do in plain English. Example: *"If an email mentions 'invoice', always mark it as High Priority."*
- **Share the Magic:** If you create a great new rule set, go to your Terminal and run:
```bash
gemini skills package ./
```
This creates a `.skill` file you can send to your friends so they can use your exact version!
