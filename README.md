
![[Pasted image 20250330153429.png]]


## **🔹 أوامر Git الأساسية**

### **🔹 1) إعداد Git لأول مرة**

بعد التثبيت، لازم تضبط اسمك وبريدك الإلكتروني علشان يكونوا موجودين في كل التعديلات اللي بتعملها:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

للتحقق من الإعدادات:

```bash
git config --list        ==      git config -l

#  للتعديل من خلال ال editor 
git config --global --edit     
#  لحذف config
git config --global --unset user.name
#  لعرض كل ال Config الممكنه
git help config             


#   إنشاء مفتاح SSH جديد
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
#   تجربة الاتصال بـ GitHub
ssh -T git@github.com

#  لعمل اسم مستعار لامر ما للتسهيل في الكتابه
git config --global alias.st status
git config --global alias.br branch
git config --global alias.cm "commit -m"
```

### **🔹 2) إنشاء مستودع جديد (Repository)**

لو عندك مشروع موجود على جهازك، ادخل عليه بـ **Terminal** واكتب: ده هيحول الفولدر لمستودع Git.

```bash
git init


git ls-files -s            # عشان تشوف الحاجات الي في ال Stagging Area (index)
```

### **🔹 3) إضافة الملفات للتتبع (Staging Area)**

كل ملف بتعدّله لازم تضيفه يدويًا قبل ما تعمله **commit**:

```bash
git add filename
```

ولو عاوز تضيف كل الملفات المعدلة:

```bash
git add .            #   . / *

git add *.txt          #   . / *
```

ولو عاوز تنزل ملف من ال Stage Area:

```bash
git reset head filename
```

### **🔹 4) حفظ التعديلات (Commit)**

بعد ما تضيف الملفات، احفظ التعديلات في Git عن طريق **commit** برسالة توضح التغيير اللي عملته:

```bash
git commit -m "شرح Git & GitHub من الصفر للاحتراف"
```

### **🔹 5) عرض حالة المستودع**

لو عاوز تعرف إيه الملفات المعدلة اللي لسه متمش إضافتها أو حفظها:

```bash
git status
```

### **🔹 6) استعراض سجل التعديلات**

لو عاوز تشوف تاريخ كل الـ commits اللي عملتها:

```bash
git log
```

ولو عاوز نسخة مختصرة:

```bash
git log --oneline
```

### **🔹7) # كل شيء عن ال Restore وال Clean**

```bash
#  لو عاوز تنزل الملف من ال Stage changes ==> changes (untracked)
git restore --staged file-name
git restore --staged *

# لعرض كل الملفات الي هتتحذف من ال untracked stage
git clean -n
# لتنفيذ امر الحذف 
git clean -f
```

---
## **🔹 العمل مع GitHub**

### **🔹 1) إنشاء مستودع جديد على GitHub**

### **🔹 2) ربط المستودع المحلي بـ GitHub**

داخل الفولدر اللي فيه الكود، نفّذ الأمر التالي لاستبدال `<your-repo-url>` برابط المستودع اللي أنشأته:

```bash
git remote add origin <your-repo-url>
```

تقدر تتأكد إن الربط تم:

```bash
git remote -v
```

### **🔹 3) رفع الملفات إلى GitHub**

بعد ما تربط المستودع، ارفع الملفات لأول مرة باستخدام:

```bash
git branch -M master  # تأكد إن الفرع الرئيسي اسمه main

git push -u origin master
```

بعد كده أي تعديلات ترفعها بـ:

```bash
git push origin master
```

---
## **🔹 العمل مع الفروع (Branches)**

الفروع بتسمح لك تشتغل على ميزات جديدة بدون ما تأثر على الكود الرئيسي.
### **🔹 1) إنشاء فرع جديد**

```bash
git branch feature-branch

# بيقولك اي الفروع الي عندك
git branch           
```

### **🔹 2) التبديل للفرع الجديد**

```bash
git checkout feature-branch     ==    git switch feature-branch

# لانشاء فرع جديد والتبديل اليه تلقائيا
git checkout -b feature-branch 

# لحذف فرع بس لو فيه تعديل بيقولك انه مينفعش
git branch -d feature-branch
# بيحذف الفرع بغض النظر فيه تعديلات ولا لا
git branch -D feature-branch

# لتغير اسم الفرع
git branch -m Development
```

### **🔹 3) دمج الفرع الجديد مع الفرع الرئيسي**

بعد ما تخلص التعديلات وتعمل **commit**، ارجع للفرع الرئيسي وادمج الفرع الجديد فيه:

```bash
git checkout master
git merge feature-branch
```

---
## **🔹 جلب التعديلات (Pull) ومزامنة الكود**

لو شغال في فريق، لازم تحدث الكود عندك بأحدث نسخة من GitHub قبل ما تضيف تعديلاتك:

```bash
git pull origin master
```

---
## **🔹 حل التعارضات (Merge Conflicts)**

لو اشتغلت انت وزميلك على نفس الملف، ممكن يحصل تعارض عند الدمج. Git هيقولك تحل التعارض يدويًا عن طريق فتح الملف وحذف التعديلات غير المطلوبة.

بعد حل التعارض، أضف التعديل:

```bash
git add .
git commit -m "حل التعارض"
git push origin main
```

---
## **🔹 استنساخ مستودع من GitHub**

لو عاوز تنسخ مشروع موجود على GitHub عندك محليًا:

```bash
git clone <repo-url>
```

---
## **🔹 استخدام .gitignore**

لو عندك ملفات خاصة متحبش ترفعها (زي ملفات الـ cache أو البيئات الافتراضية)، استخدم ملف **.gitignore** واضف فيه الملفات اللي متحبش تتضاف.  
مثال لملف `.gitignore` في مشروع Python:

```bash
*.log              # اي ملف بالامتداد ده مش هيتضاف 
!youssef.log       # ما عدا الملف الي اسمه كده
node_packs/        # برضه الملف ده متضيفوش
youssef.html       # ممكن تكتب اسم الملف نفسه وامتداده
.gitignore         # ممكن احط الملف نفسه
```

---
## **🔥 نصائح احترافية**

✅ اعمل Commitات صغيرة وسهلة الفهم.  
✅ استخدم أسماء فروع واضحة زي `feature-authentication`.  
✅ استخدم Pull Requests لمراجعة الكود قبل الدمج.  
✅ راجع **GitHub Actions** لأتمتة CI/CD.

---
# **🚀 Advanced Git Features**

## 0️⃣التعامل مع الـ Tags والـ Releases في Git

### 📌 **ما هي الـ Tags في Git؟**

الـ **Tags** في Git تُستخدم للإشارة إلى نقاط محددة في تاريخ المستودع، وعادةً ما يتم استخدامها لتحديد إصدارات البرامج. هناك نوعان رئيسيان:

1. **Lightweight Tags**: مجرد مرجع (pointer) إلى commit معين.

2. **Annotated Tags**: تحتوي على بيانات إضافية مثل الاسم، البريد الإلكتروني، والتاريخ، ويمكن توقيعها رقميًا.
---
### 🏷️ **إنشاء Tags**

#### **1. إنشاء Lightweight Tag**

```bash
git tag v1.0
```

هذا سيُنشئ tag باسم `v1.0` يشير إلى الـ commit الحالي.

#### **2. إنشاء Annotated Tag**

```bash
git tag -a v1.0 -m "إصدار النسخة الأولى"
```

يضيف وصفًا ويمكن توقيعه إذا كنت تستخدم GPG.

#### **3. إنشاء Tag لالتزام معين (Commit)**

```bash
git tag -a v1.0 3f2e1b4 -m "إصدار النسخة الأولى"
```

حيث `3f2e1b4` هو معرف الـ commit.

---

### 📤 **رفع الـ Tags إلى GitHub أو أي Remote Repository**

#### **1. رفع Tag معين**

```bash
git push origin v1.0
```

#### **2. رفع جميع الـ Tags دفعة واحدة**

```bash
git push origin --tags
```

---
### ❌ **حذف Tags**

#### **1. حذف Tag محليًا**

```bash
git tag -d v1.0
```

#### **2. حذف Tag من الـ Remote Repository**

```bash
git push origin --delete v1.0
```

---

### 🔄 **تحديث أو إعادة إنشاء Tag**

إذا كنت بحاجة لتحديث Tag على commit مختلف:

1. احذفه محليًا وRemote:

    ```bash
    git tag -d v1.0
    git push origin --delete v1.0
    ```

2. أنشئه مجددًا على commit جديد:

    ```bash
    git tag -a v1.0 -m "إصدار جديد"
    git push origin v1.0
    ```

---
### 🚀 **ما هي GitHub Releases؟**

الـ **Releases** على GitHub تُستخدم لإنشاء إصدارات رسمية من مشروعك، وغالبًا ما تكون مرتبطة بـ Tags. يمكن أن تحتوي على ملفات قابلة للتنزيل (مثل الـ binaries) وتوضيحات للإصدار.
#### **إنشاء Release على GitHub**

1. انتقل إلى صفحة المستودع على GitHub.

2. اختر **Releases** > **Draft a new release**.

3. حدد الـ Tag المرتبط بالإصدار.

4. أضف تفاصيل الإصدار (عنوان، وصف، ملفات مرفقة إذا لزم الأمر).

5. اضغط على **Publish Release**.
---
### 🔍 **عرض الـ Tags المتاحة**

```bash
git tag
git tag -l v1.*             # لو عاوز ادور علي تاج معين 
```

لعرض التفاصيل:

```bash
git show v1.0
```

---
## 💡 **متى تستخدم Tags وReleases؟**

- استخدم **Tags** عند الحاجة لتحديد نقطة ثابتة في المشروع (مثل `v1.0`، `v2.0`).

- استخدم **Releases** عندما تريد مشاركة إصدار رسمي مع ملاحظات ومرفقات.

🎯 **باختصار**، الـ **Tags** هي مجرد علامات داخلية، بينما الـ **Releases** تقدم مزيدًا من التوضيح والتنظيم للإصدارات الرسمية، خاصة عند العمل في فرق أو نشر المشاريع بشكل احترافي. 🚀

---
## **1️⃣ التعامل مع Branching & Merging باحترافية**

### **🔹 1) إنشاء فروع متفرعة من فروع أخرى**

بدل ما تعمل فرع جديد من `main`، ممكن تعمل فرع جديد متفرع من فرع آخر:

```bash
git checkout -b new-branch existing-branch
```

أو

```bash
git switch -c new-branch existing-branch
```

### **🔹 2) إعادة تسمية فرع موجود**

```bash
git branch -m old-branch new-branch
```

### **🔹 3) حذف فرع بعد الدمج**

لو خلصت شغل على فرع معين ودمجته، الأفضل تحذفه علشان ميبقاش عندك فوضى:

```bash
git branch -d branch-name
```

ولو عاوز تحذفه حتى لو مش مدموج:

```bash
git branch -D branch-name
```

### **🔹 4) حل مشاكل الدمج (Merge Conflicts)**

لو حصل **conflict** أثناء الدمج، هيظهر لك تنبيه في الملفات المتعارضة، وحلها بيكون يدويًا. بعد التعديل:

```bash
git add .
git commit -m "Fixed merge conflict"
git push origin main
```

---
## **2️⃣ Rebase مقابل Merge - متى تستخدم كل منهما؟**

- **Merge** ➝ يحتفظ بجميع التعديلات والتاريخ الزمني كما هو.

- **Rebase** ➝ يعيد كتابة التاريخ كأن التعديلات تمت مباشرة على الفرع الرئيسي.

### **🔹 تنفيذ Rebase**

```bash
git checkout feature-branch
git rebase main
```

ولو حصل **conflict**، احله ثم:

```bash
git rebase --continue
```

---

## **3️⃣ Stashing - حفظ التعديلات بدون Commit**

لو عندك تعديلات ومحتاج تبدل للفرع الرئيسي بدون ما تعمل **commit**، استخدم **stash** لتخزينها مؤقتًا:

```bash
git stash
```

ولما ترجع عاوز تسترجعها:

```bash
git stash pop
```

ولو عندك أكتر من stash وعاوز تشوف القائمة:

```bash
git stash list

# عاوز اعرف اي الي موجود في ال Stash ده 
git stash save "عباره توضيح"

#  بياخد التعديلات فقط ويسيب ال Stash زي ما هو
git stash apply

# لو عاوز اعرف محتوي Stash معين 
git stash show stash@{index}
```

```bash
# ولمسح stash معين
git stash drop stash@{index}

# لمسح كل ال stash
git stash clear
```

---
## **4️⃣ Cherry-picking - سحب Commit معين من فرع آخر**

لو عندك **commit** معين في فرع تاني وعاوز تجيبه بدون ما تدمج الفرع كله:

```bash
git checkout main
git cherry-pick commit-hash
```

---
## **5️⃣ Squashing - دمج عدة Commits في Commit واحد**

لو عندك **أكثر من commit غير ضروري** وعاوز تدمجهم في **واحد فقط** لتنظيف التاريخ:

```bash
git rebase -i HEAD~3
```

هيفتح لك شاشة فيها الـ commits، غير كلمة `pick` إلى `squash` في الـ commits اللي عاوز تدمجها، ثم احفظ.

---
## **6️⃣ تغيير الـ Commit الأخير**

لو نسيت تضيف ملف أو تعدل الرسالة:

```bash
git commit --amend -m "رسالة جديدة"
```

---
## **7️⃣ Reset مقابل Revert - متى تستخدم كل منهما؟**

- **Reset** ➝ يرجّع الكود لحالة معينة **ويحذف التعديلات** (لا يُفضل في المشاريع المشتركة).

- **Revert** ➝ ينشئ **commit جديد** يعكس التعديلات بدون حذفها.

### **🔹 Reset (لحذف التعديلات)**

```bash
git reset --hard commit-hash(زي عنوان كده)
```

### **🔹 Revert (لعكس التعديلات)**

```bash
git revert commit-hash
```

---
# **🚀 Advanced GitHub Features**

## **8️⃣ Pull Requests - كيف تديرها بشكل احترافي؟**

1. **أنشئ فرع جديد** واشتغل عليه.
    
2. **ادفع التعديلات إلى GitHub** باستخدام `git push`.
    
3. **افتح Pull Request (PR)** من GitHub.
    
4. **اطلب مراجعة الكود من فريقك**.
    
5. **ادمج التعديلات بعد الموافقة**.

### **🔹 إضافة وصف قوي لـ PR**

استخدم Markdown لكتابة وصف واضح، مثل:

```markdown
### What does this PR do?
- Fixes bug #123
- Adds new API endpoint

### How to test?
1. Run `python app.py`
2. Check if `/api/new-feature` returns the expected output.
```

---
## **9️⃣ GitHub Actions - أتمتة تنفيذ الكود (CI/CD)**

**GitHub Actions** تتيح لك تشغيل **اختبارات أو Deploy تلقائي** عند رفع التعديلات.  
مثال لملف `ci.yml` لتنفيذ **اختبارات Python** عند كل **push**:

```yaml
name: Run Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.8'

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Run tests
        run: pytest
```

احفظ الملف في `.github/workflows/ci.yml` وهيشتغل تلقائيًا عند كل push.

---
## **🔟 GitHub CLI - التحكم في GitHub من الـ Terminal**

بدل ما تروح المتصفح، تقدر تدير GitHub من **GitHub CLI** (`gh`).

### **🔹 تثبيت GitHub CLI**

```bash
sudo apt install gh  # Linux
brew install gh      # MacOS
```

### **🔹 تسجيل الدخول**

```bash
gh auth login
```

### **🔹 إنشاء Pull Request من الـ Terminal**

```bash
gh pr create --title "New Feature" --body "Description of changes"
```

---
# **🚀 Advanced Git Configurations**

## **0️⃣ Global .gitignore**

بدل ما تضيف `.gitignore` لكل مشروع، اعمل واحد **عالمي**:

```bash
git config --global core.excludesfile ~/.gitignore_global
```

بعدها أضف الملفات اللي متحبش تتضاف فيه.

---
# **💡 نصائح احترافية**

✅ **استخدم Git Hooks** لتشغيل أكواد معينة قبل أو بعد الـ commit.  
✅ **تعلّم Git Bisect** لتحديد الـ commit اللي سبب مشكلة معينة.  
✅ **استخدم Signed Commits** لو بتشتغل على مشاريع حساسة باستخدام `GPG`.  
✅ **لا تستخدم `git push --force` إلا لو متأكد 100% إنه آمن!**  
✅ **تابع Dashboard GitHub Insights** لفهم نشاط المستودع.
