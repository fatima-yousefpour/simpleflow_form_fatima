## این پروژه یک صفحه ثبت‌نام است که با استفاده از HTML، CSS و JavaScript ساخته شده و شامل موارد زیر است:
پنل سمت چپ با تصویر و افکت گرادیانت.

فرم ثبت‌نام سمت راست با اعتبارسنجی زمان واقعی و نشانگر قدرت رمز عبور.

پیام‌های خطا و پیام موفقیت.

طراحی برای رزولوشن دسکتاپ 1440x1024 بهینه شده و از فونت Figtree برای ظاهر حرفه‌ای استفاده می‌کند.

مشاهده پروژه :(https://simpleflowformfatimayousefpour.netlify.app/)

___________________________________________________________________________________________________________________________________________________________________
## ویژگی‌ها :
اعتبارسنجی زمان واقعی برای نام کاربری، نام کامل، ایمیل و رمز عبور.

نشانگر قدرت رمز عبور دینامیک: ضعیف → متوسط → قوی.

بازخورد بصری ورودی‌ها: نشانگرهای معتبر/نامعتبر برای ورودی‌ها.

پیام موفقیت: پس از ایجاد حساب کاربری نمایش داده می‌شود.

 تب‌ها: جایگاه Sign-Up / Sign-In برای توسعه‌های آینده.
___________________________________________________________________________________________________________________________________________________________________
 ## اعتبارسنجی رمز عبور
 ```javascript
function validatePassword() {
  const value = password.value;
  const lengthValid = value.length >= 8;
  const symbolValid = /[0-9!@#$%^&*]/.test(value);
  
  const usernamePart = username.value.trim();
  const emailPart = email.value.split('@')[0];
  const fullnamePart = fullname.value.trim().split(' ')[0];
  const forbidden = [usernamePart, emailPart, fullnamePart].filter(Boolean);
  const containsForbidden = forbidden.some(word => value.toLowerCase().includes(word.toLowerCase()));

  const nameValid = !containsForbidden && value.length > 0;
  const strengthValid = nameValid && lengthValid && symbolValid && value.length > 0;
  
  ruleStrength.textContent = `Password Strength: ${strengthValid ? 'Strong' : 'Weak'}`;
}
```


توضیح:
اعتبارسنجی رمز عبور بر اساس طول، وجود عدد یا نماد و عدم وجود کلمات محدود شده (نام کاربری، پیشوند ایمیل یا نام) انجام می‌شود.

نشانگر قدرت رمز عبور به‌صورت دینامیک بروزرسانی می‌شود.
___________________________________________________________________________________________________________________________________________________________________
## اعتبارسنجی فرم و فعال‌سازی دکمه ثبت
```javascript
function validateAll() {
  validateUsername();
  validateEmail();
  validateFullname();
  validatePassword();

  const allConditionsMet =
    validationStatus.username &&
    validationStatus.fullname &&
    validationStatus.email &&
    validationStatus.passwordName &&
    validationStatus.passwordLength &&
    validationStatus.passwordSymbol &&
    validationStatus.passwordStrength;
  
  if (allConditionsMet) {
    submitBtn.classList.add("active");
    submitBtn.disabled = false;
  } else {
    submitBtn.classList.remove("active");
    submitBtn.disabled = true;
  }
}
```
توضیح:
بررسی می‌کند که تمام فیلدها معتبر باشند و دکمه Create Account را فعال یا غیرفعال می‌کند.
___________________________________________________________________________________________________________________________________________________________________
## نمایش پیام خطا
```javascript
function validateUsername() {
  const value = username.value.trim();
  const isValid = value.length >= 3 && value.length <= 15;
  validationStatus.username = isValid;
  
  username.classList.remove("error", "valid");
  if (!isValid) { 
    username.classList.add("error"); 
    usernameError.classList.add("show"); 
  } else { 
    username.classList.add("valid"); 
    usernameError.classList.remove("show"); 
  }
}
```

توضیح:
نمایش یا مخفی کردن پیام‌های خطا به‌صورت دینامیک و نمایش وضعیت معتبر یا نامعتبر فیلد ورودی.
___________________________________________________________________________________________________________________________________________________________________
## پیام موفقیت و بازنشانی فرم
```javascript
submitBtn.addEventListener("click", () => {
  if(validateAll()){
    successMessage.classList.add("show");
    [username, fullname, email, password].forEach(input => input.value = "");
    validationStatus = { username: false, fullname: false, email: false, passwordName: false, passwordLength: false, passwordSymbol: false, passwordStrength: false };
    submitBtn.classList.remove("active");
    submitBtn.disabled = true;
  }
});
```

توضیح:
نمایش پیام موفقیت و بازنشانی تمام فیلدها و وضعیت اعتبارسنجی پس از ایجاد حساب.
___________________________________________________________________________________________________________________________________________________________________ ## نکات طراحی رابط کاربری
.left – پنل سمت چپ با تصویر و گرادیانت

.right – فرم ثبت‌نام سمت راست

.tabs –  تب‌ ها

.password-rules – لیست قوانین رمز عبور با بازخورد رنگی دینامیک
__________________________________________________________________________________________________________________________________________________________________
## تکنولوژی‌ها

HTML5

CSS3 (Flexbox، گرادیانت، pseudo-element)

JavaScript (Vanilla JS)

Google Fonts – Figtree
___________________________________________________________________________________________________________________________________________________________________
## نحوه استفاده

فایل index.html را در مرورگر باز کنید.

تمامی فیلدهای فرم را پر کنید.

بازخورد اعتبارسنجی و نشانگر قدرت رمز عبور را مشاهده کنید.

دکمه Create Account را فشار دهید تا پیام موفقیت نمایش داده شود.
___________________________________________________________________________________________________________________________________________________________________
## قوانین اعتبارسنجی

نام کاربری: بین ۳ تا ۱۵ کاراکتر

نام کامل: حداقل ۲ کاراکتر و شامل فاصله

ایمیل: فرمت معتبر ایمیل


رمز عبور:
حداقل ۸ کاراکتر

شامل عدد یا نماد

نباید شامل نام کاربری، پیشوند ایمیل یا نام باشد

قدرت رمز عبور: ضعیف → متوسط → قوی
___________________________________________________________________________________________________________________________________________________________________
## ساختار فایل‌
/SimpleFlow-SignUp
│
├── index.html       # فایل اصلی HTML شامل کدهای JS و CSS
├── README.md        # مستندات پروژه
└── assets/
     └── images/     # اختیاری برای تصاویر پس‌زمینه یا لوگو
     
     
     
     
     
     
     
     
     
 
