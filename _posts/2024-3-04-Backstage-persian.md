---
layout: post-pr
title: Backstage، چیست؟ چرا؟ چگونه؟
tags: مهندسی‌نرم‌افزار
image: https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage.jpg
lang: pr
---
به عنوان بخشی از فرآیند ایجاد نرم افزار، که در آن تیم ها، افراد با نقش‌های مختلف نقش ها و فرآیندهای متعددی در یک سازمان درگیر هستند، به اشتراک گذاری اطلاعات و دانش به طور فزاینده‌ای پیچیده و حتی غیرقابل مدیریت می‌شود. مثلا خیلی وقت‌ها پیش می‌آید که شما می‌بینید که یکی از سرویس‌هایتان دچار اشکال شده است، میدانید که این سرویس با چند سرویس دیگر در ارتباط است و نیاز دارید که ببینید سرویس‌های دیگر که توسط دیگر تیم‌ها توسعه داده‌ میشوند به تازگی دچار تغییری شده است یا خیر. یا به عنوان مثالی دیگر دوست دارید که داکیومنت‌های مربوط به سرویس خودتان یا دیگر سرویس‌ها را در یک جا به طور مجتمع ببینید. یا فرض کنید که بخواهید مثلا swagger یک سرویس را ببینید و هزاران چیز مشابه این که در طول روز برای ما پدید می‌آید. شما برای این که بتوانید چنین مسائلی را حل کنید خیلی وقت‌ها نیاز به چندین پنل متفاوت دارید، تازه اگر دسترسی لازم برای دیدن این اطلاعات را داشته باشید (به خصوص اگر در سازمانتان از mono repo استفاده نکرده باشید) نیاز به داشتن یک پنل جامع که همه این اطلاعات را داشته باشد، از زمانی که نرم افزار‌های اینترپرایز به شکل امروزی خودشان درآمده است، وجود داشته است؛ و همواره این ایده یک چیز فانتزی، اما جذاب بوده است. 


## بک استیج چیست؟
Backstage یک پلتفرم اوپن سورس برای ساخت پورتال توسعه دهندگان است که توسط توسعه دهندگان شرکت اسپاتیفای به عنوان پنل جادویی‌ای که بالاتر ذکر کردیم توسعه داده شده است. Backstage تمام ابزارها، خدمات و اسناد زیرساخت شما را برای ایجاد یک محیط توسعه کارآمد به صورت اند تو اند یکپارچه می‌کند. شیوه‌ی کار کردن این پنل چگونه‌است؟ بک‌استیج به این شکل کار میکند که همه سرویس‌ها در ریپازیتوری خودشان با فرمت مشخصی مشخصات سرویسشان را مینویسند (یک yaml فایل) و بعد از این که این فایل را در Backstage رجیستر میکنید، جادو شروع میشود. دیپندنسی‌ها، APIها، لینک‌های مرتبط، پایپلاین‌ها، کانتریبیوتر‌ها و... همگی در پنل بک استیج نمایش داده. و برای به روز رسانی آن کافیست که فایل yaml خود را در ریپازیتوری خود به روز نگه دارید و خود پنل بک‌استیج آن را به صورت پریودیک بررسی میکند و پنل را به روز نگه میدارد. به طور کلی بک استیج فرآیند‌های آنبوردینگ، تعداد سوالات و حواس‌پرتی‌هایی که توسط اعضا دیگر تیم‌ها به وجود می‌آید و چیزهایی از این دست را بهبود بدهد، برای این که ببینید بک‌استیج تاثیر مثبتی روی سازمانتان گذاشته است یا خیر کافیست که ببینید در این زمینه‌ها چه قدر اوضاعتان بهتر شده است. 


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