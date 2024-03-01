# التحميل التلقائي

## استخدام تحميل الملفات وفقًا لمواصفات PSR-0 الخاصة بـ composer
يتبع webman مواصفات تحميل الـ PSR-4 الأوتوماتيكي. إذا كنت بحاجة إلى تحميل مكتبة تعمل وفقًا لمواصفات PSR-0 ، فيرجى الرجوع إلى الخطوات التالية.

- إنشاء دليلًا جديدًا بإسم `extend` لتخزين مكتبة الكود الخاصة بـ PSR-0.
- تعديل `composer.json` وإضافة المحتوى التالي في `autoload`.

```js
"psr-0" : {
    "": "extend/"
}
```
النتيجة النهائية تكون مشابهة للصورة التالية
![](../../assets/img/psr0.png)

- تنفيذ الأمر `composer dumpautoload`
- تشغيل الأمر `php start.php restart` لإعادة تشغيل webman (يرجى ملاحظة أنه يجب إعادة التشغيل لجعل التغييرات سارية المفعول)

## تحميل ملفات معينة باستخدام composer

- تعديل `composer.json` وإضافة الملفات التي ترغب في تحميلها في `autoload.files`.
```
"files": [
    "./support/helpers.php",
    "./app/helpers.php"
]
```

- تنفيذ الأمر `composer dumpautoload`
- تشغيل الأمر `php start.php restart` لإعادة تشغيل webman (يرجى ملاحظة أنه يجب إعادة التشغيل لجعل التغييرات سارية المفعول)

> **ملحوظة**
> الملفات المحددة في تكوين `autoload.files` داخل ملف composer.json سيتم تحميلها قبل تشغيل webman. ومن ناحية أخرى، فإن الملفات التي تم تحميلها باستخدام `config/autoload.php` في الإطار سيتم تحميلها بعد تشغيل webman.
> يجب إعادة تشغيل webman بعد تعديل الملفات المحددة في تكوين `autoload.files` بملف composer.json لجعل التغييرات سارية المفعول، ولا تجدي تأثيرًا إذا تم إعادة التحميل. بينما يدعم تكوين `config/autoload.php` التحميل الساخن، حيث يكفي إعادة التحميل لجعل التغييرات سارية المفعول.

## تحميل ملفات معينة باستخدام الإطار

قد توجد ملفات لا تتوافق مع مواصفات SPR ولا يمكن تحميلها تلقائيًا، وفي هذه الحالة يمكننا استخدام تكوين `config/autoload.php` لتحميل هذه الملفات على سبيل المثال:

```php
return [
    'files' => [
        base_path() . '/app/functions.php',
        base_path() . '/support/Request.php', 
        base_path() . '/support/Response.php',
    ]
];
```
 > **ملحوظة**
 > من الملاحظ أن تكوين `autoload.php` يحتوي على تحميل ملفات `support/Request.php` و `support/Response.php`، وهذا يرجع إلى أن هناك ملفين مماثلين تحت مجلد `vendor/workerman/webman-framework/src/support/`، حيث يتم التفضيل لتحميل الملفات الخاصة بالمشروع الموجودة في الدليل الأساسي للمشروع `support/Request.php` و `support/Response.php`. هذا يسمح لنا بتخصيص محتوى هاتين الملفتين دون الحاجة لتعديل الملفات الموجودة في مجلد `vendor`. إذا كنت لا ترغب في تخصيص هاتين الملفتين، يمكنك تجاهل هذين التكوينين.