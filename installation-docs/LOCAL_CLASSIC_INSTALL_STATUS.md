# وضعیت نصب محلی AzerothCore Classic

تاریخ: 2026-05-27

## انجام‌شده

* پیکربندی بیلد CMake در `C:/Build` انجام شد.
* AzerothCore با حالت `RelWithDebInfo` بیلد شد.
* فایل‌های DLL موردنیاز برای اجرا در کنار فایل‌های اجرایی سرور کپی شدند:

  * `libmysql.dll`
  * `legacy.dll`
  * `libcrypto-3-x64.dll`
  * `libssl-3-x64.dll`
* فایل‌های تنظیمات اجرایی از فایل‌های `.dist` ساخته شدند:

  * `C:/Build/bin/RelWithDebInfo/configs/authserver.conf`
  * `C:/Build/bin/RelWithDebInfo/configs/worldserver.conf`
  * `C:/Build/bin/RelWithDebInfo/configs/dbimport.conf`
* دیتای رسمی AC Data v19 enUS دانلود و استخراج شد در:

  * `C:/Build/bin/RelWithDebInfo/Data`
* مقدار `DataDir` در فایل `worldserver.conf` روی مسیر زیر تنظیم شد:

  * `C:/Build/bin/RelWithDebInfo/Data`
* کاربر و دیتابیس‌های MySQL با تنظیمات پیش‌فرض AzerothCore ساخته شدند:

  * نام کاربری: `acore`
  * رمز عبور: `acore`
  * دیتابیس‌ها: `acore_auth`، `acore_characters`، `acore_world`
* دیتابیس‌ها با استفاده از `dbimport.exe` مقداردهی و به‌روزرسانی شدند.
* اجرای صحیح سرورها بررسی شد:

  * `authserver.exe` روی پورت `3724` در حال گوش دادن بود.
  * `worldserver.exe` روی پورت `8085` در حال گوش دادن بود.
  * `worldserver.exe` به اعلان کنسول `AC>` رسید.

## اجرای سرور

یک پنجره PowerShell باز کنید:

```powershell
cd C:/Build/bin/RelWithDebInfo
./authserver.exe
```

یک پنجره PowerShell دوم باز کنید:

```powershell
cd C:/Build/bin/RelWithDebInfo
./worldserver.exe
```

در کنسول `worldserver.exe` یک حساب آزمایشی بسازید:

```text
account create USERNAME PASSWORD
account set gmlevel USERNAME 3 -1
```

## نیازمندی کلاینت

AzerothCore فقط سرور است. برای بازی، به یک کلاینت جداگانه‌ی World of Warcraft نسخه 3.3.5a نیاز دارید.

بعد از نصب یا استخراج کلاینت، فایل `Wow.exe` را در پوشه کلاینت پیدا کنید و فایل realmlist کلاینت را به شکل زیر تنظیم کنید:

```text
set realmlist 127.0.0.1
```

فایل realmlist معمولاً در یکی از مسیرهای زیر داخل پوشه کلاینت WoW قرار دارد:

* `Data/realmlist.wtf`
* `Data/enUS/realmlist.wtf`
* `Data/enGB/realmlist.wtf`

سپس `Wow.exe` را اجرا کرده و با حسابی که در `worldserver.exe` ساخته‌اید وارد بازی شوید.
