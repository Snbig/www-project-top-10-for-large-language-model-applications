## LLM05:2025 مدیریت نامناسب خروجی

### توضیحات

مدیریت نامناسب خروجی به طور خاص به اعتبارسنجی، پاک‌سازی و مدیریت ناکافی خروجی‌‌های تولید شده توسط مدل‌های زبانی بزرگ (LLM) اشاره دارد، پیش از آن که به اجزا و سامانه‌های دیگر منتقل شوند. از آنجایی که محتوای تولید شده توسط مدل زبانی بزرگ (LLM) می‌تواند با ورودی پرامپت کنترل شود، این رفتار مشابه ارائه دسترسی غیرمستقیم کاربران به عملکردهای اضافی است.
تفاوت «مدیریت نامناسب خروجی» با «اتکای بیش از حد» (Overreliance) در این است که «مدیریت نامناسب خروجی» به خروجی‌های تولید‌شده توسط مدل زبانی بزرگ (LLM) پیش از آنکه به پایین‌دست منتقل شوند می‌پردازد، در حالی که «اتکای بیش از حد» بر نگرانی‌های کلی‌تری پیرامون وابستگی بیش از حد به دقت و مناسب‌بودن خروجی‌‌های مدل زبانی بزرگ (LLM) تمرکز دارد.
بهره‌برداری (Exploitation) موفقیت‌آمیز از آسیب‌پذیری «مدیریت نامناسب خروجی» می‌تواند منجر به XSS و CSRF در مرورگرهای وب و همچنین SSRF، ارتقا سطح دسترسی، یا اجرای کد از راه دور در سامانه‌های زیرسازه (Back-End) شود.
شرایط زیر می‌توانند تأثیر این آسیب‌پذیری را افزایش دهند:
- برنامه سطوح دسترسی فراتر از آنچه برای کاربران‌نهایی در نظر گرفته شده‌است، به مدل زبانی بزرگ (LLM) می‌دهد و این امر منجر به ارتقای سطح‌دسترسی یا اجرای کد از راه دور می‌شود.
- برنامه نسبت به حملات تزریق غیرمستقیم پرامپت آسیب‌پذیر است، که می‌تواند به مهاجم اجازه دسترسی ممتاز به محیط کاربر هدف را بدهد.
- افزونه‌های شخص ثالث، ورودی‌ها را به اندازه کافی اعتبارسنجی نمی‌کنند.
- عدم کدگذاری مناسب خروجی برای محتواهای مختلف (مانند HTML، Javascript، SQL)
- پایش و رویدادنگاری ناکافی خروجی‌های مدل زبانی بزرگ (LLM)
- عدم وجود محدودیت نرخ یا تشخیص ناهنجاری برای استفاده از مدل زبانی بزرگ (LLM)

### نمونه‌های رایج از مخاطرات امنیتی

1. خروجی مدل زبانی بزرگ (LLM) مستقیماً وارد واسط خط فرمان سیستم (System Shell) یا تابع مشابهی مانند exec یا eval می‌شود که منجر به اجرای کد از راه دور می‌شود.
2. جاوااسکریپت یا Markdown توسط مدل زبانی بزرگ (LLM) تولید و به کاربر بازگردانده می‌شود. سپس این کد توسط مرورگر تفسیر می‌شود که منجر به XSS می‌شود.
3. پرس‌وجوهای SQL تولید شده توسط مدل‌های زبانی بزرگ (LLM) بدون پارامترسازی مناسب اجرا می‌شوند که منجر به تزریق SQL می‌شود.
4. خروجی مدل زبانی بزرگ (LLM) برای ایجاد مسیر‌های فایل بدون پاک‌سازی مناسب استفاده می‌شود که به طور بالقوه منجر به آسیب‌پذیری‌های پیمایش مسیر (Path Traversal) می‌شود.
5. محتوای تولید شده توسط مدل زبانی بزرگ (LLM)، بدون خنثی سازی (Escaping) مناسب در قالب‌‌های رایانامه استفاده می‌شود که به طور بالقوه منجر به حملات فیشینگ (Phishing) می‌شود.

### راهبردهای پیشگیری و کاهش مخاطره

1. مدل را مانند هر کاربر دیگری در نظر بگیرید، یک رویکرد «عدم اعتماد» (Zero-Trust) را اتخاذ کنید و اعتبارسنجی مناسب ورودی را بر روی پاسخ‌هایی که از مدل به توابع زیرسازه (Back-End) می‌رسند، اعمال کنید.
2. از دستورالعمل‌های OWASP ASVS (استاندارد وارسی امنیت برنامه کاربردی) پیروی کنید تا از اعتبارسنجی و پاک‌سازی مؤثر ورودی اطمینان حاصل کنید.
3. برای کاهش اجرای ناخواسته کد توسط جاوااسکریپت یا Markdown، خروجی مدل بازگردانده شده به کاربران را کدگذاری کنید. OWASP ASVS راهنمایی‌های دقیقی در مورد کدگذاری خروجی ارائه می‌دهد.
4. کدگذاری خروجی آگاه از محتوا را بر اساس جایی که خروجی مدل زبانی بزرگ (LLM) استفاده خواهد شد، پیاده سازی کنید (برای مثال، کدگذاری HTML برای محتوای تارنما، خنثی‌سازی (Escaping) SQL برای پرس‌وجوهای پایگاه داده).
5. برای تمام عملیات پایگاه داده که شامل خروجی مدل زبانی بزرگ (LLM) هستند، از پرس‌وجوهای پارامترسازی‌شده (Parameterized Queries) یا عبارات از قبل آماده‌‌شده (Prepared Statements) استفاده کنید.
6. از سیاست‌های امنیتی محتوای (CSP) سختگیرانه برای کاهش مخاطره حملات XSS ناشی از محتوای تولید شده توسط مدل زبانی بزرگ (LLM) استفاده کنید.
7. برای شناسایی الگوهای غیرعادی در خروجی‌های مدل زبانی بزرگ (LLM) که ممکن است نشان‌دهنده تلاش‌های بهره‌برداری (Exploitation) باشد، سامانه‌های قوی رویدادنگاری و پایش را پیاده‌سازی کنید.

### نمونه فرانامه‌های حمله

#### فرانامه #۱
  برنامه کاربردی از یک افزونه‌ی مدل زبانی بزرگ (LLM) برای تولید پاسخ برای یک ویژگی چت‌بات استفاده می‌کند. این افزونه همچنین تعدادی از عملکردهای مدیریتی را ارائه می‌دهد که برای یک LLM ممتاز دیگر قابل دسترسی است. LLM عمومی مستقیماً پاسخ خود را بدون اعتبارسنجی مناسب خروجی، به افزونه منتقل می‌کند و باعث می‌شود که افزونه برای تعمیر و نگهداری خاموش شود.
#### فرانامه #۲
  کاربر از یک ابزار خلاصه‌ساز تارنما که توسط یک مدل زبانی بزرگ (LLM) ارائه می‌شود برای ایجاد خلاصه‌ای مختصر از یک مقاله استفاده می‌کند. این تارنما دارای یک پرامپت تزریق شده است که به LLM دستور می‌دهد تا محتوای حساس را از تارنما یا از مکالمه کاربر استخراج کند. از این رو، LLM داده‌های حساس را کدگذاری کرده و بدون هیچ اعتبارسنجی یا پالایش خروجی به کارساز تحت کنترل مهاجم ارسال می‌کند.
#### فرانامه #۳
  مدل زبانی بزرگ (LLM) به کاربران اجازه می‌دهد تا از طریق یک ویژگی چت‌مانند، پرس‌وجوهای SQL را برای یک پایگاه‌‌ داده سمت سرور ایجاد کنند. کاربری درخواست می‌‌دهد تا پرس‌وجویی برای حذف تمامی جداول پایگاه‌ داده ایجاد شود. اگر پرس‌وجوی ایجاد‌شده توسط LLM به دقت بررسی نشود، تمامی جداول پایگاه داده حذف خواهند شد.
#### فرانامه #۴
  برنامه تحت وب از یک مدل زبانی بزرگ (LLM) برای تولید محتوا از پرامپت‌های متنی کاربر بدون پاک‌سازی خروجی استفاده می‌کند. مهاجم می‌تواند پرامپتی دست‌کاری شده ارسال کند که باعث می‌شود LLM، داده مخرب جاوااسکریپت پاک‌سازی‌نشده را برگرداند و منجر به XSS در هنگام تفسیر در مرورگر قربانی شود. اعتبارسنجی ناکافی پرامپت‌ها این حمله را امکان‌پذیر می‌کند.
#### فرانامه #۵
  از یک مدل زبانی بزرگ (LLM) برای تولید قالب‌های پویای رایانامه برای یک کارزار بازاریابی استفاده می‌‌شود. مهاجم، LLM را به گونه‌ای دستکاری می‌کند تا جاوااسکریپت مخرب را در محتوای رایانامه قرار دهد. اگر برنامه به درستی خروجی LLM را پاک‌سازی نکند، این امر می‌تواند منجر به حملات XSS بر روی گیرندگانی شود که رایانامه را در برنامه‌های مدیریت رایانامه آسیب‌پذیر سمت کاربر مشاهده می‌کنند.
#### فرانامه #۶
  مدل زبانی بزرگ (LLM) با هدف ساده‌سازی وظایف توسعه، برای تولید کد از ورودی‌های زبان طبیعی در یک شرکت نرم‌افزاری استفاده می‌شود. با این که این رویکرد کارآمد است، مخاطرات افشای اطلاعات حساس، ایجاد روش‌های ناامن مدیریت داده‌ها یا ایجاد آسیب‌پذیری‌هایی مانند تزریق SQL را به همراه دارد. هوش مصنوعی همچنین ممکن است به دلیل خطای شناختی، بسته‌های نرم‌افزاری غیرواقعی را معرفی کند، که به طور بالقوه منجر به دریافت منابع آلوده به بدافزار توسط توسعه‌دهندگان می‌شود. بررسی دقیق کد و وارسی بسته‌های پیشنهادی برای جلوگیری از نقض‌های امنیتی، دسترسی غیرمجاز و به خطر افتادن سامانه‌ها بسیار مهم است.

### پیوندهای مرجع

1. [Proof Pudding (CVE-2019-20634)](https://avidml.org/database/avid-2023-v009/) **AVID** (`moohax` & `monoxgas`)
2. [Arbitrary Code Execution](https://security.snyk.io/vuln/SNYK-PYTHON-LANGCHAIN-5411357): **Snyk Security Blog**
3. [ChatGPT Plugin Exploit Explained: From Prompt Injection to Accessing Private Data](https://embracethered.com/blog/posts/2023/chatgpt-cross-plugin-request-forgery-and-prompt-injection./): **Embrace The Red**
4. [New prompt injection attack on ChatGPT web version. Markdown images can steal your chat data.](https://systemweakness.com/new-prompt-injection-attack-on-chatgpt-web-version-ef717492c5c2?gi=8daec85e2116): **System Weakness**
5. [Don’t blindly trust LLM responses. Threats to chatbots](https://embracethered.com/blog/posts/2023/ai-injections-threats-context-matters/): **Embrace The Red**
6. [Threat Modeling LLM Applications](https://aivillage.org/large%20language%20models/threat-modeling-llm/): **AI Village**
7. [OWASP ASVS - 5 Validation, Sanitization and Encoding](https://owasp-aasvs4.readthedocs.io/en/latest/V5.html#validation-sanitization-and-encoding): **OWASP AASVS**
8. [AI hallucinates software packages and devs download them – even if potentially poisoned with malware](https://www.theregister.com/2024/03/28/ai_bots_hallucinate_software_packages/) **Theregiste**
