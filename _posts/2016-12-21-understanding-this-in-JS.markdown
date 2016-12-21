---
layout: post
title:  "Understanding This keword in Javascript !"
date:   2016-12-20 18:08:34
categories: Tutorial
---

Javascript စတင္ေလ့လာပါက အမွားအမ်ားဆံုး ျဖစ္ေလ့ျဖစ္ထရိွသည့္ အရာတစ္ခုထဲတြင္ “This” keyword သည္ တစ္ခုအပါအ၀င္ျဖစ္ပါတယ္၊ ဘာေျကာင့္အမွား မ်ားရသလဲဆိုပါက အျခားေသာ programming language အမ်ားစုတြင္ this သည္ object ကို ရည္ညြန္းက်ေလ့ရိွျပီး javascript တြင္မူ တမူထူးျခားစြာ လုပ္ေဆာင္ေသာေျကာင့္ျဖစ္သည္

**Javascript တြင္ this သည္ function တစ္ခုမည္ကဲ့သို့ invoke လုပ္ျခင္းခံရလဲ ဆိုသည့္အခ်က္ေပါ မ်ားစြာမူတည္ပါတယ္၊** 

ဥပမာ ဆိုပါစို့ console ထဲတြင္ ေအာက္ပါအတိုင္း function တစ္ခုကို သတ္မွတ္လိုက္ျပီး this ကို return ျပန္လိုက္ျပီး ေနာက္တစ္ေျကာင္းတြင္ invoke လုပ္လုိက္သည္၊

    function foo() {
    return this;
    }
    foo() === window;  

ထြက္လာသည့္ result မွာ true ျဖစ္သည္၊
အဘယ္ေျကာင့္ဆိုေသာ္ foo ဆိုသည့္ function သည္ default binding ျဖစ္သည့္ window object ေပါတြင္ ေခါယူထားေသာေျကာင့္ျဖစ္သည္၊ ေ
အာက္ပါ syntax တြင္ ေတြ့ရိွနိုင္သည္၊

window.foo()===window
window.foo()===foo();

ပိုမိုရွင္းလင္းေစရန္ variable သံုးျပီးျပေပးသြားပါမည္.

    var a = ‘global’
    function bar() {
        var a = 'inner'
        return this.a;
    }
    bar();

အထက္ပါ bar function ကို run ပါက ‘global’ ကို output ေတြ့ရမည္ျဖစ္သည္၊ အဘယ္ေျကာင့္ဆိုေသာ္ “this” သည္ bar function နွင့္မသက္ဆိုင္ဘဲ function မည္သည့္ context ေပါတြင္ invoke လုပ္ခံရလဲဆိုသ့ည့္ အေပါတြင္သာ မူတည္ျခင္းေျကာင့္ျဖစ္သည္၊
ထို့ေျကာင့္ အနွစ္ ဆိုရေသာ္ javascript တြင္ this ၏ မူလ default binding သည္ window object ျဖစ္သည္၊
ဒါဆိုရင္ မူလ default binding ကို မသံုးခ်င္ဘူး တျခားေသာ context ကို bind မလဲ ? ေအာက္မွာ နမူနာနွင့္တကြေရးျပသြားမွာပါ.

    var name = ‘Mg Mg’;
    var user = { name : ‘john doe’ };
    function sayName(){
          return this.name;
    }

sayName() ကို run ပါ ဘာထြက္သြားမွာပါလဲ ?  ဟုတ္ပါတယ္ function ၏ default binding သည္ window ျဖစ္သည့္အတြက္ ‘Mg Mg’ ကိုရွာပါ၊
ဒါဆိုရင္ sayName() ဆိုတဲ့ function ကိုလဲ မျပင္ခ်င္ဘူး၊ 
this ကို ေတ့ာ window object မဟုတ္ဘဲ တျခားေသာ object သံုးခ်င္တယ္၊ ဘယ္လို လုပ္ရမလဲ၊ လြယ္ပါတယ္၊

    sayName.call(user) === ‘john doe’; 

call ဆိုသည့္ method ကိုသံုးျပီး user ဆိုသည့္  object ကို pass ေပးလုိက္ျခင္းျဖင့္ sayName() ဆိုသည့္ function ထဲရိွ this ၏ context ကို ေျပာင္းေပးလိုက္ျခင္းျဖင့္ရရိွနိုင္ပါသည္၊ အလြယ္ေျပာရရင္ 
Hay .... 
“SayName ဆိုတဲ့ function မင္းထဲမွာရိွတဲ့ thisကို အခုငါေပးလိုက္တဲ့ context ကိုသံုးျပီး run ပါ“ ေပါ့
Another example

    var users = [‘nyan win’ ,'pyae sone nyein'];
    function sayName(){
            return this[1];
    }

    sayName.call(users) === users[1]; ---> true

က်န္ေနေသးသည့္ constructor function အတြင္းရိွ ‘this’, this ကို ေတြ့ရအမ်ားဆံုး object literal အတြင္းရိွ  method ၏  ‘this’ , event handler အတြင္းရိွ this keyword မ်ားကို ေနာက္ေန့မ်ားတြင္ ဆက္ေရးေပးသြားမွာပါ၊

**NOTE : strict mode တြင္မူ အထက္ပါအခ်က္အလက္မ််ားသည္ ကြဲျပားမွုရိွသည္၊**

