---
layout: post-pr
title: Backstage، چیست؟ چرا؟ چگونه؟
tags: مهندسی‌نرم‌افزار
image: https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage.jpg
lang: pr
---
به عنوان بخشی از فرآیند ایجاد نرم افزار، که در آن تیم‌ها و افراد با نقش‌های مختلف درگیر هستند، به اشتراک گذاری اطلاعات و دانش به طور فزاینده‌ای پیچیده و حتی غیرقابل مدیریت می‌شود. مثلاً خیلی وقت‌ها پیش می‌آید که شما می‌بینید که یکی از سرویس‌هایتان دچار اشکال شده است و نیاز دارید که ببینید سرویس‌های دیگر که توسط دیگر تیم‌ها توسعه داده‌ می‌شوند به تازگی دچار تغییری شده است یا خیر. 

## بک استیج چیست؟
Backstage یک پلتفرم اوپن‌سورس برای ساخت پورتال توسعه‌دهندگان است که توسط توسعه‌دهندگان شرکت اسپاتیفای به عنوان پنل جادویی‌ای توسعه داده شده است. Backstage تمام ابزارها، خدمات و اسناد زیرساخت شما را برای ایجاد یک محیط توسعه کارآمد به صورت اند تو اند یکپارچه می‌کند.

## چگونه بک استیج کار می‌کند؟
بک‌استیج به این شکل کار می‌کند که همه سرویس‌ها در ریپازیتوری خودشان با فرمت مشخصی مشخصات سرویس‌هایشان را مینویسند (یک YAML فایل) و بعد از این که این فایل را در Backstage ثبت می‌کنید، جادو شروع می‌شود. دیپندنسی‌ها، APIها، لینک‌های مرتبط، پایپلاین‌ها، کانتریبیوتر‌ها و... همگی در پنل بک‌استیج نمایش داده می‌شوند.

## چگونه بک استیج را در سازمان خود ستاپ کنیم؟
برای نصب بک‌استیج، باید NodeJS، Yarn، Docker و Git را نصب داشته باشید. سپس دستورات زیر را اجرا کنید:

```
npx @backstage/create-app@latest
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


