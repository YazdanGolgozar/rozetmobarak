# برای تو، بُشرا 💗

سایت فارسی و راست‌به‌چپ روز دختر، از طرف یزدان: دسته‌گل اختصاصی، نامهٔ بازشدنی، چهار کارت، سه سورپرایز و آهنگ «مرگ رویا» از کوروش.

HTML، CSS و JavaScript ساده؛ بدون وابستگی نصب‌شدنی، بک‌اند یا کلید API.

## اجرا

Node.js نسخهٔ ۲۲ یا بالاتر لازم است؛ نسخهٔ پیشنهادی در `.node-version` ثبت شده است.

```sh
npm start
```

یا بدون npm:

```sh
node scripts/serve.mjs
```

سایت در `http://localhost:4173` باز می‌شود. سرور ابتدا خروجی را می‌سازد. نصب بسته لازم نیست. برای پورت دیگر، متغیر محیطی `PORT` را تنظیم کنید. دستور قدیمی `node server.mjs` هم کار می‌کند.

## ساختار مخزن

```text
src/
  index.html       ساختار فارسی صفحه
  styles.css       ظاهر و طراحی واکنش‌گرا
  config.js        نام‌ها، پیام‌ها و موسیقی
  app.js           نامه، کارت‌ها، هدیه‌ها و بازنشانی
  music.js         پلیر آنلاین و فایل صوتی محلی
public/
  assets/          تصویرها و فونت محلی
    audio/         فایل آهنگ همراه پروژه
scripts/
  build.mjs        ساخت dist از src و public
  check.mjs        بررسی کد، تنظیمات و دارایی‌ها
  serve.mjs        پیش‌نمایش و پشتیبانی از seek فایل صوتی
tests/
  serve.test.mjs   آزمون HTTP و درخواست‌های Range
.github/workflows/
  ci.yml           بررسی خودکار روی push و pull request
  pages.yml        انتشار دستی با GitHub Pages
docs/assets.md     منابع و مجوزها
dist/              خروجی تولیدی؛ در Git ثبت نمی‌شود
```

سورس در `src/` و دارایی‌ها در `public/` هستند. `dist/` در هر ساخت دوباره تولید می‌شود؛ آن را دستی ویرایش نکنید. تنظیمات همان سایت قبلی در `.openai/hosting.json` حفظ شده است و در بستهٔ قابل‌انتقال Git صادر نمی‌شود.

## شخصی‌سازی

همهٔ نام‌ها، مناسبت، نامه، کارت‌ها، هدیه‌ها و موسیقی در `src/config.js` قرار دارند. جایگزین‌های `{recipient}`، `{sender}` و `{occasion}` خودکار پر می‌شوند. `date: null` یعنی تاریخی نمایش داده نشود. عکس یا خاطرهٔ شخصی ساخته نشده است.

پس از ویرایش، `npm run build` یا `node scripts/build.mjs` را اجرا و مرورگر را تازه کنید.

## موسیقی

فایل «مرگ رویا» از کوروش که کاربر فراهم کرده، داخل `public/assets/audio/marge-roya.mp3` همراه سورس قرار دارد. با ساخت پروژه، فایل به `dist/assets/audio/marge-roya.mp3` کپی می‌شود. پلیر با مسیر نسبی `assets/audio/marge-roya.mp3` از فایلِ همان سایت پخش می‌کند و برای موسیقی به سرویس خارجی نیاز ندارد.

روی «مرگ رویا» در سربرگ و سپس «پخش آهنگ» بزنید. پخش خودکار وجود ندارد. دکمهٔ توقف، خروج از زبانه و شروع دوباره، پخش را متوقف می‌کنند. لینک «باز کردن آهنگ» همچنان صفحهٔ معرفی آهنگ در Radio Javan را باز می‌کند.

«پخش از دستگاه» هم برای انتخاب فایل صوتی دیگر موجود است؛ فایل انتخابی فقط در مرورگر پخش می‌شود و آپلود یا ذخیره نمی‌شود.

برای تعویض آهنگ، فایل را در `public/assets/audio/` قرار دهید و `music.src` را در `src/config.js` تغییر دهید:

```js
music: {
  enabled: true,
  title: 'مرگ رویا',
  artist: 'کوروش',
  provider: 'audio',
  url: 'https://play.radiojavan.com/song/koorosh-marge-roya',
  src: 'assets/audio/marge-roya.mp3',
  loop: true,
  volume: 0.55
}
```

اگر فایل محلی تنظیم‌شده وجود نداشته باشد، دستور check با خطا متوقف می‌شود. `src` می‌تواند لینک HTTPS فایل صوتی هم باشد. پشتیبانی اختیاری از پلیر SoundCloud حفظ شده است: `provider: 'soundcloud'`، `url: 'https://soundcloud.com/koorowsh420/marge-roya'` و `src: null`. منابع و مجوز فونت در `docs/assets.md` ثبت شده‌اند.

## بررسی و ساخت

```sh
npm run check
npm test
npm run build
```

معادل‌های بدون npm:

```sh
node scripts/check.mjs
node --test
node scripts/build.mjs
```

بعد از ساخت، محتویات `dist/` قابل میزبانی روی هاست استاتیک است. مسیرهای نسبی با آدرس پروژه‌های GitHub Pages سازگارند. `dist/index.html` را هم می‌توان مستقیم باز کرد؛ پخش آنلاین به محدودیت‌های مرورگر و شبکه وابسته است.

## Git و GitHub Pages

سورس و دارایی‌ها داخل Git قرار می‌گیرند؛ خروجی، بسته‌های دانلودی، گزارش‌ها، وابستگی‌ها و `.env` در `.gitignore` کنار گذاشته شده‌اند. `.gitattributes` پایان خطوط و فایل‌های باینری را مدیریت می‌کند. هیچ مخزن GitHub خودکار ایجاد نشده است.

اگر از ZIP شروع می‌کنید و مخزن خالی در GitHub دارید:

```sh
git init -b main
git add .
git commit -m "Add Boshra gift website"
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
git push -u origin main
```

نشانی نمونه را با نشانی مخزن خودتان جایگزین کنید. برای مخزن موجود، مرحلهٔ ساخت مخزن را انجام ندهید و remote همان مخزن را حفظ کنید.

برای GitHub Pages:

1. در Settings → Pages، منبع انتشار را **GitHub Actions** قرار دهید.
2. در Actions، گردش‌کار **Publish GitHub Pages** را باز کنید.
3. **Run workflow** را روی شاخهٔ `main` اجرا کنید.

انتشار Pages دستی است. **Check website** روی push و pull request اجرا می‌شود. گردش‌کارها مطابق [راهنمای GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages) هستند؛ انتشار واقعی به تنظیمات مخزن شما نیاز دارد.

## دسترس‌پذیری

کنترل‌های صفحه‌کلید، تمرکز قابل مشاهده، نامهٔ کامل برای صفحه‌خوان، پنجره‌های قابل‌بستن، فونت فارسی محلی و کاهش حرکت سیستم پشتیبانی می‌شوند. آغاز دوباره، نامه، هدیه‌ها و موسیقی را بازنشانی می‌کند.
