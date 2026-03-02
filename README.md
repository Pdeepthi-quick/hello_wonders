COMPLETE GIT WORKFLOW (3-Member Team)
Members
    • TL — Team Lead (Prabha)
    • M1 — Member 1
    • M2 — Member 2

PART 0 — ONE-TIME SETUP (ALL MEMBERS)
Install Git:
sudo apt install git
Configure:
git config --global user.name "YourName"
git config --global user.email "your@email.com"
Create SSH:
ssh-keygen -t ed25519 -C "your@email.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
Paste key in GitHub → Settings → SSH Keys
Test:
ssh -T git@github.com

PART 1 — TEAM LEAD INITIAL REPO SETUP
Create project folder:
mkdir seven-wonders
cd seven-wonders
Initialize repo:
git init
echo "Seven Wonders" > wonders.txt
git add .
git commit -m "Initial commit"
git branch -M main
Connect GitHub repo:
git remote add origin git@github.com:PrabhaB1210/seven-wonders.git
git push -u origin main
Add collaborators (GitHub → Settings → Collaborators)

PART 2 — MEMBERS CLONE
M1 and M2:
git clone git@github.com:PrabhaB1210/seven-wonders.git
cd seven-wonders

PART 3 — CREATE BRANCHES
TL
git checkout -b wonder-tl
M1
git checkout -b wonder-m1
M2
git checkout -b wonder-m2

PART 4 — ADD FILES + PUSH
TL
echo "Machu Picchu" > tl.txt
git add .
git commit -m "TL added wonder"
git push -u origin wonder-tl
M1
echo "Great Wall" > m1.txt
git add .
git commit -m "M1 added wonder"
git push -u origin wonder-m1
M2
echo "Taj Mahal" > m2.txt
git add .
git commit -m "M2 added wonder"
git push -u origin wonder-m2

PART 5 — CREATE MERGE CONFLICT
TL edits main:
git checkout main
git pull
echo "Edited by TL" >> wonders.txt
git add .
git commit -m "TL edit"
git push
M1 edits SAME file:
git checkout wonder-m1
echo "Edited by M1" >> wonders.txt
git add .
git commit -m "M1 edit"
git push
M2 edits SAME file:
git checkout wonder-m2
echo "Edited by M2" >> wonders.txt
git add .
git commit -m "M2 edit"
git push

PART 6 — TEAM LEAD MERGES
Fetch branches:
git checkout main
git fetch origin
Merge M1:
git merge origin/wonder-m1
Resolve conflict:
nano wonders.txt
Remove markers → save.
Then:
git add wonders.txt
git commit -m "Conflict resolved M1"
git push
Merge M2:
git merge origin/wonder-m2
Resolve → commit → push

PART 7 — REBASE (MEMBERS)
M1
git checkout wonder-m1
git fetch origin
git rebase origin/main
M2
git checkout wonder-m2
git fetch origin
git rebase origin/main

PART 8 — CLEANUP
TL deletes remote branches:
git push origin --delete wonder-m1
git push origin --delete wonder-m2
git push origin --delete wonder-tl
Members delete local branches:
git branch -d wonder-m1
git branch -d wonder-m2

VERY IMPORTANT MEMORY FLOW (EXAM)
Always remember the story:
SSH setup
→ Repo creation
→ Clone
→ Branch
→ Commit
→ Push
→ Merge
→ Conflict resolve
→ Rebase
→ Cleanup
