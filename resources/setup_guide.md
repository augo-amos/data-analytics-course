# Setup Guide: Data Foundations

**Time required:** 45–60 minutes (first time)  
**Difficulty:** No experience needed – follow every click  
**Support:** Post in `#setup-help` on Slack (screenshots encouraged)

---

## Before You Start (Important!)

**Read this entire guide before downloading anything.** Some steps must be done in order.

**What you'll install:**
1. Python + Jupyter (via Anaconda – one installer does both)
2. Tableau Public (for dashboards)
3. Git & GitHub (for submitting work)
4. Slack (for communication)

**Total download size:** ~1.5 GB (about 20-30 minutes on home internet)

---

## Part 1: Install Anaconda (Python + Jupyter)

### What is Anaconda?
Anaconda installs **Python** (the programming language) and **Jupyter Notebook** (where you'll write code) together. It also includes 300+ data libraries so you don't need to install anything else.

### Step-by-Step Installation

#### Windows Users

1. **Download the installer**
   - Go to: [anaconda.com/download](https://www.anaconda.com/download)
   - Click the blue **"Download"** button (it should automatically detect Windows)
   - If asked: Choose **64-bit Graphical Installer** (≈600 MB)

2. **Run the installer**
   - Find the file in your Downloads folder (named `Anaconda3-...-Windows-x86_64.exe`)
   - **Double-click** to run
   - Click **"Yes"** if Windows asks for permission

3. **Installation wizard (follow exactly)**
   - Click **"Next"** (don't change anything)
   - Click **"I Agree"** (license agreement)
   - **"Install for: Just Me"** → Next
   - **Destination folder:** Leave as default (`C:\Users\YourName\anaconda3`) → Next
   - **IMPORTANT:** Check the box that says **"Add Anaconda to my PATH environment variable"** (it's red text – check it anyway)
   - **IMPORTANT:** Check the box that says **"Register Anaconda as my default Python"**
   - Click **"Install"** (takes 5-10 minutes – coffee break)

4. **After installation**
   - Click **"Next"** (skip Microsoft VSCode installation – not needed)
   - Click **"Next"** (skip PyCharm – not needed)
   - Click **"Finish"**

5. **Verify installation**
   - Press `Windows` key, type `Anaconda Navigator`
   - Click the app icon – it should open a window (may take 30 seconds first time)
   - You should see a screen with "Jupyter Notebook", "Anaconda Prompt", etc.

#### Mac Users

1. **Determine your Mac type**
   - Click the Apple logo (top-left) → "About This Mac"
   - Look at **"Chip"**:
     - **Apple M1, M2, or M3** → You need "Apple Silicon" version
     - **Intel** → You need "Intel" version

2. **Download the installer**
   - Go to: [anaconda.com/download](https://www.anaconda.com/download)
   - Click **"Download"** – choose the correct version for your chip
   - File will be in Downloads folder (named `Anaconda3-...-MacOSX-...sh`)

3. **Run the installer**
   - Double-click the `.pkg` file (not the `.sh` file if both appear)
   - Click **"Continue"** through the screens
   - Click **"Agree"** to license
   - **"Install for: All users"** or **"Just me"** – either works
   - Click **"Install"** (may ask for your computer password)
   - Wait 5-10 minutes

4. **Verify installation**
   - Open **Finder** → **Applications** → **Anaconda Navigator**
   - Double-click to launch (may say "first time opening")
   - You should see the Anaconda Navigator window

#### Linux Users

```bash
# Open Terminal (Ctrl+Alt+T)
# Download the installer
wget https://repo.anaconda.com/archive/Anaconda3-2024.10-Linux-x86_64.sh

# Run the installer
bash Anaconda3-2024.10-Linux-x86_64.sh

# Follow prompts:
# - Press Enter to scroll through license
# - Type "yes" to agree
# - Press Enter for default install location
# - Type "yes" to run conda init

# Close and reopen terminal, then verify
conda --version
```

### Common Anaconda Issues

| Problem | Solution |
|---------|----------|
| "Anaconda Navigator won't open" | Open Anaconda Prompt (Windows) or Terminal (Mac) and type: `anaconda-navigator` |
| "Add to PATH" option didn't appear (Windows) | Reinstall – uncheck and recheck the box. It's critical. |
| "Disk full" error | Free up 5 GB space. Delete old downloads, empty trash. |
| Mac: "can't be opened because Apple cannot check it" | Right-click the installer → Open → Click "Open" again |

---

## Part 2: Launch Jupyter Notebook & Test Python

### Open Jupyter Notebook

**Windows:**
- Press `Windows` key, type `Jupyter Notebook`
- Click the app (may open a black window – that's normal)
- Your browser will open to `http://localhost:8888/tree`

**Mac:**
- Open **Anaconda Navigator**
- Under "Jupyter Notebook", click **"Launch"**
- Your browser will open to Jupyter

**You should see:** A file browser showing your computer's folders.

### Create Your First Notebook

1. In Jupyter, navigate to your **Desktop** (click "Desktop" folder)
2. Click **"New"** button (top-right) → **"Python 3"**
3. A new tab opens with an empty notebook

### Test Python

1. Click the first empty cell (gray box)
2. Type exactly:
```python
print("Hello, Data Analytics!")
```
3. Press **Shift + Enter** (hold Shift, press Enter, release both)
4. You should see `Hello, Data Analytics!` printed below

**If you see the output:** ✅ Python works! Close the tab (don't save) – we'll use GitHub for organized work.

**If you see an error:** Screenshot and post in `#setup-help` on Slack.

---

## Part 3: Install & Set Up Tableau Public

### What is Tableau Public?
A free tool to create interactive dashboards and publish them online. No coding required.

### Step-by-Step Installation

**Windows & Mac:**

1. **Download Tableau Public**
   - Go to: [public.tableau.com/app/download](https://public.tableau.com/en-us/s/download)
   - Click **"Download Tableau Public"** (blue button)
   - File size: ~500 MB

2. **Run the installer**
   - **Windows:** Double-click `.exe` file → Click through defaults
   - **Mac:** Double-click `.dmg` file → Drag Tableau Public to Applications folder

3. **Create a free account**
   - Open Tableau Public
   - Click **"Sign Up for Free"** (or "Create Account")
   - Use your email (personal or school)
   - Create a password (write it down – you'll need it Week 3)
   - Verify email (check inbox for confirmation link)

4. **Test it works**
   - After logging in, click **"Connect to Data"** (left sidebar)
   - Click **"Text File"** → navigate to `sample_sales.csv` (if you don't have it yet, just close – we'll use it Week 3)
   - You should see a data preview. Close Tableau for now.

### Tableau Public vs Tableau Desktop

| Feature | Tableau Public (free) | Tableau Desktop (paid, $70/month) |
|---------|----------------------|-----------------------------------|
| Save locally | ❌ No (cloud only) | ✅ Yes |
| Share link | ✅ Yes (public) | ❌ No (private only) |
| Data size limit | 10 million rows | Unlimited |
| For this course | ✅ Perfect | ❌ Not needed |

**Don't accidentally download Tableau Desktop** – it requires payment. Look for "Tableau Public" in the name.

---

## Part 4: GitHub & Git (For Submitting Work)

### What is GitHub?
A website where you save your code. Like Google Docs but for programmers. You'll submit exercises here.

### Create GitHub Account

1. **Go to:** [github.com/join](https://github.com/join)
2. **Enter:**
   - Username: `your-firstname-lastname` (e.g., `alex-chen`)
   - Email: (use same email as Slack)
   - Password: (create one – write it down)
3. Click **"Verify"** (puzzle or email code)
4. Click **"Create account"**
5. Choose **"Free"** plan (skip any paid upgrade screens)

### Install GitHub Desktop (Easiest for Beginners)

**Why GitHub Desktop?** You click buttons instead of typing commands.

**Windows & Mac:**

1. **Download:** [desktop.github.com](https://desktop.github.com)
2. **Run installer** (Windows: `.exe` / Mac: drag to Applications)
3. **Sign in** to your GitHub account (use the website login, not desktop app)

### Fork & Clone the Course Repo

**What does this mean?**
- **Fork** = Copy the course materials to your GitHub account
- **Clone** = Download that copy to your computer

**Step-by-step:**

1. **Open the course repo** (instructor will provide link on Day 1 – placeholder below)
   ```
   https://github.com/your-academy/data-analytics-pilot
   ```

2. **Click "Fork"** (top-right corner of the page)
   - Keep "Copy the main branch only" checked
   - Click **"Create fork"**

3. **Open GitHub Desktop**
   - Click **"File"** → **"Clone repository"**
   - Click **"URL"** tab
   - Paste your fork URL:
     ```
     https://github.com/YOUR-USERNAME/data-analytics-pilot
     ```
     (replace YOUR-USERNAME with your actual GitHub username)
   - **Local path:** Choose Desktop (easy to find)
   - Click **"Clone"**

4. **Verify it worked**
   - Open your **Desktop** folder
   - You should see a folder named `data-analytics-pilot`
   - Inside: folders like `week1-python-basics`, `week2-pandas`, etc.

### Alternative: Command Line (Only if GitHub Desktop fails)

If GitHub Desktop won't install or you prefer typing:

**Windows:**
- Search "Git Bash" in Start menu → open
- Type: `cd Desktop`
- Type: `git clone https://github.com/YOUR-USERNAME/data-analytics-pilot.git`

**Mac:**
- Open Terminal (Applications → Utilities → Terminal)
- Type: `cd Desktop`
- Type: `git clone https://github.com/YOUR-USERNAME/data-analytics-pilot.git`

---

## Part 5: Join Slack (Communication)

### What is Slack?
A messaging app for the course. You'll ask questions here.

### Step-by-Step

1. **Check your email** for an invitation from `your-academy.slack.com`
   - Subject: "You've been invited to join [Academy Name] on Slack"
   - If not found in 10 minutes, check Spam folder

2. **Click the invitation link** – it will open in your browser

3. **Create account**
   - Enter your name (as you want to be called)
   - Create a password (different from GitHub)
   - Click "Join"

4. **Download Slack app (recommended)**
   - Go to: [slack.com/downloads](https://slack.com/downloads)
   - Download for your operating system
   - Install and sign in

5. **Join these channels:**
   - `#general` (course announcements)
   - `#introductions` (say hello!)
   - `#python-help` (technical questions)
   - `#random` (non-course chat)

### How to Ask for Help (Important!)

When stuck, **don't** say: "It doesn't work"  
**Do** say:
```
Problem: When I run `print(x)`, I get "NameError: name 'x' is not defined"

What I tried: I defined x = 5 in the cell above

Screenshot: [paste image]
```

**Post in `#python-help`** – instructor or peers will reply within 4 hours.

---

## Part 6: Create Loom Account (For Capstone Video)

### What is Loom?
A free screen recording tool. You'll use it to record your final project presentation in Week 4.

### Step-by-Step

1. **Go to:** [loom.com](https://loom.com)
2. Click **"Sign up free"**
3. Choose **"Sign up with Google"** (easiest) or "Sign up with email"
4. Download the desktop app (optional – browser version works)
5. **Test recording:**
   - Click "Record" button
   - Choose "Screen + Camera" (camera optional)
   - Record 10 seconds saying "Hello"
   - Stop recording – it auto-saves to cloud
   - Copy the link – it should work

**Free tier limits:** 5 minutes per video, 25 videos total – plenty for this course.

---

## Final Verification Checklist

Before Week 1 starts, complete this checklist:

### Python & Jupyter
- [ ] Anaconda Navigator opens without errors
- [ ] Jupyter Notebook launches in browser
- [ ] You created a notebook and ran `print("Hello")` successfully

### Tableau
- [ ] Tableau Public opens
- [ ] You can log in with your account
- [ ] You see "Connect to Data" screen

### GitHub
- [ ] GitHub account created
- [ ] GitHub Desktop installed
- [ ] You forked and cloned the course repo
- [ ] The `data-analytics-pilot` folder is on your Desktop

### Communication
- [ ] Slack account created
- [ ] You joined `#introductions` and posted a short hello
- [ ] You can post a message in `#random`

### Loom (optional for Week 1)
- [ ] Loom account created
- [ ] You can record and share a short test video

---

## Still Stuck? (Read This Before Panicking)

### "I followed all steps but Jupyter won't open"

**Try this:** Open Command Prompt (Windows) or Terminal (Mac) and type:
```bash
jupyter notebook
```
Copy the URL that appears (starts with `http://localhost:8888`) and paste into Chrome.

### "I can't find the Anaconda download page"

Direct links (if the website is confusing):
- **Windows 64-bit:** [Click here](https://repo.anaconda.com/archive/Anaconda3-2024.10-Windows-x86_64.exe)
- **Mac Intel:** [Click here](https://repo.anaconda.com/archive/Anaconda3-2024.10-MacOSX-x86_64.pkg)
- **Mac Apple Silicon (M1/M2/M3):** [Click here](https://repo.anaconda.com/archive/Anaconda3-2024.10-MacOSX-arm64.pkg)

### "My Tableau dashboard won't save"

Tableau Public saves to the cloud, not your computer. Look for **"Save to Tableau Public As..."** in File menu, not "Save As".

### "GitHub Desktop says 'No repositories found'"

You need to fork first (step in Part 4). Go to the course repo in your browser and click "Fork" before cloning.

### "I missed the Slack invite"

Email the instructor (instructor@youracademy.com) with "Slack invite" in the subject line.

---

## Office Hours for Setup

**Special Week 0 Setup Session:** [Date – day before Week 1 starts]

**Time:** 7–8 PM ET

**Link:** [Zoom link will be posted in Slack]

**What to bring:** 
- Your computer (laptop preferred)
- Any error messages you've seen
- A cup of coffee (it's okay to be confused)

**No question is too basic.** We'll get everyone working before Week 1 starts.

---

## You're Ready! Next Steps

Once everything above is checked off:

1. **Open the course repo** on your Desktop
2. **Navigate to:** `week1-python-basics/README.md`
3. **Read Week 1 instructions** (what to do before Tuesday)
4. **Attend Tuesday lecture** (link in Slack)

**Welcome to the pilot. You've already done the hardest part – setting up. The rest is learning.**

*Save this guide. You'll need it again in Week 1 when you launch Jupyter.*
**Questions?** Post in `#setup-help` on Slack. Include a screenshot – it helps us help you faster.

