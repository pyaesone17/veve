---
layout: post
title:  "Laravel Migration Part I!"
date:   2016-08-06 18:08:34
categories: Tutorial
---
In this tutorial I will talk about Database Migration, How it is realated to version Control and Many More.



## 1.INTRODUCTION  ##

Laravel ကို စေလ့လာတာနဲ့ ပံုမွန္အားျဖင့္ က်ေနာ္တို့က Request, Response, Controller, Route ျပီးရင္ Eloquent ကို အေလးေပးျပီးျကည့္က်တာ မ်ားပါတယ္၊ ပံုမွန္အားျဖင့္လည္း အဲ့အပုိင္းေတြက Application တည္ေဆာက္ရာမွာ အဓိက က်တဲ့ အပုိင္းေတြျဖစ္တာေျကာင့္လည္းပါ ပါတယ္၊ 

ဒီ Migration ကို က်ေနာ္ေရးဖို့လဲ စိတ္ကူးမရိွခဲ့ပါဘူး၊ သုိ့ေသာ္ အခုေနာက္ပိုင္း က်ေနာ္ေတြ့ဆံု ခဲ့ရတဲ့ Developer အခ်ို့က  **PHP My Admin နဲ့ဆို UI ပါရတယ္၊ ျပင္လိုက္ရင္လြယ္တာေပါ့. Migration ကို ဘာလို့သံုးတာလဲ**၊ လို့ေမးလာတဲ့အတြက္ က်ေနာ္သိသေလာက္ ေရးျပီးေ၀မွ်လိုက္ပါတယ္ ၊ 

က်ေနာ့္ အျမင္အရေတာ့့PHP My Admin သည္ အလြန္ေကာင္းမြန္တဲ့ Software ပါ ၊ သို့ေသာ္ က်ေနာ္တို့က “**Chose the right tool for the right place**” ဆိုတဲ့ စကားနဲ့ အညီ ဆံုးျဖတ္ရမွာျဖစ္ပါတယ္၊ ဘာအေျကာင္းေျကာင့္ Migration သံုးရတာလဲ ဘယ္ေနရာမွာ Migration ကို သံုးသင့္သလဲ၊ Migration သံုးရျခင္းေျကာင္းျဖစ္ေပါလာမဲ့ ေကာင္းက်ိုးဆိုးက်ိုးေတြကို ရွင္းျပသြားမွာပါ၊

## 2.PROBLEM  ##

က်ေနာ္တို့ Team နဲ့အလုပ္လုပ္ ရျပီဆိုရင္ အသင္းရဲ့ member ၀င္တစ္ေယာက္ေယာက္ရဲ့ ေျပာင္းလဲလိုက္သည့္ Database Schema ကို အျမဲ မျပတ္ သိဖို့လိုအပ္လာပါတယ္၊ ဒါမွသာ Develop လုပ္ေနတဲ့ App က Error ကင္းကင္းနဲ့ အလုပ္လုပ္နိုင္မွာပါ၊

က်ေနာ္တို့ ေတာ္ေတာ္မ်ားမ်ားျကံုဖူးမွာပါ၊    “ဟာ အခုေလးတင္ Code က အလုပ္လုပ္ေနေသးတယ္၊ Git Pull လုပ္ျပီးမွ Code ေတြ အလုပ္မလုပ္ေတာ့ဘူး . Error Log မွာေတာ့ Database Column မရိွလို့ျဖစ္တယ္ျပေနတယ္ , ဘယ္သူ Database Update လုပ္ေသးလဲ“   ဒီစကားေလးက Developer ေတာ္ေတာ္မ်ားမ်ား ျငီးသြားဖူးမွာပါ ၊

ျငီးတြားျပီးရင္ေတာ့ PHP My Admin ကိုဖြင့္ ၊ Column ေတြကို manual နဲ့ create လုပ္ရအံုးမွာ၊ Geek ဆိုရင္ေတာ့ terminal ထဲသြားျပီး Alter table blah blah ေတြရိုက္ရမွာေပ့ါ၊ Database  changes သိပ္မရိွဘဲ   develop လုပ္ရတဲ့ APP မ်ိုး၊ ဒါမွမဟုတ္ Table Structure အားလံုးကို တစ္ခါတည္း Analysis ေလ့ရိွတဲ့ SSADM methodology မ်ိုးဆိုရင္ေတာ့ ပံုမွန္ Traditional နည္းလမ္း နဲ့ အဆင္ေျပေနမွာပါ၊

## 3.AGILE AND MIGRATION ##

Aglie လို methodology က Iterative Devlopment ျဖစ္တဲ့ အတြက္ Code ေတြ Database ေတြဟာ အခ်ိန္နဲ့ အမွ်အျမဲတမ္းေျပာင္းလဲေနမွာပါ၊ ေျပာင္းလဲေနတဲ့ Code ေတြနဲ့ အညီေျပာင္းလဲသြားတဲ့ Database structure ကို version control လုပ္ျပီး မွတ္သားထားဖုိ့လိုပါတယ္၊ 

Code ေတြအတြက္ Version Control ကို Git Hub မွအလြယ္တကူ မွတ္သားနိုင္ေပမယ့္ ၊ ေျပာင္းလဲသြားတဲ့ Database Structure ကို sql File ျဖစ္ Export လုပ္ျပီး Git နဲ့ တင္ဖို့က်ေတ့ာ အဆင္မေျပပါဘူး၊
 
ဒီေနရာမွာ Database Structure ကို Version Control လုပ္ေပးနိုင္တဲ့ Migration Tool ေတြကို အသံုးျပုဖို့လိုအပ္လာခဲ့ပါတယ္၊ Agile ေခတ္စားလာတာနဲ့ အညီ Migration Tool ေတြဟာ အခုေနာက္ပိုင္း Modern Framework ေတြမွာ Out of The Box Feature အျဖစ္ပါ၀င္လာခဲ့ပါတယ္၊ 

Laravel , Rails အစရိွတဲ့ နာမည္ေက်ာ္ Framework ေတြမွာ built in ပါ၀င္သလို Express Js အတြက္ဆိုရင္လည္း knex လို Third party Library သံုးျပီး စီမံနိုင္မွာပါ၊အခု လာမယ့္ tutorial ေတြမွာေတာ့ က်ေနာ္က Laravel Migration အေျကာင္းကို ရွင္းျပသြားမွာျဖစ္ပါတယ္. 

**Migrations are like version control for your database, allowing a team to easily modify and share the application's database schema. Migrations are typically paired with Laravel's schema builder to easily build your application's database schema.**  

*From Laravel Documentation*   

THANK YOU FOR READING !    See you Again :)
