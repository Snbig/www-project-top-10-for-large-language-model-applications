## LLM02:2025 افشای اطلاعات حساس

### توضیحات

اطلاعات حساس می‌توانند هم مدل زبانی بزرگ (LLM) و هم برنامه آن را تحت تاثیر قرار دهد. این اطلاعات شامل اطلاعات شخصی قابل شناسایی (PII)، جزئیات مالی، سوابق سلامت، داده‌های محرمانه کسب‌وکار، اعتبارنامه‌های امنیتی و اسناد حقوقی هستند. همچنین مدل‌های انحصاری، به ویژه مدل‌های بسته یا پایه‌ای، ممکن است روش‌های آموزش منحصر‌به‌فرد و کد منبعی داشته باشند که  حساس تلقی می‌شوند.

مدل‌های زبانی بزرگ (LLM)، به ویژه هنگامی که در برنامه‌ها تعبیه می‌شوند، مخاطره افشای داده‌های حساس، الگوریتم‌های انحصاری یا جزئیات اعتبارنامه‌ها را از طریق خروجی خود دارند. این موضوع می‌تواند منجر به دسترسی غیرمجاز به داده‌ها، نقض حریم خصوصی و نقض مالکیت معنوی شود. مصرف‌کنندگان باید از نحوه تعامل ایمن با مدل‌های زبانی بزرگ (LLM) آگاه باشند. آن‌ها باید مخاطرات ارائه ناخواسته داده‌های حساس را که ممکن است بعداً در خروجی مدل افشا شوند، درک کنند.

برای کاهش این خطر، برنامه‌های مبتنی بر مدل‌های زبانی بزرگ (LLM) باید به اندازه‌ی کافی پاک‌سازی داده‌ها را انجام دهند تا از ورود داده‌های کاربر به مدل آموزشی جلوگیری کنند. صاحبان برنامه همچنین باید خط مشی‌های صریح ضوابط استفاده را ارائه دهند که به کاربران اجازه می‌دهد از وارد شدن داده‌هایشان در مدل آموزشی انصراف دهند. افزودن محدودیت‌هایی در پرامپت سیستم در مورد انواع داده‌هایی که مدل زبانی بزرگ (LLM) باید برگرداند، می تواند راهکاری برای جلوگیری از افشای اطلاعات حساس باشد. با این حال، چنین محدودیت‌هایی ممکن است همیشه رعایت نشوند و بتوان از طریق «تزریق پرامپت» یا روش‌های دیگر آن‌ها را دور زد.

### نمونه‌های رایج از مخاطرات امنیتی

#### ۱. نشت اطلاعات شخصی قابل شناسایی (PII)
اطلاعات شخصی قابل شناسایی (PII) ممکن است در طول تعامل با مدل زبانی بزرگ (LLM) افشا شود.
#### ۲. افشای الگوریتم انحصاری
  خروجی‌های مدل با پیکربندی ضعیف می‌توانند الگوریتم‌ها یا داده‌های اختصاصی را افشا کنند. افشای داده‌های آموزشی می‌تواند مدل‌ها را در معرض حملات وارونگی (Inversion Attacks) قرار دهد، که در آن مهاجمان اطلاعات حساس را استخراج کرده یا ورودی‌ها را بازسازی می‌کنند. برای مثال، همان‌طور که در حمله Proof Pudding (CVE-2019-20634) نشان داده شده‌ است، داده‌های آموزشی افشا شده، استخراج و وارونگی مدل را تسهیل کردند و به مهاجمان اجازه دادند تا کنترل‌های امنیتی موجود در الگوریتم‌های یادگیری ماشین و پالایشگرهای رایانامه را دور بزنند.
#### ۳. افشای داده‌های حساس کسب‌و‌کار
  پاسخ‌های تولیدشده ممکن است به طور ناخواسته شامل اطلاعات محرمانه کسب‌وکار باشند.

### راهبردهای پیشگیری و کاهش مخاطره

#### پاک‌سازی:

#### ۱. ادغام روش‌های پاک‌سازی داده
  پاک‌سازی داده‌‌ها را برای جلوگیری از ورود داده‌های کاربر به مدل آموزشی پیاده‌سازی کنید. این کار شامل حذف یا پوشاندن محتوای حساس قبل از استفاده از آن برای آموزش است.
#### ۲. اعتبارسنجی قوی ورودی
  روش‌های اعتبارسنجی ورودی سخت‌گیرانه‌ای را برای شناسایی و پالایش ورودی‌های حاوی داده‌های بالقوه زیان‌بار یا حساس اعمال کنید تا اطمینان حاصل شود که مدل را به خطر نمی‌اندازند.

#### کنترل‌های دسترسی:

#### ۱. اعمال کنترل‌های دسترسی سخت‌گیرانه
  دسترسی به داده‌های حساس را بر اساس اصل حداقل امتیاز (Least Privilege) محدود کنید. اجازه‌ی دسترسی را فقط به داده‌هایی بدهید که برای یک کاربر مشخص یا فرایند خاص ضروری است.
#### ۲. محدود‌ کردن منابع داده
  دسترسی مدل را به منابع داده خارجی محدود کنید و اطمینان حاصل کنید که هماهنگ‌سازی داده‌ها در زمان اجرا به طور امن مدیریت می‌شود تا از نشت ناخواسته داده‌ها جلوگیری شود.

#### یادگیری هم‌افزا (Federated Learning) و روش‌های حفظ حریم خصوصی:

#### ۱. استفاده از یادگیری هم‌افزا
  مدل‌ها را با استفاده از داده‌های غیرمتمرکز ذخیره‌شده در چندین سرور یا دستگاه آموزش دهید. این رویکرد نیاز به جمع‌آوری داده‌های متمرکز را به حداقل می‌رساند و خطرات افشا را کاهش می‌دهد.
#### 2. به‌کارگیری حریم خصوصی تفاضلی (Differential Privacy)
  از روش‌هایی استفاده کنید که نویز را به داده‌ها یا خروجی‌ها اضافه می‌کنند و برای مهاجمان، مهندسی معکوس نقاط داده فردی را دشوار می‌سازند.

#### آموزش کاربر و شفافیت:

#### ۱. آموزش کاربران در خصوص استفاده ایمن از LLM
  راهنمایی‌هایی در مورد اجتناب از وارد کردن اطلاعات حساس ارائه دهید. آموزش‌هایی در مورد به‌روش‌ها برای تعامل ایمن با مدل‌های زبانی بزرگ (LLM) ارائه دهید.
#### 2. تضمین شفافیت در استفاده از داده‌ها
  سیاست‌های روشنی در مورد نگهداری، استفاده و حذف داده‌ها داشته‌باشید. به کاربران اجازه دهید تا از گنجاندن داده‌هایشان در فرآیندهای آموزش انصراف دهند.

#### پیکربندی امن سامانه:

#### ۱. مخفی‌سازی تنظیمات اولیه سامانه
  توانایی کاربران برای بازنویسی یا دسترسی به تنظیمات اولیه سامانه را محدود کنید و به این ترتیب خطر افشای تنظیمات داخلی را کاهش دهید.
#### ۲. ارجاع به به‌روش‌های «پیکربندی نادرست امنیتی»
  برای جلوگیری از افشای اطلاعات حساس از طریق پیام‌های خطا یا جزئیات پیکربندی، از دستورالعمل‌هایی مانند «OWASP API8:2023 پیکربندی نادرست امنیتی» پیروی کنید.
  (پیوند مرجع:[OWASP API8:2023 Security Misconfiguration](https://owasp.org/API-Security/editions/2023/en/0xa8-security-misconfiguration/))

#### روش‌های پیشرفته:

#### ۱. رمزگذاری هم‌ریختی
  از رمزگذاری هم‌ریختی برای تجزیه و تحلیل امن داده‌ها و یادگیری ماشین با حفظ حریم خصوصی استفاده کنید. این کار تضمین می‌کند که داده‌ها در حین پردازش توسط مدل، محرمانه باقی می‌مانند.
#### ۲. نشانه‌گذاری و ویرایش
  برای پیش‌پردازش و پاک‌سازی اطلاعات حساس، نشانه‌گذاری (tokenization) را پیاده‌سازی کنید. تکنیک‌هایی مانند تطبیق الگو (Pattern Matching) می‌توانند محتوای محرمانه را قبل از پردازش شناسایی و ویرایش کنند.

### نمونه‌هایی از فرانامه‌های حمله

#### فرانامه #۱: افشای غیرعمدی داده‌ها
  کاربر به دلیل پاک‌سازی ناکافی داده‌ها، پاسخی حاوی داده‌های شخصی کاربر دیگری را دریافت می‌کند.
#### فرانامه #۲: تزریق هدفمند پرامپت
  مهاجم پالایشگرهای ورودی را دور می‌زند تا اطلاعات حساس را استخراج کند.
#### فرانامه #۳: نشت داده از طریق داده‌های آموزش
  درج سهل‌انگارانه‌ی داده‌ها در آموزش، منجر به افشای اطلاعات حساس می‌شود.

### پیوندهای مرجع

1. [Lessons learned from ChatGPT’s Samsung leak](https://cybernews.com/security/chatgpt-samsung-leak-explained-lessons/): **Cybernews**
2. [AI data leak crisis: New tool prevents company secrets from being fed to ChatGPT](https://www.foxbusiness.com/politics/ai-data-leak-crisis-prevent-company-secrets-chatgpt): **Fox Business**
3. [ChatGPT Spit Out Sensitive Data When Told to Repeat ‘Poem’ Forever](https://www.wired.com/story/chatgpt-poem-forever-security-roundup/): **Wired**
4. [Using Differential Privacy to Build Secure Models](https://neptune.ai/blog/using-differential-privacy-to-build-secure-models-tools-methods-best-practices): **Neptune Blog**
5. [Proof Pudding (CVE-2019-20634)](https://avidml.org/database/avid-2023-v009/) **AVID** (`moohax` & `monoxgas`)

### چارچوب‌ها و طبقه‌بندی‌های مرتبط

برای کسب اطلاعات جامع، فرانامه‌ها، راهبردهای مربوط به استقرار زیرساخت، کنترل‌های محیطی کاربردی و سایر به‌روش‌ها، به این بخش مراجعه کنید.

- [AML.T0024.000 - Infer Training Data Membership](https://atlas.mitre.org/techniques/AML.T0024.000) **MITRE ATLAS**
- [AML.T0024.001 - Invert ML Model](https://atlas.mitre.org/techniques/AML.T0024.001) **MITRE ATLAS**
- [AML.T0024.002 - Extract ML Model](https://atlas.mitre.org/techniques/AML.T0024.002) **MITRE ATLAS**