# Setup Guide: Decodemy Data Analytics Pilot

**Course:** Foundations of Data Analytics  
**Academy:** Decodemy  
**Time required:** 35–45 minutes (first time)  
**Difficulty:** No experience needed – follow every click  
**Support:** Email: `augoamos@gmail.com` (response within 24 hours)

---

## Table of Contents

1. [What You'll Install](#what-youll-install)
2. [System Requirements](#system-requirements)
3. [Part 1: Install Anaconda (Python + Jupyter)](#part-1-install-anaconda-python--jupyter)
   - [Windows Instructions](#windows-instructions)
   - [Mac Instructions (Intel)](#mac-instructions-intel)
   - [Mac Instructions (Apple Silicon M1/M2/M3)](#mac-instructions-apple-silicon-m1m2m3)
   - [Linux Instructions](#linux-instructions)
4. [Part 2: Verify Anaconda Installation](#part-2-verify-anaconda-installation)
5. [Part 3: Install Tableau Public](#part-3-install-tableau-public)
6. [Part 4: Create GitHub Account](#part-4-create-github-account)
7. [Part 5: Install GitHub Desktop](#part-5-install-github-desktop)
8. [Part 6: Fork & Clone the Course Repository](#part-6-fork--clone-the-course-repository)
9. [Final Verification Checklist](#final-verification-checklist)
10. [Common Installation Issues & Fixes](#common-installation-issues--fixes)
11. [Still Stuck?](#still-stuck)

---

## What You'll Install

| # | Tool | Purpose | Size | Free? |
|---|------|---------|------|-------|
| 1 | **Anaconda** | Python + Jupyter Notebook + 300+ data libraries | ~600 MB | ✅ |
| 2 | **Tableau Public** | Interactive dashboards (no coding) | ~500 MB | ✅ |
| 3 | **GitHub Account** | Save and submit your code | n/a | ✅ |
| 4 | **GitHub Desktop** | Easy way to use GitHub (no command line) | ~300 MB | ✅ |

**Total download size:** ~1.4 GB  
**Total install time:** 35–45 minutes

---

## System Requirements

### Minimum Requirements

| Component | Requirement |
|-----------|-------------|
| **Operating System** | Windows 10/11, macOS 11+, or Ubuntu 20.04+ |
| **RAM** | 8 GB (4 GB minimum, but slower) |
| **Storage** | 5 GB free space |
| **Internet** | Required for downloads and publishing dashboards |
| **Browser** | Chrome, Firefox, or Safari (latest version) |

### Check Your System Before Starting

**Windows:**
- Press `Windows + Pause/Break` to see RAM and OS version

**Mac:**
- Click Apple logo → "About This Mac"

**If you have less than 4 GB RAM:** The course will run slowly. Consider using [Google Colab](https://colab.research.google.com/) as an alternative for Python exercises.

---

## Part 1: Install Anaconda (Python + Jupyter)

### What is Anaconda?

Anaconda installs **Python** (the programming language) and **Jupyter Notebook** (where you'll write code) together in one package. It also includes 300+ data libraries (Pandas, Matplotlib, Seaborn, NumPy) so you don't need to install anything else.

### Download Anaconda

1. Go to: [anaconda.com/download](https://www.anaconda.com/download)
2. Click the blue **"Download"** button
3. The website should automatically detect your operating system

**Direct download links (if website is slow):**

| Operating System | Direct Link |
|-----------------|-------------|
| Windows 64-bit | [Download](https://repo.anaconda.com/archive/Anaconda3-2024.10-Windows-x86_64.exe) |
| Mac Intel | [Download](https://repo.anaconda.com/archive/Anaconda3-2024.10-MacOSX-x86_64.pkg) |
| Mac Apple Silicon (M1/M2/M3) | [Download](https://repo.anaconda.com/archive/Anaconda3-2024.10-MacOSX-arm64.pkg) |
| Linux 64-bit | [Download](https://repo.anaconda.com/archive/Anaconda3-2024.10-Linux-x86_64.sh) |

---

### Windows Instructions

**Step 1: Run the installer**
- Find the downloaded file (usually in `Downloads` folder)
- File name: `Anaconda3-2024.10-Windows-x86_64.exe`
- **Double-click** to run
- Click **"Yes"** if Windows asks for permission

**Step 2: Installation wizard (follow exactly)**
- Click **"Next"** (don't change anything)
- Click **"I Agree"** (license agreement)
- **"Install for: Just Me"** → Click **"Next"**
- **Destination folder:** Leave as default (`C:\Users\YourName\anaconda3`) → Click **"Next"**

**Step 3: Advanced options (CRITICAL!)**
- ✅ **Check the box** that says **"Add Anaconda to my PATH environment variable"**
  - *Note: This option has red text warning – check it anyway*
- ✅ **Check the box** that says **"Register Anaconda as my default Python"**
- Click **"Install"**

**Step 4: Wait for installation**
- This takes **5-10 minutes**
- Progress bar will move slowly – this is normal

**Step 5: Finish installation**
- Click **"Next"** (skip Microsoft VSCode installation – not needed for this course)
- Click **"Next"** (skip PyCharm – not needed)
- Click **"Finish"**

**Step 6: Verify installation**
- Press `Windows` key
- Type `Anaconda Navigator`
- Click the app icon
- **First launch may take 30-60 seconds** – be patient
- You should see a window with "Jupyter Notebook", "Anaconda Prompt", etc.

---

### Mac Instructions (Intel)

**Step 1: Determine your Mac type**
- Click Apple logo (top-left) → "About This Mac"
- Look at **"Chip"**:
  - If it says **Intel** → follow these instructions
  - If it says **Apple M1, M2, or M3** → skip to [Mac Apple Silicon instructions](#mac-instructions-apple-silicon-m1m2m3)

**Step 2: Run the installer**
- Find the downloaded `.pkg` file (not the `.sh` file)
- File name: `Anaconda3-2024.10-MacOSX-x86_64.pkg`
- **Double-click** to run

**Step 3: Installation wizard**
- Click **"Continue"** through the screens
- Click **"Agree"** to license
- **"Install for: All users"** or **"Just me"** – either works
- Click **"Install"**
- Enter your computer password when prompted

**Step 4: Wait for installation**
- Takes **5-10 minutes**

**Step 5: Verify installation**
- Open **Finder** → **Applications** → **Anaconda Navigator**
- **First launch:** Right-click → "Open" (to bypass security warning)
- Click "Open" again when prompted
- You should see the Anaconda Navigator window

---

### Mac Instructions (Apple Silicon M1/M2/M3)

**Step 1: Confirm you have Apple Silicon**
- Click Apple logo → "About This Mac"
- Chip should say **Apple M1, M2, or M3**

**Step 2: Download the correct version**
- File name: `Anaconda3-2024.10-MacOSX-arm64.pkg`
- *Note: "arm64" = Apple Silicon*

**Step 3: Run the installer**
- Double-click the `.pkg` file
- Click **"Continue"**

**Step 4: Installation wizard**
- Click **"Agree"** to license
- Click **"Install"**
- Enter your computer password

**Step 5: Verify installation**
- Open **Finder** → **Applications** → **Anaconda Navigator**
- First launch may take 30-60 seconds
- You should see the Anaconda Navigator window

---

### Linux Instructions (Ubuntu/Debian)

**Step 1: Open Terminal**
- Press `Ctrl + Alt + T`

**Step 2: Download and install**
```bash
# Download the installer
wget https://repo.anaconda.com/archive/Anaconda3-2024.10-Linux-x86_64.sh

# Run the installer
bash Anaconda3-2024.10-Linux-x86_64.sh
```

**Step 3: Follow prompts**
- Press `Enter` to scroll through license agreement
- Type `yes` to agree
- Press `Enter` for default install location (`/home/username/anaconda3`)
- Type `yes` to run `conda init`

**Step 4: Close and reopen terminal**

**Step 5: Verify installation**
```bash
conda --version
# Should show: conda 24.x.x
```

---

## Part 2: Verify Anaconda Installation

### Launch Jupyter Notebook

**Windows:**
- Press `Windows` key, type `Jupyter Notebook`
- Click the app (a black terminal window may open – this is normal)
- Your browser will open to `http://localhost:8888/tree`

**Mac:**
- Open **Anaconda Navigator**
- Under "Jupyter Notebook", click **"Launch"**
- Your browser will open to Jupyter

**You should see:** A file browser showing your computer's folders.

### Create Your First Notebook (Test)

1. In Jupyter, navigate to your **Desktop** (click "Desktop" folder)
2. Click **"New"** button (top-right) → **"Python 3"**
3. A new tab opens with an empty notebook

### Run Your First Python Code

1. Click the first empty cell (gray box)
2. Type exactly:
```python
print("Hello, Decodemy!")
```
3. Press **Shift + Enter** (hold Shift, press Enter, release both)
4. You should see `Hello, Decodemy!` printed below

**If you see the output:** ✅ Python works! Close the tab (don't save).

**If you see an error:** Take a screenshot and email `instructor@decodemy.com` with the error message.

---

## Part 3: Install Tableau Public

### What is Tableau Public?

Tableau Public is a **free** tool to create interactive dashboards. No coding required. You'll use it in Week 3 and Week 4.

### Step-by-Step Installation

**Step 1: Download Tableau Public**

- Go to: [public.tableau.com/app/download](https://public.tableau.com/en-us/s/download)
- Click **"Download Tableau Public"** (blue button)

**Step 2: Run the installer**

| Operating System | Instructions |
|-----------------|--------------|
| **Windows** | Double-click `.exe` → Click through defaults |
| **Mac** | Double-click `.dmg` → Drag Tableau Public to Applications folder |

**Step 3: Create a free account**

1. Open Tableau Public
2. Click **"Sign Up for Free"** (or "Create Account")
3. Use your email
4. Create a password (**write this down** – you'll need it Week 3)
5. Verify your email (check inbox for confirmation link)

**Step 4: Test it works**

1. After logging in, click **"Connect to Data"** (left sidebar)
2. Click **"Text File"** → navigate to any CSV (or just close – we'll use it Week 3)
3. You should see a data preview

### Important Notes About Tableau Public

| Do ✅ | Don't ❌ |
|-------|---------|
| Save to Tableau Public cloud | Save locally (not possible) |
| Share links with anyone | Save as `.twbx` file (requires Desktop) |
| Use up to 10 million rows | Expect desktop app features |

> **Warning:** Tableau Public is different from Tableau Desktop. Tableau Desktop costs $70/month. **Do not download Tableau Desktop** – we use the free Public version.

---

## Part 4: Create GitHub Account

### What is GitHub?

GitHub is a website where you save your code. Like Google Docs, but for programmers. You'll submit all exercises here.

### Step-by-Step

1. **Go to:** [github.com/join](https://github.com/join)

2. **Enter your information:**
   - **Username:** `your-firstname-lastname` (e.g., `alex-chen`, `maria-garcia`)
     - *Tip: Keep it professional – employers may see this*
   - **Email:** Use a valid email (where you can receive messages)
   - **Password:** Create a strong password (**write it down**)

3. **Complete verification:**
   - Solve the puzzle or enter email code
   - Click **"Create account"**

4. **Choose plan:**
   - Select **"Free"** (skip any paid upgrade screens)

5. **Verify your email:**
   - Check your inbox for a verification email from GitHub
   - Click the verification link

### Your GitHub username is important

You'll use it throughout the course. Write it down:

> **My GitHub username:** _______________

---

## Part 5: Install GitHub Desktop

### What is GitHub Desktop?

A **click-button** way to use GitHub. No command line or typing needed.

### Step-by-Step Installation

**Step 1: Download**
- Go to: [desktop.github.com](https://desktop.github.com)
- Click **"Download for Windows"** or **"Download for Mac"**

**Step 2: Install**

| Operating System | Instructions |
|-----------------|--------------|
| **Windows** | Double-click `.exe` → Click through defaults |
| **Mac** | Double-click `.zip` → Drag GitHub Desktop to Applications |

**Step 3: Sign in**
1. Open GitHub Desktop
2. Click **"Sign in to GitHub.com"**
3. Your browser will open – log in with your GitHub username and password
4. Click **"Authorize GitHub Desktop"**
5. Return to GitHub Desktop app

**Step 4: Configure Git (one-time setup)**
- Click **"File"** → **"Options"** (Windows) or **"Preferences"** (Mac)
- Enter your name and email (same as GitHub)
- Click **"Save"**

---

## Part 6: Fork & Clone the Course Repository

### What Do These Terms Mean?

| Term | Definition | Analogy |
|------|------------|---------|
| **Fork** | Copy the course materials to YOUR GitHub account | "Copy" a Google Doc |
| **Clone** | Download that copy to YOUR computer | "Download" the Google Doc as a Word file |

### Step 1: Get the Course Repository Link

Your instructor will provide a link. It looks like:
```
https://github.com/decodemy/data-analytics-pilot
```

### Step 2: Fork the Repository

1. **Open the course link** in your browser
2. Click the **"Fork"** button (top-right corner of the page)

```
┌─────────────────────────────────────────────────────────────┐
│  decodemy / data-analytics-pilot                    [Fork]  │
├─────────────────────────────────────────────────────────────┤
│  ...                                                       │
└─────────────────────────────────────────────────────────────┘
```

3. Keep **"Copy the main branch only"** checked
4. Click **"Create fork"**
5. Wait a few seconds – you now have your own copy at:
   ```
   https://github.com/YOUR-USERNAME/data-analytics-pilot
   ```

### Step 3: Clone the Repository (Download to Computer)

**Using GitHub Desktop (recommended for beginners):**

1. **Open GitHub Desktop**
2. Click **"File"** → **"Clone repository"**

```
┌─────────────────────────────────────────────────────────────┐
│  Clone a repository                                         │
│  ┌─────────────────────────────────────────────────────────┐│
│  │ URL tab │ GitHub.com tab                               ││
│  └─────────────────────────────────────────────────────────┘│
│                                                             │
│  Repository URL: https://github.com/YOUR-USERNAME/...      │
│                                                             │
│  Local path: C:\Users\YourName\Desktop                     │
│                                                             │
│                      [Clone]                                │
└─────────────────────────────────────────────────────────────┘
```

3. Click the **"URL"** tab
4. Paste your fork URL:
   ```
   https://github.com/YOUR-USERNAME/data-analytics-pilot
   ```
   *(Replace YOUR-USERNAME with your actual GitHub username)*

5. **Local path:** Choose `Desktop` (easy to find)
6. Click **"Clone"**

### Step 4: Verify it worked

1. Open your **Desktop** folder
2. You should see a folder named `data-analytics-pilot`
3. Open it – you should see folders like:
   - `week1-python-basics/`
   - `week2-pandas/`
   - `week3-visualization-tableau/`
   - `week4-capstone/`
   - `resources/`

### Alternative: Command Line (If GitHub Desktop Fails)

**Windows (Git Bash):**
```bash
# Open Git Bash (search in Start menu)
cd Desktop
git clone https://github.com/YOUR-USERNAME/data-analytics-pilot.git
```

**Mac (Terminal):**
```bash
# Open Terminal (Applications → Utilities → Terminal)
cd Desktop
git clone https://github.com/YOUR-USERNAME/data-analytics-pilot.git
```

---

## Final Verification Checklist

Before Week 1 starts, complete this checklist:

### Python & Jupyter
- [ ] Anaconda Navigator opens without errors
- [ ] Jupyter Notebook launches in browser
- [ ] You created a notebook and ran `print("Hello, Decodemy!")` successfully

### Tableau
- [ ] Tableau Public opens
- [ ] You can log in with your account
- [ ] You see "Connect to Data" screen

### GitHub
- [ ] GitHub account created
- [ ] You remember your GitHub username: _______________
- [ ] GitHub Desktop installed
- [ ] You forked the course repository
- [ ] You cloned the repository to your Desktop
- [ ] The `data-analytics-pilot` folder exists on your Desktop

### Final Test: Open Week 1 Materials
- [ ] Navigate to `data-analytics-pilot/week1-python-basics/` on your computer
- [ ] Open `README.md` (it should open in your browser or text editor)
- [ ] You can see the Week 1 instructions

---

## Common Installation Issues & Fixes

### Issue #1: "Add Anaconda to PATH" option didn't appear (Windows)

**Problem:** You missed the PATH checkbox during installation.

**Fix:**
1. Uninstall Anaconda (Control Panel → Programs and Features)
2. Reinstall Anaconda
3. **Carefully check** the box "Add Anaconda to my PATH environment variable"

### Issue #2: "conda is not recognized" (Windows)

**Problem:** PATH is still not configured.

**Fix (Option A):** Use Anaconda Prompt instead of Command Prompt
- Press Windows key, type `Anaconda Prompt`
- Use this for any conda commands

**Fix (Option B):** Reinstall Anaconda and check the PATH box

### Issue #3: Jupyter notebook doesn't open browser

**Problem:** Jupyter starts but no browser appears.

**Fix:**
1. Look at the terminal/command prompt window
2. Find a line like: `http://localhost:8888/tree?token=...`
3. **Copy that entire URL** (starts with `http://localhost:8888`)
4. Paste into Chrome or Firefox

### Issue #4: "ModuleNotFoundError: No module named pandas"

**Problem:** You're trying to import pandas before installing it.

**Fix:** In Jupyter, run this in a code cell:
```python
!conda install pandas matplotlib seaborn -y
```

### Issue #5: Tableau Public won't install (Mac)

**Problem:** "Tableau Public cannot be opened because Apple cannot check it."

**Fix:**
1. Right-click the installer
2. Click **"Open"**
3. Click **"Open"** again when prompted

### Issue #6: GitHub Desktop says "No repositories found"

**Problem:** You haven't forked the course repo yet.

**Fix:**
1. Go to the course repo in your browser
2. Click **"Fork"** button
3. Wait for fork to complete
4. Try cloning again

### Issue #7: My fork is behind the original repo

**Problem:** The instructor added new files after you forked.

**Fix (in GitHub Desktop):**
1. Click **"Fetch upstream"** (top of window)
2. Click **"Fetch and merge"**

### Issue #8: "Git is not installed" (when using command line)

**Problem:** Git is not on your computer.

**Fix:** Download from [git-scm.com](https://git-scm.com/downloads)

### Issue #9: Computer is too slow / low disk space

**Alternative Option:** Use Google Colab (free, runs in browser)

1. Go to [colab.research.google.com](https://colab.research.google.com)
2. Sign in with Google account
3. File → New Notebook
4. You can run Python code without installing anything

**Limitation:** You'll still need Tableau Public for Weeks 3-4.

---

## Still Stuck?

### Troubleshooting Flowchart

```
Encounter problem?
       ↓
Read the error message (it tells you what's wrong)
       ↓
Search the error online (copy-paste into Google)
       ↓
Still stuck? Email instructor@decodemy.com with:
  - Your operating system (Windows 11 / Mac M2 / Ubuntu)
  - Exact error message (copy-paste)
  - What you already tried
  - Screenshot of the problem
       ↓
Instructor responds within 24 hours
```

### Contact Information

| Support Channel | When to Use | Response Time |
|----------------|-------------|---------------|
| Email: `instructor@decodemy.com` | Any installation issue | 24 hours |
| GitHub Issues (in your forked repo) | Code-specific questions | 24-48 hours |

### What to Include in Your Email

**Subject:** Setup Issue – [Your Name] – [Brief Description]

**Body:**
```
Operating System: (e.g., Windows 11, Mac M2, Ubuntu 22.04)

What I was trying to do: (e.g., "Launch Jupyter Notebook")

What happened: (e.g., "Nothing opens, but I see a black window")

What I already tried: (e.g., "Restarted computer, reinstalled Anaconda")

Attached: Screenshot of the error
```

---

## Week 0 Office Hours (Before Week 1)

**Date:** [Day before Week 1 starts]  
**Time:** 7–8 PM ET  
**Location:** [Zoom link will be emailed to you]

**What to bring:**
- Your computer (laptop preferred)
- Any error messages you've seen
- Questions (no question is too basic)

**What will happen:**
1. Walk through installation together
2. Troubleshoot common issues live
3. Verify everyone can launch Jupyter
4. First look at the course repository

**Can't attend?** Email instructor for a recording link.

---

## You're Ready!

Once everything on the checklist is checked:

1. **Open the course repo** on your Desktop
2. **Navigate to:** `week1-python-basics/README.md`
3. **Read Week 1 instructions** (what to do before Tuesday)
4. **Attend Tuesday lecture** (Zoom link will be emailed)

---

## Quick Reference Card

| Tool | What to Type / Where to Click |
|------|-------------------------------|
| Launch Jupyter | Windows: `Jupyter Notebook` in Start menu<br>Mac: Anaconda Navigator → Launch |
| Launch Tableau | Desktop shortcut or Applications folder |
| Open course repo | Desktop → `data-analytics-pilot` |
| Submit exercises | GitHub Desktop → Commit → Push → Pull Request |
| Get help | Email: `instructor@decodemy.com` |

---

**Save this guide.** You'll reference it throughout the course.

**Welcome to Decodemy!** 
