---
layout: post-pr
title: Backstage، چیست؟ چرا؟ چگونه؟
tags: SoftwareEngineering 
image: https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage.jpg
lang: pr
---

هر چه قدر که نرم‌افزاری که در حال توسعه‌ی آن هستیم بزرگتر میشود، میکروسرویس‌های بیشتری ایجاد می‌شود، افراد بیشتری به صورت همزمان روی نرم‌افزار کار می‌کنند و انتقال دانش بین تیم‌ها سخت‌تر و پیچیده‌تر می‌شود.

بگذارید یک مثال از دنیای واقعی بزنم؛ در شرکتی که من در آن کار میکنم، هر کدام از سرویس‌ها API‌هایشان را در قالب ابزاری به نام swagger منتشر میکنند. Swagger ابزاریست که تحت وب بالا می‌آید و schemaی API‌ها را نشان میدهد و به شما این اجازه را میدهد که از همان جا آن‌ها را فراخوانی کنید. با گذر زمان، تعداد میکروسرویس‌ها در سازمان ما بیشتر شد و به تبع از آن تعداد پنل‌های Swagger برای هر کدام از این اپلیکیشن‌ها هم بیشتر شد و شما می‌بایست که آدرس Swagger همه این سرویس‌ها را حفظ میبودی یا از توسعه دهندگان آن میپرسیدی و مشکل اصلی زمانی بود که تو حتی نمیدانستی که توسعه دهنده‌ی سرویس مد نظر تو چه کسی یا چه تیمی‌ست. 

همانطور که در این مثال مشاهده میشود، حلقه‌ی مفقوده در این داستان، عدم وجود بستر مناسب برای انتقال دانش بین تیم‌هاست. 

بنابراین چه اتفاقی افتاد؟ یکی از برنامه نویسان خلاق در سازمان اقدام کرد به تولید یک پنل ساده‌ی htmlی که در آن آدرس Swagger همه سرویس‌ها وجود داشت. 

اجازه بدهید یک نیازمندی دیگر را مطرح کنم، فرض کنید که یکی از سرویس‌هایتان دچار اشکال شده است، میدانید که این سرویس با چند سرویس دیگر در ارتباط است و نیاز دارید که ببینید این سرویس‌ها که توسط دیگر تیم‌ها توسعه داده‌ میشوند به تازگی دچار تغییری شده است یا خیر. یا تصور کنید که دوست دارید که داکیومنت‌های مربوط به سرویس خودتان یا دیگر سرویس‌ها را در یک جا به طور مجتمع ببینید. 

همه این ها باعث میشود که در طول روز مجبور باشید در هزاران پنل لاگین کنید و هزاران اطلاعات مختلف را برای پیشبرد یک مسئله از ابزار‌های مختلف جمع‌آوری کنید. ضمنا همه این ها به شرطی هست که شما دسترسی لازم برای این موضوع را هم داشته باشید. 

فرض کنید که یک پنلی وجود داشت که همه این اطلاعات را در خود جا داده بود. زندگی چه قدر ساده‌تر میشد؟ بک‌استیج دقیقا برای همین موضوع به وجود آمده است. 



## بک استیج چیست؟
و اما بک‌استیج چیست؟ دقیقا بک استیج یک سلوشن برای مسئله‌ی ذکر شده‌ی بالاست. توسعه دهندگان اسپاتیفای هم مثل ما دچار مشکلات بالا بودند و به واسطه‌ی همین، نیازمند این موضوع بودند که به اصطلاح خودشان یک developer portal داشته باشند که بتواند به تسریع و تسهیل انتقال دانش کمک بکند. به همین علت Backstage را توسعه دادند و وقتی که دیدند از نظر تکنولوژی همچین چیز عجیب غریبی هم نیست، اما بسیار گره گشاست تصمیم گرفتند آن را اوپن سورس کنند و یک باری را از روی دوش برنامه نویسان دیگر شرکت‌ها نیز بردارند. 

بنابراین بک استیج یک ابزار مبتنی بر خوداظهاری است، (یعنی خود توسعه دهندگان کمک میکنند که این ابزار غنی از اطلاعات شود) که کمی هم اتومیشن به خرج داده است. 

اگر بخواهم دقیق‌تر بگویم شما در بک استیج به طریقی (که جلوتر اشاره‌ای به آن خواهم کرد) سرویس خود را مشخص میکنید، ای پی آی ها آن را تعریف میکنی، لینک‌های مرتبط با سرویس خود را به اشتراک میگذاری، دیپندنسی‌های سرویست را مشخص میکنی (و هزاران کار دیگر از این دست) و بک استیج مسئولیت نمایش، دسته‌بندی، به روز‌رسانی داده‌های تغییر کرده و... را به عهده میگیرد.

در تصویر زیر نمونه‌ای از لیست سرویس‌ها در بک‌استیج را مشاهده میکنید:   
<img src="https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage/components.png" style="vertical-align:middle;text-align: center;"  width="450" >  

برای هر کدام از سرویس‌ها میتوان اطلاعاتی نظیر وابستگی‌ها به سایر سرویس‌ها، لیست لینک‌ها مهم داکیومنت‌ها و مرج‌ریکوئست‌ها، زبان برنامه نویسی و هر آن چه بخواهیم را نمایش بدهیم  
در تصویر زیر نمونه‌ی اطلاعات یک سرویس را به حداقلی‌ترین شکل ممکن(!) میبینید   
<img src="https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage/component.webp" style="vertical-align:middle;text-align: center;"  width="450" >  

یکی از اصلی‌ترین ویژگی‌های بک‌استیج این است که شما میتوانید پلاگین‌های متنوعی را روی آن نصب کنید و اطلاعات مربوط به هر کدام از سرویس‌ها را در بک‌استیج غنی‌تر کنیم.
به عنوان مثال تصویر زیر نمونه‌ای از پلاگین گیت‌لب است که اطلاعات مربوط به یکی از سرویس‌ها را نمایش میدهد  
<img src="https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage/gitlab.webp" style="vertical-align:middle;text-align: center;"  width="450" >  

و اما اگر بخواهم آخر صحبت‌هام رو به اول صحبت‌هام وصل کنم، اگر یادتون بیاد در مورد اشتراک گذاری api ها در قالب swagger صحبت کرده بودم، در backstage برای هر سرویس میتوانید api تعریف کنید، تصویر زیر نمونه‌ای از api تعریف شده در یکی از سرویس‌هاست. 
<img src="https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage/api.webp" style="vertical-align:middle;text-align: center;"  width="450" >  


## چگونه بک استیج را ستاپ کنیم؟
برای نصب بک‌استیج، باید NodeJS، Yarn، Docker و Git را نصب داشته باشید. سپس دستور زیر را اجرا کنید:

```sh
npx @backstage/create-app@latest
```

بعد از آن دستورات زیر را اجرا کنید

```sh
cd your-backstage-directory
yarn dev
```

تبریک میگویم، حال کافیست که localhost:3000 را در بروزر خود باز کنید تا بک استیج برای اولین بار در سیستم شما بالا بیاید.‌

به طور کلی کارهایی که باید بکنید که بتوانید بک استیج خود را به بهترین شکل کانفیگ کنید را در زیر لیست خواهم کرد:

<b>
۱.	ستاپ کردن دیتابیس postgres برای بک استیجتان:
</b>

 این کار باعث میشود که تغییرات شما روی دیتابیس ذخیره شود، به صورت پیشفرض در بک‌استیج از sqlite استفاده میشود که همه ما میدانیم چه اشکالاتی دارد :)

برای انجام این کار میتوانید از [راهنما](https://backstage.io/docs/getting-started/configuration#install-and-configure-postgresql) استفاده کنید

<b>
۲.	اینتگریت کردن با گیتلب سازمانیتون (self hosted gitlab) :
</b>

 انجام این کار باعث میشود که بک استیج تعریف سرویس‌هایتان را بتواند از روی گیت سازمانی‌تان بخواند، بتواند آن را به صورت دوره‌ای به روز رسانی کند و اطلاعاتی نظیر مرج ریکوئست‌ها، کانتریبیوتر‌ها، ایشو‌ها، زبان برنامه نویسی و اطلاعاتی از این دست را از هر کدام از ریپازیتوری‌هایتان را در بک استیج هم داشته باشید.

برای انجام این کار هم یک پلاگین مناسب وجود دارد که با استفاده از [راهنما](https://github.com/immobiliare/backstage-plugin-gitlab) میتوانید به راحتی از آن استفاده کنید


<b>
۳.	استقرار و داکرایز کردن اپلیکیشن  
</b>

برای این کار چند روش وجود دارد، مثل جدا کردن بکند و فرانت‌اند، مثل استفاده از داکر فایل مولتی استیج و روش‌های دیگری از این دست، برای این موضوع هم هیچ جا بهتر از خود [داکیومنت رسمی بک‌استیج](https://backstage.io/docs/deployment/) نمیتونه به کمکتون بیاد.



### اضافه کردن یک سرویس به بک‌استیج:
برای افزودن سرویس به پشت‌صحنه، دو مرحله را طی کنید.

<b>
 مرحله ۱: اضافه کردن فایل YAML مربوط به سرویس در ریپازیتوری گیت  
</b>

برای افزودن سرویس جدید، فایلی با فرمت YAML در ریپازیتوری سرویس ایجاد کنید و مشخصات سرویس را پر کنید.

```yaml
apiVersion: backstage.io/v1alpha1
kind: Component
metadata:
  name: your-service-name # In this section, write the name of your service, for example, report-center and...
  description: some shit about your service # In this section, you can explain a little about what this service is for.
  links: # In this section, you can add links related to your service, such as Grafana, Hangfire, Confluence, etc.
    - url: https://some.link/ 
      title: some-link 
      icon: some-material-icon # For this part, you can use material UI icons, for example, dashboard, etc. To be able to use the right icon, you can use this link: https://fonts.google.com/icons
    - url: https://another.link/
      title: backstage-official-website
      icon: some-material-icon
spec:
  type: service 
  lifecycle: Production # you can use Production/Development
  owner: platform # write your team name. (Choose you team from this file: )
  providesApis: # Names of API resources provided by your service and defined below (you can have any number of APIs)
    - openapi-example 
    - proto-example
  consumesApis: # Names of API resources provided by another service and defined in the entities.yaml of that service(you can have any number of APIs)
    - another-service-api-proto 

--- 
apiVersion: backstage.io/v1alpha1
kind: API
metadata:
  name: openapi-example 
  description: your openapi api information
spec:
  type: openapi
  lifecycle: production
  owner: platform
  dependsOn: # The names of the components you have dependencies on (if that component exists in the backstage, the name you enter must be the same as its name in the backstage)
    - sql-serevr
    - envoy
    - report-center
  definition:
    $text: https://address.swagger.json/ # Add address of your swagger json for example https://foo.bar/swagger/v1/swagger.json
--- 
apiVersion: backstage.io/v1alpha1
kind: API
metadata:
  name: grpc-example
  description: your proto api information
spec:
  type: grpc
  lifecycle: production
  owner: platform
  definition:
    $text: https://gitlab.your.company/rout/to/your/proto-file.proto
```
<b>
مرحله ۲: فایل خود را در Backstage ثبت کنید:
</b>

۱. وارد Backstage شوید و گزینه "+ create" را بزنید.  
۲. بر روی "Register Existing Component" کلیک کنید.  
۳. آدرس فایل YAML خود را وارد کرده و دکمه "آنالیز" را بزنید.  
۴. پس از بررسی، اجزای اضافه شده را تایید کنید.


 امیدوارم که این بلاگ بتواند به آشنایی بیشتر شما با بک‌استیج کمک کند، در صورتی که بخواهید میتوانید  در مورد این پنل و کاربرد‌هایش بیشتر با هم صحبت کنیم.