# 🌅 The AI Daily Update Agent

Welcome! If you're here, you probably want to turn your chaotic morning inbox into a beautiful, curated daily briefing without doing any manual work. You are in the right place.

This guide is written for everyone—even if you've never used a command line before. We will walk through this step-by-step.

## 🤔 What is this?
This is a "Skill" for the Gemini AI. Once installed, you can simply ask your AI to read your recent emails and calendar, figure out what's urgent, and email you a beautifully designed summary. It acts like your personal Chief of Staff.

---

## 🛠 Phase 1: The One-Time Setup
Before the AI can do its magic, we need to give your computer the right tools. You only have to do this once.

### Step 1: Open your "Terminal"
The Terminal is just a text-based way to talk to your computer.

*   🍎 **If you are on a Mac:** Press `Command + Space` on your keyboard, type the word `Terminal`, and press `Enter`. A black or white box will pop up.
*   🪟 **If you are on Windows:** Open your Start menu, type the word `PowerShell`, and press `Enter`.

### Step 2: Install the Gemini CLI
This skill runs on the Gemini AI Command Line tool. You need to install it first. Copy this code, paste it into your Terminal, and press Enter:
```bash
npm install -g @google/gemini-cli
```
*(If you get a permission error, try: `sudo npm install -g @google/gemini-cli`)*

### Step 3: Download the Code
Copy this exact line of code, paste it into your Terminal, and press Enter:
```bash
git clone https://github.com/yourusername/ai-daily-update.git
cd ai-daily-update
```

### Step 4: Set Your Preferences
Tell the AI your email address and what rules you want it to follow. Run these two lines to create your settings files:
```bash
cp env.example .env
cp config.example.yaml config.yaml
```
*Open the `config.yaml` file in any text editor. You can type out plain-English rules like "Flag emails from investors as Urgent!"*

### Step 5: Install the Skill
Now, let's teach the AI how to do this specific job. In your Terminal, paste this code and press Enter:
```bash
gemini skills install ./ --scope user
```

---

## ⚠️ Phase 2: Connecting the AI's "Brain" (The API Key)
To use this, Gemini needs a key to connect to Google's servers. 

Did you get an error saying "you must specify the GEMINI_API_KEY"? Don't panic! This just means your AI needs its key. Here is exactly how to fix it:

1. **Get your free key**: Go to [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey) in your web browser.
2. Click the blue button that says "Create API key".
3. Copy the long string of letters and numbers it gives you.
4. Go back to your Terminal. We are going to save this key to a hidden file so you never have to enter it again.
5. Copy the code below, but replace `PASTE_YOUR_KEY_HERE` with your actual long key, then paste it into the Terminal and press Enter:
   ```bash
   echo "GEMINI_API_KEY=PASTE_YOUR_KEY_HERE" >> .env
   ```

---

## 🚀 Phase 3: How to Actually Use It!
You are fully set up! Whenever you want your daily briefing, here is what you do:

1. Open your Terminal.
2. Type `gemini` and press `Enter`. You will see a greeting welcoming you to the Gemini CLI.
3. Now that you are inside the AI chat, simply type:
   **"Run my AI Daily Update."**

**What to expect when you run this:**
*   The AI will quietly scan your inbox and calendar in the background.
*   It will apply the custom rules you wrote in `config.yaml`.
*   Wait about 30-60 seconds.
*   Check your Gmail! A beautifully formatted intelligence brief will be waiting in your inbox.

### ⏱️ Want it to run automatically every day? (macOS only)
If you are on a Mac, you don't even have to ask. You can tell your computer to run this every day at 5:00 PM EST. Just run this command from the repo folder:
```bash
launchctl load automation/com.user.aidailyupdate.plist
```

---

## 🎨 Make it Yours (No coding required)
Don't like the colors? Want to send it to Slack instead of Gmail? You don't need to be a developer to customize this skill!

*   **Change the Design:** Open the `assets/template.html` file in any text editor (like Notepad or TextEdit). You can change the hex color codes (like `#FFFFFF` for white) or swap out the fonts without breaking the AI's logic.
*   **Change the Rules:** Open `config.yaml`. Under the `rules` section, just type what you want the AI to do in plain English. For example: *"If an email mentions 'invoice', always put it in Action Required."*
*   **Share your changes:** If you create a great new color scheme or rule set, go to your Terminal and run:
    ```bash
    gemini skills package ./
    ```
    This creates a new `.skill` file that you can send to your friends or team so they can use your exact version!
