مرحبا — سأرشدك خطوة بخطوة لإضافة صور الشعار وصور الأصناف إلى ملف المنيو الذي أرسلتَه. سأشرح خطوات العمل المحلية (نسخ/تسمية/اختبار) ثم أُريك أوامر بسيطة لتحسين الصور، وفي النهاية أقدّم خيارين لتضمين الصور في الكود (مسارات ثابتة أو data-img مع تحميل ديناميكي).

ماذا فعلتُ الآن
- عدّلتُ الملف HTML في المثال وأضفتُ عناصر <img> مع مسارات مقترحة داخل assets/images/ لكل صنف، إضافة شعار assets/images/logo.png.
- أضفتُ CSS صغير لعرض الصور بطريقة متناسقة وخصائص تحميل كسول (lazy) وتعامل مع خطأ العرض إن لم توجد الصورة.

الخطوات خطوة بخطوة (سهل الاتّباع)

1) أنشئ مجلداً للصور داخل المشروع
- مكان مقترح: assets/images/
- أمر (Linux/macOS):
```bash
mkdir -p assets/images
```
- أمر (Windows PowerShell):
```powershell
New-Item -ItemType Directory -Path .\assets\images -Force
```

2) جهّز صورك وسمّها بنفس الأسماء المقترحة أو غيّر المسارات في الملف
- أسماء مقترحة (كما في المثال):
  - logo.png (الشعار)
  - pepperoni.jpg
  - disney.jpg
  - four_seasons.jpg
  - margherita.jpg
  - mr_pizza.jpg
  - bbq.jpg
  - ranch.jpg
  - four_cheese.jpg
  - kumpir.jpg
  - chocoliza.jpg
  - caesar.jpg
  - veg_pasta.jpg
  - chicken_ranch_pasta.jpg
  - hotdog_pasta.jpg
- انسخ/حمّل الصور إلى assets/images/. مثال:
```bash
# افتراض أنك داخل مجلد المشروع
cp /مسار/صور/pepperoni.jpg assets/images/pepperoni.jpg
cp /مسار/صور/logo.png assets/images/logo.png
```

3) اختبر الملف محلياً في المتصفح
- افتح الملف menu-mrpizza_Version15.html في متصفح (سحب الملف إلى المتصفح أو استضافة محليّة).
- إن كانت بعض الصور لا تظهر، سيختفي عنصر الصورة بفضل onerror="this.style.display='none'" — ستعرف أين تنقص الصور.

4) إذا أردت اسماء مختلفة أو مجلدات أخرى — عدّل المسارات في HTML
- ابحث عن src="assets/images/..." وغيّر المسار إلى اسم الملف/المجلد الفعلي.

5) (اختياري) تحسين الصور لتسريع التحميل (مستحسن)
- تحويل إلى WebP أو تصغير الحجم باستخدام ImageMagick:
```bash
# تثبيت ImageMagick إن لم يكن مثبتاً
# macOS (Homebrew): brew install imagemagick
# Ubuntu: sudo apt-get install imagemagick

# مثال لتعديل حجم وصنع webp
magick convert assets/images/pepperoni.jpg -strip -resize 1200x800 -quality 80 assets/images/pepperoni.webp
```
- ثم غيّر في HTML src إلى .webp أو استخدم <picture> للبديل.

6) بديل برمجي: استخدام data-img والتحميل الديناميكي (فائدة: يمكنك إبقاء src فارغاً وتعيين الصورة عبر JS، مفيد لو تحمّل من API)
- مثال JS بسيط (أضف إلى أسفل ملف الـ HTML قبل إغلاق </body> أو في ملف JS خارجي):
```html
<script>
  document.querySelectorAll('.menu-card').forEach(card=>{
    const imgPath = card.dataset.img; // مثال: data-img="assets/images/pepperoni.jpg"
    if (imgPath){
      const img = card.querySelector('.menu-img');
      if (img) img.src = imgPath;
    }
  });
</script>
```
- ولتفعيل هذا الأسلوب، عدّل كل بطاقة:
```html
<div class="menu-card" data-prices='...' data-img="assets/images/pepperoni.jpg">
  <img class="menu-img" alt="..." loading="lazy" onerror="this.style.display='none'"/>
  ...
</div>
```

7) فحوصات نهائية
- تأكد من حجم الملف الكلي: صفحات الويب المحمولة تفضّل صور مضغوطة.
- افتح الصفحة على هاتف لتتأكد من الاستجابة (responsive).
- إذا تريد روابط CDN أو استضافة صور على إنترنت عام — أعطني الروابط وأعدّل المسارات لك.

خيارات أقدمها لك الآن (اختر أحدها)
A) أساعدك خطوة بخطوة أثناء رفع الصور — أخبرني أين تحفظ الصور (على جهازك أم في مستودع GitHub؟).
B) أُنشئ لك نسخة من الملف مع data-img تلقائياً (أحتاج أن تُعطيني أسماء الصور أو أن أستخدم أسماء افتراضية).
C) أقدم أوامر ImageMagick تلقائياً لكل صورة لتحويلها إلى webp وأحجام متعددة.

ماذا أفعل الآن لمساعدتك فوراً؟
- أرسل لي: 1) هل الصور على حاسوبك أم في GitHub؟ 2) أطلعني على أسماء الملفات التي تريد استخدامها (أو قل "أريد أن أسميها كما في الاقتراح"). 
سأرد عليك بالتعليمات الدقيقة التالية أو أعدّل الملف لك وأعرض لك المقطع المعدّل جاهزاً للنسخ.