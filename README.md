# Thai-Git-Command-Manual
# คู่มือการใช้ Git Commands ฉบับสมบูรณ์

## สารบัญ
1. [Git คืออะไร](#git-คืออะไร)
2. [การติดตั้งและตั้งค่าเริ่มต้น](#การติดตั้งและตั้งค่าเริ่มต้น)
3. [คำสั่งพื้นฐาน](#คำสั่งพื้นฐาน)
4. [การจัดการ Repository](#การจัดการ-repository)
5. [การจัดการไฟล์และการเปลี่ยนแปลง](#การจัดการไฟล์และการเปลี่ยนแปลง)
6. [การจัดการ Branch](#การจัดการ-branch)
7. [การ Merge และ Rebase](#การ-merge-และ-rebase)
8. [การทำงานร่วมกับ Remote Repository](#การทำงานร่วมกับ-remote-repository)
9. [การดู History และ Log](#การดู-history-และ-log)
10. [การแก้ไขและย้อนกลับ](#การแก้ไขและย้อนกลับ)
11. [การจัดการ Tags](#การจัดการ-tags)
12. [Git Stash](#git-stash)
13. [Git Configuration](#git-configuration)
14. [คำสั่งขั้นสูง](#คำสั่งขั้นสูง)
15. [เทคนิคและ Best Practices](#เทคนิคและ-best-practices)

---

## Git คืออะไร

Git เป็นระบบควบคุมเวอร์ชัน (Version Control System) แบบกระจาย (Distributed) ที่ช่วยให้นักพัฒนาสามารถติดตามการเปลี่ยนแปลงของไฟล์ และทำงานร่วมกันในโปรเจกต์ได้อย่างมีประสิทธิภาพ

### ข้อดีของ Git
- ติดตามการเปลี่ยนแปลงของไฟล์ได้ทุกเวอร์ชัน
- สามารถย้อนกลับไปยังเวอร์ชันก่อนหน้าได้
- ทำงานร่วมกับผู้อื่นได้โดยไม่เกิดความขุ่นมัว
- สำรองข้อมูลได้หลายแห่ง
- ทำงานได้แม้ไม่มีอินเทอร์เน็ต

---

## การติดตั้งและตั้งค่าเริ่มต้น

### การติดตั้ง Git

**Windows:**
```bash
# ดาวน์โหลดจาก https://git-scm.com/
# หรือใช้ Chocolatey
choco install git

# หรือใช้ winget
winget install Git.Git
```

**macOS:**
```bash
# ใช้ Homebrew
brew install git

# หรือ MacPorts
sudo port install git
```

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install git
```

**Linux (CentOS/RHEL):**
```bash
sudo yum install git
# หรือ
sudo dnf install git
```

### การตั้งค่าเริ่มต้น

```bash
# ตั้งชื่อผู้ใช้ (จำเป็น)
git config --global user.name "ชื่อของคุณ"

# ตั้งอีเมล (จำเป็น)
git config --global user.email "email@example.com"

# ตั้ง default editor
git config --global core.editor "code --wait"  # Visual Studio Code
git config --global core.editor "vim"          # Vim
git config --global core.editor "nano"         # Nano

# ตั้งค่าการจัดการบรรทัดใหม่
git config --global core.autocrlf true    # Windows
git config --global core.autocrlf input   # macOS/Linux

# ตั้งค่าสีให้สวยงาม
git config --global color.ui auto

# ตั้งค่า default branch name
git config --global init.defaultBranch main

# ดูการตั้งค่าทั้งหมด
git config --list
```

---

## คำสั่งพื้นฐาน

### ตรวจสอบเวอร์ชันและความช่วยเหลือ

```bash
# ตรวจสอบเวอร์ชัน Git
git --version

# ดูความช่วยเหลือทั่วไป
git help

# ดูความช่วยเหลือสำหรับคำสั่งเฉพาะ
git help <command>
git <command> --help

# ดูคำสั่งย่อๆ
git <command> -h
```

### การสร้างและโคลน Repository

```bash
# สร้าง repository ใหม่ในโฟลเดอร์ปัจจุบัน
git init

# สร้าง repository ใหม่ในโฟลเดอร์ที่กำหนด
git init <folder-name>

# สร้าง bare repository (สำหรับเซิร์ฟเวอร์)
git init --bare

# โคลน repository จาก remote
git clone <url>

# โคลนและเปลี่ยนชื่อโฟลเดอร์
git clone <url> <folder-name>

# โคลนเฉพาะ branch เดียว
git clone -b <branch-name> <url>

# โคลนแบบ shallow (ไม่เอา history ทั้งหมด)
git clone --depth 1 <url>
```

---

## การจัดการ Repository

### ตรวจสอบสถานะ Repository

```bash
# ดูสถานะไฟล์ทั้งหมด
git status

# ดูสถานะแบบสั้น
git status -s
git status --short

# ดูสถานะและไฟล์ที่ถูกละเว้น
git status --ignored

# ดูสถานะแบบละเอียด
git status -v
git status --verbose
```

### การตั้งค่า Remote Repository

```bash
# ดู remote ทั้งหมด
git remote
git remote -v    # ดูพร้อม URL

# เพิ่ม remote ใหม่
git remote add <name> <url>
git remote add origin https://github.com/user/repo.git

# เปลี่ยน URL ของ remote
git remote set-url <name> <new-url>

# เปลี่ยนชื่อ remote
git remote rename <old-name> <new-name>

# ลบ remote
git remote remove <name>
git remote rm <name>

# ดูข้อมูลของ remote
git remote show <name>
```

---

## การจัดการไฟล์และการเปลี่ยนแปลง

### การเพิ่มไฟล์เข้า Staging Area

```bash
# เพิ่มไฟล์เดียว
git add <filename>

# เพิ่มไฟล์หลายไฟล์
git add <file1> <file2> <file3>

# เพิ่มไฟล์ทั้งหมดในโฟลเดอร์ปัจจุบัน
git add .

# เพิ่มไฟล์ทั้งหมดใน repository
git add -A
git add --all

# เพิ่มเฉพาะไฟล์ที่ถูก tracked แล้ว
git add -u
git add --update

# เพิ่มไฟล์แบบเลือกส่วน (interactive)
git add -i
git add --interactive

# เพิ่มแค่บางส่วนของไฟล์
git add -p <filename>
git add --patch <filename>

# เพิ่มไฟล์ตามรูปแบบ
git add "*.txt"
git add src/
```

### การ Commit

```bash
# Commit พร้อมข้อความ
git commit -m "ข้อความอธิบายการเปลี่ยนแปลง"

# Commit พร้อมข้อความแบบหลายบรรทัด
git commit -m "หัวข้อ" -m "รายละเอียด"

# Commit และ add ไฟล์ที่ tracked พร้อมกัน
git commit -am "ข้อความ"

# เปิด editor เพื่อเขียนข้อความ commit
git commit

# แก้ไข commit ล่าสุด
git commit --amend

# แก้ไข commit ล่าสุดโดยเก็บข้อความเดิม
git commit --amend --no-edit

# Commit โดยไม่ต้องผ่าน pre-commit hooks
git commit --no-verify

# Commit เปล่า (ไม่มีการเปลี่ยนแปลง)
git commit --allow-empty -m "Empty commit"

# Commit พร้อมวันที่เฉพาะ
git commit --date="2023-01-01 12:00:00" -m "ข้อความ"
```

### การลบและย้ายไฟล์

```bash
# ลบไฟล์จาก working directory และ staging area
git rm <filename>

# ลบไฟล์หลายไฟล์
git rm <file1> <file2>

# ลบไฟล์แต่เก็บไว้ใน working directory
git rm --cached <filename>

# ลบโฟลเดอร์และไฟล์ข้างใน
git rm -r <folder-name>

# บังคับลบไฟล์ที่มีการแก้ไข
git rm -f <filename>

# ย้ายหรือเปลี่ยนชื่อไฟล์
git mv <old-filename> <new-filename>
```

### การดูความแตกต่าง (Diff)

```bash
# ดูความแตกต่างของไฟล์ที่ยังไม่ได้ add
git diff

# ดูความแตกต่างของไฟล์เฉพาะ
git diff <filename>

# ดูความแตกต่างของไฟล์ที่อยู่ใน staging area
git diff --staged
git diff --cached

# ดูความแตกต่างระหว่าง commit
git diff <commit1> <commit2>

# ดูความแตกต่างระหว่าง branch
git diff <branch1> <branch2>

# ดูแค่ชื่อไฟล์ที่เปลี่ยน
git diff --name-only

# ดูสถิติการเปลี่ยนแปลง
git diff --stat

# ดูความแตกต่างแบบ word-by-word
git diff --word-diff
```

---

## การจัดการ Branch

### การสร้างและเปลี่ยน Branch

```bash
# ดู branch ทั้งหมด
git branch

# ดู branch ทั้งหมดรวมถึง remote
git branch -a

# ดู remote branch
git branch -r

# สร้าง branch ใหม่
git branch <branch-name>

# สร้าง branch ใหม่จาก commit เฉพาะ
git branch <branch-name> <commit-hash>

# เปลี่ยนไป branch อื่น
git checkout <branch-name>

# สร้าง branch ใหม่และเปลี่ยนไปใช้เลย
git checkout -b <branch-name>

# สร้าง branch จาก remote branch
git checkout -b <local-branch> origin/<remote-branch>

# เปลี่ยน branch (คำสั่งใหม่)
git switch <branch-name>

# สร้าง branch ใหม่และเปลี่ยนไป (คำสั่งใหม่)
git switch -c <branch-name>
```

### การจัดการ Branch

```bash
# เปลี่ยนชื่อ branch ปัจจุบัน
git branch -m <new-branch-name>

# เปลี่ยนชื่อ branch อื่น
git branch -m <old-name> <new-name>

# ลบ branch (ต้องไม่อยู่ใน branch นั้น)
git branch -d <branch-name>

# บังคับลบ branch
git branch -D <branch-name>

# ลบ remote branch
git push origin --delete <branch-name>

# ดู branch ที่ถูก merge แล้ว
git branch --merged

# ดู branch ที่ยังไม่ได้ merge
git branch --no-merged

# ดูข้อมูลล่าสุดของแต่ละ branch
git branch -v

# ตั้งค่า upstream branch
git branch --set-upstream-to=origin/<branch-name>
git branch -u origin/<branch-name>
```

---

## การ Merge และ Rebase

### การ Merge

```bash
# Merge branch อื่นเข้ามาใน branch ปัจจุบัน
git merge <branch-name>

# Merge แบบ fast-forward (ถ้าเป็นไปได้)
git merge --ff-only <branch-name>

# Merge แบบไม่ fast-forward (สร้าง merge commit เสมอ)
git merge --no-ff <branch-name>

# Merge แต่ไม่ commit เลย
git merge --no-commit <branch-name>

# Merge พร้อมข้อความ
git merge <branch-name> -m "ข้อความ merge"

# ยกเลิก merge ที่กำลังทำอยู่
git merge --abort

# ดำเนินการ merge ต่อหลังแก้ conflict
git merge --continue
```

### การ Rebase

```bash
# Rebase branch ปัจจุบันกับ branch อื่น
git rebase <branch-name>

# Rebase แบบ interactive
git rebase -i <commit-hash>
git rebase -i HEAD~3  # rebase 3 commit ล่าสุด

# ดำเนินการ rebase ต่อหลังแก้ conflict
git rebase --continue

# ข้าม commit ปัจจุบันใน rebase
git rebase --skip

# ยกเลิก rebase
git rebase --abort

# Rebase โดยไม่สร้าง merge commit
git rebase --onto <new-base> <old-base> <branch-name>
```

### การแก้ไข Merge Conflicts

```bash
# ดูไฟล์ที่มี conflict
git status

# เปิดไฟล์แก้ conflict ด้วย merge tool
git mergetool

# หลังแก้ conflict แล้ว
git add <conflicted-file>
git commit  # สำหรับ merge
git rebase --continue  # สำหรับ rebase

# ตั้งค่า merge tool
git config --global merge.tool vimdiff
git config --global merge.tool vscode
```

---

## การทำงานร่วมกับ Remote Repository

### การ Push และ Pull

```bash
# Push ไปยัง remote repository
git push

# Push branch ใหม่ไปยัง remote
git push -u origin <branch-name>
git push --set-upstream origin <branch-name>

# Push ทุก branch
git push --all

# Push tags ทั้งหมด
git push --tags

# Push พร้อม tags
git push --follow-tags

# บังคับ push (ระวัง!)
git push --force
git push -f

# บังคับ push แบบปลอดภัย
git push --force-with-lease

# Pull จาก remote repository
git pull

# Pull จาก branch เฉพาะ
git pull origin <branch-name>

# Pull แบบ rebase
git pull --rebase

# Pull โดยไม่ commit
git pull --no-commit
```

### การ Fetch

```bash
# Fetch ข้อมูลจาก remote
git fetch

# Fetch จาก remote เฉพาะ
git fetch <remote-name>

# Fetch branch เฉพาะ
git fetch origin <branch-name>

# Fetch และลบ branch ที่ไม่มีใน remote
git fetch --prune
git fetch -p

# Fetch tags ทั้งหมด
git fetch --tags

# Fetch แบบ shallow
git fetch --depth=1
```

---

## การดู History และ Log

### การดู Commit Log

```bash
# ดู commit log พื้นฐาน
git log

# ดู log แบบสั้น
git log --oneline

# ดู log จำนวนเฉพาะ
git log -n 5
git log -5

# ดู log พร้อมกราฟ
git log --graph

# ดู log แบบสวยงาม
git log --oneline --graph --decorate --all

# ดู log ของไฟล์เฉพาะ
git log <filename>

# ดู log ตามช่วงเวลา
git log --since="2023-01-01"
git log --until="2023-12-31"
git log --since="2 weeks ago"

# ดู log ตามผู้เขียน
git log --author="ชื่อผู้เขียน"

# ดู log ตามข้อความ commit
git log --grep="bug fix"

# ดู log พร้อมการเปลี่ยนแปลง
git log -p
git log --patch

# ดูสถิติการเปลี่ยนแปลง
git log --stat

# ดู log แบบย่อ
git log --pretty=format:"%h - %an, %ar : %s"
```

### การดูประวัติการเปลี่ยนแปลง

```bash
# ดูประวัติการเปลี่ยนแปลงของไฟล์
git blame <filename>

# ดู blame พร้อมข้อมูลผู้เขียนเดิม
git blame -C <filename>

# ดู blame ตามบรรทัด
git blame -L 10,20 <filename>

# ดูการเปลี่ยนแปลงของคำสั่ง git
git reflog

# ดู reflog ของ branch เฉพาะ
git reflog <branch-name>

# ดูข้อมูลของ commit
git show <commit-hash>

# ดูไฟล์ใน commit เฉพาะ
git show <commit-hash>:<filename>
```

---

## การแก้ไขและย้อนกลับ

### การย้อนกลับการเปลี่ยนแปลง

```bash
# ย้อนกลับไฟล์ที่ยังไม่ได้ add
git checkout -- <filename>
git restore <filename>  # คำสั่งใหม่

# ย้อนกลับไฟล์ทั้งหมดที่ยังไม่ได้ add
git checkout -- .
git restore .

# ย้อนกลับไฟล์จาก staging area
git reset HEAD <filename>
git restore --staged <filename>  # คำสั่งใหม่

# ย้อนกลับไฟล์จาก commit เฉพาะ
git checkout <commit-hash> -- <filename>
git restore --source=<commit-hash> <filename>
```

### การ Reset

```bash
# Reset แบบ soft (เก็บการเปลี่ยนแปลงใน staging area)
git reset --soft <commit-hash>
git reset --soft HEAD~1  # ย้อนกลับ 1 commit

# Reset แบบ mixed (default - เก็บการเปลี่ยนแปลงใน working directory)
git reset <commit-hash>
git reset HEAD~1

# Reset แบบ hard (ลบการเปลี่ยนแปลงทั้งหมด - ระวัง!)
git reset --hard <commit-hash>
git reset --hard HEAD~1

# Reset ไฟล์เฉพาะจาก staging area
git reset <filename>
```

### การ Revert

```bash
# สร้าง commit ใหม่ที่ย้อนกลับการเปลี่ยนแปลงของ commit เฉพาะ
git revert <commit-hash>

# Revert โดยไม่สร้าง commit
git revert --no-commit <commit-hash>

# Revert หลาย commit
git revert <commit1>..<commit2>

# Revert merge commit
git revert -m 1 <merge-commit-hash>
```

### การทำความสะอาด

```bash
# ดูไฟล์ที่จะถูกลบ
git clean -n
git clean --dry-run

# ลบไฟล์ที่ไม่ได้ track
git clean -f

# ลบไฟล์และโฟลเดอร์ที่ไม่ได้ track
git clean -fd

# ลบไฟล์ที่ถูกละเว้นด้วย
git clean -fx

# ลบทั้งหมดแบบ interactive
git clean -i
```

---

## การจัดการ Tags

### การสร้าง Tags

```bash
# สร้าง lightweight tag
git tag <tag-name>

# สร้าง lightweight tag ที่ commit เฉพาะ
git tag <tag-name> <commit-hash>

# สร้าง annotated tag
git tag -a <tag-name> -m "ข้อความอธิบาย"

# สร้าง signed tag
git tag -s <tag-name> -m "ข้อความอธิบาย"

# สร้าง tag ย้อนหลัง
git tag -a v1.0 -m "เวอร์ชัน 1.0" <commit-hash>
```

### การจัดการ Tags

```bash
# ดู tags ทั้งหมด
git tag

# ดู tags ที่ตรงกับรูปแบบ
git tag -l "v1.*"

# ดูข้อมูลของ tag
git show <tag-name>

# ลบ tag ใน local
git tag -d <tag-name>

# ลบ tag ใน remote
git push origin --delete <tag-name>

# Push tag เฉพาะ
git push origin <tag-name>

# Push tags ทั้งหมด
git push origin --tags

# Checkout ไปยัง tag
git checkout <tag-name>

# สร้าง branch จาก tag
git checkout -b <branch-name> <tag-name>
```

---

## Git Stash

### การใช้ Stash

```bash
# เก็บการเปลี่ยนแปลงไว้ใน stash
git stash

# เก็บพร้อมข้อความ
git stash save "ข้อความอธิบาย"
git stash push -m "ข้อความอธิบาย"

# เก็บรวมถึงไฟล์ที่ไม่ได้ track
git stash -u
git stash --include-untracked

# เก็บทุกอย่างรวมถึงไฟล์ที่ถูกละเว้น
git stash -a
git stash --all

# เก็บเฉพาะไฟล์เฉพาะ
git stash push <filename>

# เก็บแบบ interactive
git stash -p
git stash --patch
```

### การจัดการ Stash

```bash
# ดู stash ทั้งหมด
git stash list

# ดูการเปลี่ยนแปลงใน stash
git stash show
git stash show -p  # แบบละเอียด

# นำ stash ล่าสุดมาใช้และลบออกจาก stash
git stash pop

# นำ stash เฉพาะมาใช้
git stash pop stash@{1}

# นำ stash มาใช้แต่ไม่ลบออกจาก stash
git stash apply
git stash apply stash@{1}

# ลบ stash เฉพาะ
git stash drop stash@{1}

# ลบ stash ทั้งหมด
git stash clear

# สร้าง branch จาก stash
git stash branch <branch-name>
```

---

## Git Configuration

### การตั้งค่าระดับต่างๆ

```bash
# ตั้งค่าระดับระบบ (ทุกผู้ใช้)
git config --system <key> <value>

# ตั้งค่าระดับผู้ใช้ (user ปัจจุบัน)
git config --global <key> <value>

# ตั้งค่าระดับโปรเจกต์ (repository ปัจจุบัน)
git config --local <key> <value>
git config <key> <value>  # default เป็น --local

# ดูการตั้งค่าทั้งหมด
git config --list

# ดูการตั้งค่าเฉพาะ
git config <key>

# ลบการตั้งค่า
git config --unset <key>
```

### การตั้งค่าที่สำคัญ

```bash
# ข้อมูลผู้ใช้
git config --global user.name "ชื่อผู้ใช้"
git config --global user.email "email@example.com"

# Editor
git config --global core.editor "code --wait"

# Diff tool
git config --global diff.tool vscode
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'

# Merge tool
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'

# การจัดการ line endings
git config --global core.autocrlf true     # Windows
git config --global core.autocrlf input    # Mac/Linux

# การตั้งค่า push default
git config --global push.default simple

# การตั้งค่า pull default
git config --global pull.rebase false

# Aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
```

---

## คำสั่งขั้นสูง

### Git Cherry-pick

```bash
# นำ commit เฉพาะมาใช้
git cherry-pick <commit-hash>

# นำหลาย commit มาใช้
git cherry-pick <commit1> <commit2>

# นำช่วง commit มาใช้
git cherry-pick <start-commit>..<end-commit>

# Cherry-pick โดยไม่ commit
git cherry-pick --no-commit <commit-hash>

# แก้ไขข้อความ commit ขณะ cherry-pick
git cherry-pick --edit <commit-hash>

# ดำเนินการต่อหลังแก้ conflict
git cherry-pick --continue

# ยกเลิก cherry-pick
git cherry-pick --abort
```

### Git Bisect

```bash
# เริ่ม bisect
git bisect start

# กำหนด commit ที่มีปัญหา
git bisect bad <commit-hash>

# กำหนด commit ที่ไม่มีปัญหา
git bisect good <commit-hash>

# ทดสอบ commit ปัจจุบันและกำหนดสถานะ
git bisect good    # ถ้าไม่มีปัญหา
git bisect bad     # ถ้ามีปัญหา

# ข้าม commit ปัจจุบัน
git bisect skip

# เสร็จสิ้น bisect
git bisect reset

# Bisect แบบอัตโนมัติ
git bisect run <command>
```

### Git Submodules

```bash
# เพิ่ม submodule
git submodule add <repository-url> <path>

# โคลน repository พร้อม submodules
git clone --recursive <repository-url>

# เริ่มต้น submodules ใน repository ที่มีอยู่
git submodule init

# อัปเดต submodules
git submodule update

# เริ่มต้นและอัปเดต submodules พร้อมกัน
git submodule update --init

# อัปเดต submodules แบบ recursive
git submodule update --init --recursive

# อัปเดต submodules ไปยังเวอร์ชันล่าสุด
git submodule update --remote

# ดู status ของ submodules
git submodule status

# ลบ submodule
git submodule deinit <path>
git rm <path>
rm -rf .git/modules/<path>
```

### Git Worktree

```bash
# สร้าง worktree ใหม่
git worktree add <path> <branch-name>

# สร้าง worktree พร้อม branch ใหม่
git worktree add -b <new-branch> <path>

# ดู worktrees ทั้งหมด
git worktree list

# ลบ worktree
git worktree remove <path>

# ทำความสะอาด worktree ที่ไม่มีอยู่แล้ว
git worktree prune
```

### Git Archive

```bash
# สร้างไฟล์ archive จาก HEAD
git archive HEAD --format=zip > project.zip

# สร้าง archive จาก branch เฉพาะ
git archive <branch-name> --format=tar.gz > project.tar.gz

# สร้าง archive จาก tag
git archive v1.0 --format=zip --prefix=project-v1.0/ > release.zip

# สร้าง archive เฉพาะโฟลเดอร์
git archive HEAD:src/ --format=zip > src.zip
```

### Git Filter-branch และ Git Filter-repo

```bash
# ลบไฟล์ออกจากประวัติทั้งหมด (ใช้ filter-branch - deprecated)
git filter-branch --force --index-filter \
  'git rm --cached --ignore-unmatch <filename>' \
  --prune-empty --tag-name-filter cat -- --all

# ใช้ git-filter-repo (แนะนำ)
# ติดตั้งก่อน: pip install git-filter-repo

# ลบไฟล์ออกจากประวัติ
git filter-repo --path <filename> --invert-paths

# ลบโฟลเดอร์ออกจากประวัติ
git filter-repo --path <folder-name> --invert-paths

# เปลี่ยนชื่อผู้เขียน
git filter-repo --commit-callback '
  if commit.author_name == b"Old Name":
    commit.author_name = b"New Name"
    commit.author_email = b"new@email.com"
'
```

---

## เทคนิคและ Best Practices

### Git Aliases ที่มีประโยชน์

```bash
# ตั้งค่า aliases ที่มีประโยชน์
git config --global alias.s status
git config --global alias.a add
git config --global alias.c commit
git config --global alias.cm 'commit -m'
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.df diff
git config --global alias.dfs 'diff --staged'

# Log aliases
git config --global alias.lg "log --oneline --graph --decorate --all"
git config --global alias.ll "log --pretty=format:'%C(yellow)%h%Creset %C(blue)%ad%Creset %C(green)%an%Creset %s' --date=short"
git config --global alias.last 'log -1 HEAD'

# อื่นๆ
git config --global alias.unstage 'reset HEAD --'
git config --global alias.uncommit 'reset --soft HEAD~1'
git config --global alias.amend 'commit --amend --no-edit'
git config --global alias.pushf 'push --force-with-lease'
```

### การจัดการ .gitignore

```bash
# สร้างไฟล์ .gitignore
touch .gitignore

# ตัวอย่างเนื้อหาในไฟล์ .gitignore
echo "
# Dependencies
node_modules/
vendor/

# Build outputs
dist/
build/
*.exe
*.dll

# Logs
*.log
logs/

# Environment variables
.env
.env.local

# IDE files
.vscode/
.idea/
*.swp
*.swo

# OS files
.DS_Store
Thumbs.db

# Temporary files
*.tmp
*.temp
" > .gitignore

# ลบไฟล์ที่ถูก track แล้วออกจาก Git
git rm --cached <filename>

# อัปเดต .gitignore สำหรับไฟล์ที่ถูก track แล้ว
git rm -r --cached .
git add .
git commit -m "Update .gitignore"
```

### การเขียน Commit Messages ที่ดี

```bash
# รูปแบบ Conventional Commits
# <type>(<scope>): <description>
#
# <body>
#
# <footer>

# ตัวอย่าง:
git commit -m "feat(auth): add login with Google OAuth

- Implement Google OAuth 2.0 integration
- Add login button to homepage
- Handle authentication errors

Closes #123"

# Types ที่นิยมใช้:
# feat: คุณสมบัติใหม่
# fix: แก้ไขบั๊ก
# docs: อัปเดตเอกสาร
# style: แก้ไขรูปแบบโค้ด
# refactor: ปรับปรุงโค้ดโดยไม่เปลี่ยนการทำงาน
# test: เพิ่มหรือแก้ไขการทดสอบ
# chore: งานจัดการโปรเจกต์
```

### Git Hooks

```bash
# ดู hooks ที่มีอยู่
ls .git/hooks/

# สร้าง pre-commit hook
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/bash
# ตรวจสอบรูปแบบโค้ดก่อน commit
npm run lint
EOF

chmod +x .git/hooks/pre-commit

# สร้าง commit-msg hook
cat > .git/hooks/commit-msg << 'EOF'
#!/bin/bash
# ตรวจสอบรูปแบบข้อความ commit
commit_regex='^(feat|fix|docs|style|refactor|test|chore)(\(.+\))?: .{1,50}'

if ! grep -qE "$commit_regex" "$1"; then
    echo "Invalid commit message format!"
    echo "Format: type(scope): description"
    exit 1
fi
EOF

chmod +x .git/hooks/commit-msg
```

### การแก้ไขปัญหาทั่วไป

```bash
# แก้ไข "fatal: refusing to merge unrelated histories"
git pull --allow-unrelated-histories

# ลบ branch ที่ถูกลบใน remote แล้ว
git remote prune origin

# แก้ไข line ending issues
git config core.autocrlf true  # Windows
git config core.autocrlf input # Mac/Linux

# ลบ credentials ที่เก่า
git config --global --unset credential.helper

# แก้ไข "SSL certificate problem"
git config --global http.sslverify false  # ไม่แนะนำสำหรับ production

# ตั้งค่า proxy
git config --global http.proxy http://proxy.company.com:8080
git config --global https.proxy https://proxy.company.com:8080

# ลบการตั้งค่า proxy
git config --global --unset http.proxy
git config --global --unset https.proxy
```

### การเพิ่มประสิทธิภาพ

```bash
# ทำความสะอาด repository
git gc

# ทำความสะอาดแบบ aggressive
git gc --aggressive

# ตรวจสอบขนาด repository
git count-objects -vH

# ลด shallow clone ให้เป็น full clone
git fetch --unshallow

# Clone แบบ partial (Git 2.19+)
git clone --filter=blob:none <url>

# ตั้งค่า maintenance
git maintenance start
git maintenance run

# การตั้งค่าสำหรับ repository ใหญ่
git config core.preloadindex true
git config core.fscache true
git config gc.auto 256
```

### Git Flow Workflow

```bash
# เริ่มต้นโปรเจกต์ใหม่
git flow init

# เริ่ม feature ใหม่
git flow feature start <feature-name>

# เสร็จสิ้น feature
git flow feature finish <feature-name>

# เริ่ม release ใหม่
git flow release start <version>

# เสร็จสิ้น release
git flow release finish <version>

# เริ่ม hotfix
git flow hotfix start <version>

# เสร็จสิ้น hotfix
git flow hotfix finish <version>
```

### การ Backup และ Recovery

```bash
# สร้าง backup
git bundle create backup.bundle --all

# Restore จาก backup
git clone backup.bundle restored-repo

# สร้าง mirror repository
git clone --mirror <original-repo-url>

# Recovery commit ที่หายไป
git reflog
git cherry-pick <lost-commit-hash>

# กู้คืนไฟล์ที่ถูกลบ
git ls-files --deleted
git checkout HEAD -- <deleted-file>
```

### การวิเคราะห์ Repository

```bash
# วิเคราะห์ contributor
git shortlog -sn

# ดูไฟล์ที่เปลี่ยนแปลงบ่อยที่สุด
git log --name-only --pretty=format: | grep -v "^$" | sort | uniqc -c | sort -rn

# ดูขนาดของไฟล์ใน repository
git ls-tree -r -t -l --full-name HEAD | sort -n -k 4

# วิเคราะห์การเปลี่ยนแปลงต่อวัน
git log --format="%ad" --date=short | sort | uniq -c

# ดูจำนวนบรรทัดที่เพิ่ม/ลบ
git log --shortstat --pretty=format: | grep -E "fil(e|es) changed" | awk '{files+=$1; inserted+=$4; deleted+=$6} END {print "Files changed:", files, "Lines inserted:", inserted, "Lines deleted:", deleted}'
```

---

## สรุป

Git เป็นเครื่องมือที่ทรงพลังสำหรับการจัดการเวอร์ชันของโค้ด คู่มือนี้ครอบคลุมคำสั่งและเทคนิคต่างๆ ตั้งแต่พื้นฐานจนถึงขั้นสูง การฝึกฝนใช้คำสั่งเหล่านี้อย่างสม่ำเสมอจะช่วยให้คุณเชี่ยวชาญ Git และสามารถจัดการโปรเจกต์ได้อย่างมีประสิทธิภาพ

### เคล็ดลับสำหรับมือใหม่

1. **เริ่มจากคำสั่งพื้นฐาน**: `git add`, `git commit`, `git push`, `git pull`
2. **ใช้ `git status` บ่อยๆ**: เพื่อตรวจสอบสถานะของไฟล์
3. **เขียน commit message ที่ดี**: อธิบายการเปลี่ยนแปลงอย่างชัดเจน
4. **สร้าง branch สำหรับ feature ใหม่**: อย่าทำงานใน main branch โดยตรง
5. **ใช้ `.gitignore`**: เพื่อไม่ให้ไฟล์ที่ไม่ต้องการถูก track

### แหล่งข้อมูลเพิ่มเติม

- [Git Official Documentation](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Interactive Git Tutorial](https://learngitbranching.js.org/)

จำไว้ว่า Git มีความซับซ้อน แต่ด้วยการฝึกฝนและใช้งานอย่างสม่ำเสมอ คุณจะเชี่ยวชาญและใช้ประโยชน์จาก Git ได้อย่างเต็มที่!