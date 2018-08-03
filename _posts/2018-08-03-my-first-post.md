---
layout: blog_post
title: My Simple Validation Code in PHP
date: 2018-08-03
---

## Intro
My college assignment is create a program in PHP + MySQL. And should using form input validation. Moreover, the lecturer want the program builds by using pure PHP without framework.

This program about vehicle rental. You can checkout the source code at: https://github.com/ganjarhadiatna/rentalmobil

This assignment task is not individual but group. My partner is Ganjar Hadiatna. We create the program by separate the frontend and backend part. Two part communicate by json (simple API). So Backend PHP should return json.

I create `lib-yudi.php` that contains the validation functions (checkout the [full code here](https://github.com/ganjarhadiatna/rentalmobil/blob/master/api/lib-yudi.php))

## Main content

I will discuss one validation function. For others, just checkout the full source code.

By the way, this is my function that will useful for making the code readable.

```php
function markAsValid()      { return true;  }
function markAsInvalid()    { return false; }
```

This is the validation function:

```php
/**
 * return true if valid
 */
function validate_number_only($input) {
    if (preg_match('/[^0-9]+/', $input)) {
        return markAsInvalid();
    }
    return markAsValid();
}
```

Below the code that using that validation function (checkout [the code here](https://github.com/ganjarhadiatna/rentalmobil/blob/master/api/post/mobil.php)).

```php
if (! validate_alphanumeric_only($plat_nomor))                  validasiGagal('This field only accepts alphabet chars, numbers, space and dot.');
if (! validate_number_only($no_rangka))                         validasiGagal('This field only accepts numbers.');
if (! validate_name_only($jenis))                               validasiGagal('This field only accepts alphabet chars, space and dot.');
if (! validate_enum($warna, ['merah', 'biru', 'hitam', 'abu'])) validasiGagal('Only accepts "merah", "biru", "hitam", "abu". (case is important)');
if (! validate_format($tahun, 'dddd'))                          validasiGagal('Year should be in format YYYY');

kirimPesanJikaValidasiGagal();
```

My code is mixing the english and Bahasa Indonesia words (sorry). So this is translated code for make you easily understand the code:

1. `validasiGagal()` translated to english is `validationFail()`
2. `kirimPesanJikaValidasiGagal()` is `sendMessageIfValidationFail()`


