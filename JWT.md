# JWT

## توضیحات کلی :

* مخفف JSON Web Token
* یک استراتژی اعتبارسنجی است که در اپلیکیشن های کلاینت سرور استفاده میشود  که در ان کلاینت یک وب اپلیکیشن با جاوا اسکریپت و بعضی فریم ورک ها مثل angular یا React است .
* username+password را دریافت میکند و دواجازه می دهد :
  * access token : برای حدود 5 دقیقه معتبر است 
  * refresh token : برای حدود 1 روز معتبر است 
* این token ها سه بخش دارند مانند : xxx.yyy.zzz  که header.payload.signature است :
  * signature : header base64 + payload base64 +`secret_key
  * اگر اطلاعات header یا payload تغییر کند signature بی ارزش میشود و تنها راه برای فهمیدن بی ارزش شدن ان استفاده از secret_key میباشد

## نصب :

1. ```pip install djangorestframework_simplejwt```
2. ```'rest_framework_simplejwt.authentication.JWTAuthentication',``` در REST_FRAMEWORK در **settings.py**
3. اضافه کردن دو url :
   * ```path('api/token/', jwt_views**.**TokenObtainPairView**.**as_view(), name**=**'token_obtain_pair')```
   * ```path('api/token/refresh/', jwt_views**.**TokenRefreshView**.**as_view(), name**=**'token_refresh')```

### افزایش زمان access و refresh

```en-us
SIMPLE_JWT = {
	'ACCESS_TOKEN_LIFETIME': timedelta(days=5),
	'REFRESH_TOKEN_LIFETIME': timedelta(days=30),
}
```



### سطح دسترسی : 

با استفاده از عبارت ```permission_classes = (IsAuthenticated,)``` میتوان دسترسی را فقط به کسانی که token دارند محدود کرد .

برای محدود سازی بیشتر میتوان فایلی به نام permitions ساخت و داخل ان از کلاس هایی که از BasePermision ارث بری میکنند استفاده کرد و یک سری محدودیت قرار داد . 

