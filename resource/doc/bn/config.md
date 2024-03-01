# কনফিগারেশন ফাইল

## অবস্থান
webman এর কনফিগারেশন ফাইলগুলি `config/` ডিরেক্টরিতে থাকে, প্রজেক্টের মধ্যে `config()` ফাংশনের মাধ্যমে সম্প্রতি কনফিগারেশন পেতে পারেন।

## কনফিগারেশন পান

সমস্ত কনফিগারেশন পেতে
```php
config();
```

`config/app.php` তে সমস্ত কনফিগারেশন পেতে
```php
config('app');
```

`config/app.php` তে `debug` কনফিগারেশন পেতে
```php
config('app.debug');
```

যদি কনফিগারেশন অ্যারে হয়, তবে `.` ব্যবহার করে অ্যারেতে ভিতরের উপাদানগুলির মান পেতে পারেন, উদাহরণস্বরূপ
```php
config('file.key1.key2');
```

## ডিফল্ট মান
```php
config($key, $default);
```
দ্বিতীয় প্যারামিটার ব্যবহার করে config দ্বারা ডিফল্ট মান পাঠাবেন, যদি কনফিগারেশন অস্তিত্ব না থাকে তাহলে ডিফল্ট মানটি প্রদান করবে।
কনফিগারেশনটি অস্তিত্ব না থাকা এবং কোনও ডিফল্ট মান সেট না থাকা এর কারণে `null` ফিরিয়ে দেবে।

## কাস্টমাইজড কনফিগারেশন
ডেভেলপাররা `config/` ডিরেক্টরিতে নিজেদের কনফিগারেশন ফাইল যুক্ত করতে পারেন, উদাহরণস্বরূপ

**config/payment.php**

```php
<?php
return [
    'key' => '...',
    'secret' => '...'
];
```

**কনফিগারেশন পেতে ব্যবহার করা**
```php
config('payment');
config('payment.key');
config('payment.key');
```

## কনফিগারেশন পরিবর্তন
webman ডাইনামিক কনফিগারেশন সাপোর্ট করে না, সমস্ত কনফিগারেশন ফাইল ম্যানুয়ালি পরিবর্তন করতে হবে এবং পুনরারম্ভ বা পুনঃআরম্ভ পদক্ষেপ নিতে হবে

> **মন্তব্য**
> সার্ভার কনফিগারেশন `config/server.php` এবং প্রসেস কনফিগারেশন `config/process.php` পুনরারম্ভ সাপোর্ট করে না, এগুলি পুনঃআরম্ভ করতেই হবে।