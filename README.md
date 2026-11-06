# RigSync

**Keep your REAPER setup identical on every computer.**

RigSync syncs your REAPER configuration (actions and shortcuts, menus and
toolbars, scripts, extensions, FX chains, templates, themes and more) between
your computers. Change something on your laptop, push it, and pull it on your
studio PC. No copying folders by hand, and no "which one is newer?" conflicts.

Your setup is stored in **your own private GitHub repository**, or in a
**shared folder on your own network** (a NAS or a shared drive) if you'd rather
nothing leaves your home or studio. RigSync has no servers and never sees your
files.

> **Early release.** RigSync is new. Before your first push or pull, make a
> copy of your REAPER folder somewhere safe, just in case.

---

## What you need

- **Windows 10 or 11** (64-bit). A Mac version is planned.
- **REAPER installed on each computer.** RigSync syncs REAPER's settings, not
  REAPER itself. It works with normal and portable installs.
- **A free GitHub account** (sign up at [github.com/signup](https://github.com/signup)),
  **or** a shared folder every computer can open, like a NAS. See
  [Use a shared folder instead of GitHub](#use-a-shared-folder-instead-of-github).

---

## Install

1. Download **RigSync-Setup.exe** from the [Releases page](https://github.com/jaysabins/rigsync-releases/releases/latest).
2. Double-click it and click through. It installs just for you (no admin
   password) and adds RigSync to the Start menu.
3. Open **RigSync** from the Start menu.

Prefer no installer? **RigSync-Portable.zip** on the same page is the same
app as a folder: unzip it somewhere permanent and run `RigSync.exe` inside.

**"Windows protected your PC"?** RigSync isn't code-signed yet, so Windows
doesn't recognise it. Click **More info**, then **Run anyway**.

---

## Set up your first computer (about 5 minutes)

**Close REAPER first.**

### 1. Your REAPER folder
RigSync usually finds it automatically. If the box is empty, open REAPER, go
to *Options > Show REAPER resource path in explorer/finder*, and choose that
folder.

### 2. Create your private repository
In step 2, **GitHub** is selected. (Using a shared folder instead? See
[below](#use-a-shared-folder-instead-of-github) and skip to step 5.)

Click **Create a private repo**. GitHub opens with the name filled in. Make
sure **Private** is selected, then click **Create repository**.

That's the only thing you'll ever do in this repo. RigSync fills it for you.

### 3. Create an access token
This is a password that lets RigSync use that one repository, and nothing else
on your account.

1. Click **Create an access token**. GitHub opens with the right permission
   already filled in.
2. Under **Repository access**, choose **Only select repositories** and pick
   the repo you just made.
3. Under **Expiration**, pick **No expiration** (or a date, if you'd rather
   renew it now and then).
4. Click **Generate token** and copy it. It starts with `github_pat_`.
5. Save it in your password manager. GitHub shows it only once, and you'll
   use it on your other computers too.

### 4. Connect
Back in RigSync, fill in:
- **Repository:** `your-github-name/your-repo-name` (or paste the repo's URL)
- **Access token:** paste it
- **This computer's name:** something like `STUDIO` or `LAPTOP`

Click **Connect**.

### 5. Choose what to sync
Open the **Files** tab. The recommended items are already selected (click
**Select recommended** to get back to them). Look over the list, change
anything you like, then click **Save selection**.

### 6. Push
Click **Push**. Your setup is now in your private repo. The first push can
take a few minutes if you have lots of scripts.


### Use a shared folder instead of GitHub
If every computer can open the same folder on your network (a NAS, a shared
drive, or a folder shared from one PC), RigSync can keep its copy there and
nothing goes to the internet.

1. In step 2 of setup, click **SHARED FOLDER**.
2. Choose the folder, like `\\NAS\REAPER` or `Z:\RigSync`. RigSync makes a
   `RigSync.git` folder inside it the first time.
3. Click **Connect**. On your other computers, pick the **same** folder.

Syncing needs the computers to be on that network. Away from it (say, with
your laptop on the road) RigSync shows **Shared folder not reachable**,
REAPER works as normal, and you push your changes when you're back. If the
folder is shared from one PC, that PC has to be on.

---

## Set up your other computers

1. Install REAPER, ideally in the **same folder** as on your first computer
   (for example `C:\REAPER` on both). Some settings files contain full file
   paths, and those only work if the path is the same.
2. Install RigSync (see **Install** above).
3. **Close REAPER.**
4. Open RigSync and connect to the **same repository**, with the same token.
   Give this computer its own name.
5. Click **Pull cloud setup**.

Anything RigSync replaces is backed up first. Files that only this computer
has are kept.

---

## Everyday use

| When | What to do |
|---|---|
| You've changed something in REAPER | Open RigSync, click **Push** |
| You sit down at another computer | Close REAPER, open RigSync, click **Pull** |

RigSync always tells you which one you need: the status card says *Up to
date*, *Changes to push*, or *Newer changes in the cloud*.

To see exactly what changed in a file, click it in the **Changes** tab. Lines
shown in red were removed and lines in green were added, compared with the
last sync.

**Close REAPER before pulling.** REAPER saves its settings when it quits, so
it would overwrite what you just pulled. RigSync won't pull while REAPER is
open. Pushing while REAPER is open is fine.

### Optional: let RigSync handle it for you
In **Settings**, click **Create "REAPER (RigSync)" shortcut**, then pin the
new shortcut to your taskbar. Opening REAPER with it will:

1. pull anything new,
2. open REAPER,
3. push your changes when you quit.

You never have to remember to sync. Your normal REAPER icon still works as
usual.

### Optional: REAPER actions
In **Settings**, click **Add REAPER actions**. Then, once, in REAPER: go to
*Actions > Show action list > New action > Load ReaScript…*, open
*Scripts > RigSync*, and select the three **RigSync - …** files.

You get **Push now**, **Status** and **Open app** actions that you can put on
a toolbar or give a shortcut.

---

## Choosing what syncs

The **Files** tab shows everything in your REAPER folder.

- **Select or unselect** anything. Open a folder with its arrow to choose what's
  inside it, as deep as you like.
- **A dash in a box** means only part of that folder syncs.
- **Unselecting never deletes anything** on any computer; it just stops syncing.
- **Greyed-out items** are part of REAPER itself (in portable installs) and
  are never synced.
- **Search** finds any file or folder by name, however deep it is.
- **Double-click a file** to see what changed in it since the last sync.
- **Click Save selection** when you're done. Your choices reach your other
  computers on the next push.

### Leave a folder alone on one computer
Some folders should be managed by hand on one computer, for example a scripts
folder you write in git and publish with ReaPack. In **Settings > Leave alone
on this computer**, add that folder. On that computer RigSync won't upload,
change or remove anything in it. Your other computers keep syncing their own
copy. Remove it from the list to sync it again. (RigSync never copies a git
repo's hidden `.git` data either way.)

### Media Explorer databases
Tick **MediaDB** in the Files tab to sync your Media Explorer databases (it's
off by default). If your sound libraries live in different places on each
computer, name them in **Settings > Sound library locations**: for example
`SFX` is `D:\SFX` on one computer and `E:\Library\SFX` on the other. Each
computer's databases then point at its own folders.

### What's recommended
Your scripts, JSFX, extensions (SWS, ReaPack, ReaImGui and others), FX chains,
track and project templates, themes, presets, actions and shortcuts, menus and
toolbars, mouse modifiers, render presets and screensets.

Your **Preferences** sync too, through the item **reaper.ini (shared
settings)**. RigSync copies them setting by setting, so each computer keeps
its own audio and MIDI devices, folder paths, recent projects and window
positions. A pull never removes a setting, and it waits until REAPER is closed.

### What isn't, and why
- **`reaper.ini` as a whole file**: it also holds your audio device, buffer
  size and folder paths, which should stay different on each computer. The
  shared settings item above covers the rest of it.
- **Plugin scan caches**: REAPER rebuilds these on each computer.
- **Peak files and render queues**: specific to one computer.
- **Media Explorer databases**, unless you tick **MediaDB** (see above).

### Toolbar and window layout
Toolbar *buttons* sync, and so do docked toolbars and dockers through the
shared settings. *Floating* windows stay where each computer puts them, because
screens differ. To carry a whole window layout across:

1. On the computer with the layout you like, open REAPER and go to
   *View > Screensets/Layouts > Windows*.
2. **Save** a screenset, then push.
3. On the other computer, pull, then **Load** that screenset.

---

## Keeping REAPER itself on the same version

Each computer tells your repo which REAPER version it has. If another computer
is on a newer one, RigSync shows a warning with an **Update REAPER** button.
With REAPER closed, click it: RigSync downloads that version's official
installer from reaper.fm and installs it in place. Your settings aren't
touched. Afterwards, push once so your other computers know.

---

## Safety nets

- **Backups:** anything RigSync replaces or removes is copied first. Find
  them in *History > Open backups folder*. The last 30 are kept.
- **History:** every push is saved. In the **History** tab, pick any version
  and click **Restore this version**, then push to make it current everywhere.
- **No overwriting newer work:** a computer that's behind can't push over
  newer changes. It's asked to pull first.
- **Same file changed on two computers:** RigSync shows which file and asks
  which version to keep. The other one is kept in History or a backup. If
  this computer's version is the one you want, click **Keep this computer's
  version** instead of pulling.
- **Big removals ask first:** any push or pull that would remove 25 or more
  files stops and asks you to confirm.
- **A fresh or emptied REAPER folder:** RigSync recognises it and offers
  **Restore from cloud** instead of syncing the missing files as deletions.

---

## Making every computer match one

If your computers have drifted apart and you want a clean start, pick the
computer whose setup you trust. Close REAPER on every computer, then:

1. On the trusted computer: *Settings > Start fresh >* **Make the cloud match
   this computer**.
2. On each other computer: *Settings > Start fresh >* **Make this computer
   match the cloud**.

Anything replaced or removed is backed up first, and the old cloud version
stays in History.

---

## Updating RigSync

When a new version is out, a bar appears at the top of the window. Click
**Get update** and say yes: RigSync downloads the new version, closes,
installs it and opens again. Your settings carry over.

---

## Privacy

- Your files go only to **your own private GitHub repository**. RigSync
  doesn't talk to any other server, apart from reaper.fm when you ask it to
  update REAPER.
- Your token is stored in **Windows Credential Manager**, not in a plain file.
- RigSync refuses to use a public repository.
- To stop a computer syncing: *Settings > Disconnect this computer*.
- To revoke access completely: delete the token on GitHub (*Settings >
  Developer settings > Personal access tokens*).

---

## Troubleshooting

| You see | What to do |
|---|---|
| "Windows protected your PC" | Click **More info > Run anyway**. |
| Windows Defender says the file contains a virus | A false alarm some antivirus tools give unsigned apps. In *Windows Security > Protection history*, choose the RigSync item, then *Actions > Allow on device*. |
| "GitHub rejected the access token" | The token expired, was regenerated or deleted, or lost access to the repo. Click **Enter a new token** and paste a new one. |
| "Repo not found" | Check the repo name, and that the token was given access to that repo. |
| "Close REAPER before pulling" | Quit REAPER, then pull. |
| "The cloud has newer changes" | Pull first, then push. |
| "This push would remove … files" | Check the **Changes** tab. Only confirm if you meant to delete them. |
| "Couldn't be written" after a pull | Click **Pull** again. If it keeps failing, the message names the file. |
| Something is slow, frozen or erroring | *Settings >* **Copy diagnostics**, then paste the report to whoever is helping you. It never includes your token or your files. |
| Pulled, but toolbars or windows are in different places | Select **reaper.ini (shared settings)** for docked layout. Floating windows don't sync; use a screenset (see **Toolbar and window layout**). |

---

## Uninstall

1. *Settings > Disconnect this computer* (removes the saved token).
2. Uninstall RigSync in *Windows Settings > Apps* (or delete the folder, if
   you used the portable zip).
3. Optionally delete `%APPDATA%\RigSync` (RigSync's settings and backups).
4. Optionally delete the token on GitHub, and the repository if you no longer
   want the stored setup.

Your REAPER folder isn't touched by any of this.

---

*RigSync is not affiliated with Cockos or REAPER. REAPER is a trademark of
Cockos Incorporated.*
