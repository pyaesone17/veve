---
layout: post
title:  "Exploring Facade Pattern In Laravel!"
date:   2016-08-25 18:08:34
categories: Tutorial
---
<p>( For Advance Developer Only ) </p>

<p>က်ေနာ္တို့ Laravel နာမည္ေက်ာ္လာရျခင္း အေျကာင္းအရာတစ္ခုက သူ့ရဲ့ elegant ျဖစ္တဲ့ syntax လြယ္ကူတဲ့ေရးပံုေရးနည္း ေတြေျကာင့္ဆိုရင္လဲ မမွားပါဘူး၊  <br>
တကယ္ေတာ့ က်ေနာ္တို့ လြယ္လြယ္ကူကူ ေရးသားေနရျခင္္းရဲ့ ေနာက္ကြယ္မွာ Laravel Contributor ေတြရဲ့ effort ေတြအမ်ားျကီးပါတယ္ဆိုတာကိုေတာ့ ျငင္းလို့မရပါဘူး၊</p>

<p>အဲ့ဒီထဲကမွ Laravel က က်ေနာ္တို့ developer ေတြ လိုအပ္တဲ့Service ေတြလြယ္ကူစြာေခါသံုးနိုင္ေအာင္ လုပ္ထားေပးတဲ့ Facade အေျကာင္းရွင္းျပေပးသြားမွာပါ၊ </p>

<p>Facade သံုးတဲ့ အတြက္ေျကာင့္ က်ေနာ္တို့ object ေတြကို instantiated လုပ္ဖို့တာ၀န္တစ္ခု မလိုအပ္ေတာ့ဘဲ အလြယ္တကူ ေခါသံုးနုိင္တဲ့ အျကိုးေက်းဇူးရပါတယ္၊ <br>
က်ေနာ္တို့ေန့စဥ္သံုးေနက် ထဲမွာ Facade ဆိုတဲ့အရာပါပါတယ္ ၊ သတိမထားမိတာလဲျဖစ္မွာပါ၊ ဒါေတြကေတာ့ နမူနာ ေန့စဥ္သံုးေနက် Facade ေတြပါဘဲ၊ </p>

<ol>
<li>Request::all();</li>
<li>View::make();</li>
<li>Mail::send();</li>
<li>Route::get();</li>
</ol>

<p>သံုးလို့ရတဲ့ Facade စာရင္းမ်ား ကိုေတာ့ ေအာက္ပါ လင့္ခ္မွာ ေလ့လာနိုင္ပါတယ္၊</p>

<p><a href="https://laravel.com/docs/5.3/facade">https://laravel.com/docs/5.3/facade</a>…</p>



<h2 id="facade-explanation">FACADE Explanation</h2>

<p>Facade အေျကာင္းမရွင္းျပခင္ PHP မွာ scope resolution သံုးပံုသံုးနည္း ကို နမူနာေရးျပသြားမွာပါ၊</p>

<pre><code>&lt;?php 
class Bicycle  {     
    public static function wheels() {         
        return 2;     
    } 
}
?&gt;
</code></pre>

<p>Bicycle ဆိုတဲ့ class ထဲက static wheels method ကို scope resolution သံုးျပီးေခါသြားျခင္းျဖစ္ပါတယ္၊ အေသးစိတ္ကုိေတာ့ မိမိဘာသာ php.net မွာေလ့လာနိုင္ပါတယ္၊</p>

<pre><code>Bicycle::wheels(); // result 2 
</code></pre>

<p>Static method နဲ့ scope resolution အေျကာင္းရွငး္ျပျပီးသြားျပီဆိုေတာ့  <br>
Facade ဆိုတာဘာလဲ ဆိုတာ နမူနာ ျကည့္ျပီး တစ္ခ်က္ေလာက္ေလ့လာျကည့္ရေအာင္ဗ်၊ </p>

<pre><code>Request::except(‘_token’);
</code></pre>

<p>PHP နည္းအရ ျကည့္မယ္ဆိုရင္ Request class ထဲမွာရိွတဲ့ public static function except  ကို သြားေခါျပီး အလုပ္လုပ္ေပးရမွာပါ၊ ဘာေျကာင့္လဲဆိုေတာ့ :: scope resolution operator သည္ static အတြက္သာ ေခါသံုးလို့ရတဲ့ အတြက္ေျကာင့္ျဖစ္ပါတယ္၊ </p>

<p><img src="{{ site.url }}img/facade-1.jpg" alt="enter image description here" title=""></p>

<p>static ေျကျငာမထားသည့္ method</p>

<p>တကယ္တမ္း Request Class ကို သြားျကည့္တဲ့အခါမွာ public static function except  ကိုမေတြ့ပါဘူး ၊ Object ေဆာက္ျပီးေခါသံုးမွသာရမဲ့ public except function ကိုေတြ့ပါလိမ့္မယ္. </p>

<p>ဟုတ္ျပီ ဘယ္လိုမ်ား Laravel က scope resolution operator ကို ခါသံုးလို့ရေအာင္ လုပ္ထားပါသလဲ ? သင္လဲ စိတ္၀င္စားလာျပီ ဟုတ္တယ္မလား xP  <br>
ဒီေတာ့ က်ေနာ္တို့ ယူသံုးထားတဲ့ Request Facade ကိုရွာေဖြျကည့္ပါတယ္၊</p>

<p><img src="{{ site.url }}img/facade-2.jpg" alt="enter image description here" title=""> <br>
Request Facade Class</p>

<p>ဒါကေတာ့ Request Facade object ျဖစ္ျပီး ‘request’ ဆိုတဲ့ string တစ္ေျကာင္းကိုသာ return  ျပန္ထားပါတယ္၊ျပီးေတာ့ Facade class ကို extends လုပ္ထားတာေတြ့ရမွာပါ၊ ဒါကေတာ့ Facade register လုပ္ရာမွာ လိုက္နာရမဲ့ နည္းျဖစ္ပါတယ္၊ အေသးစိတ္ register လုပ္နည္းကိုေတာ့ ေအာက္ကလင့္ခ္မွာေလ့လာနုိင္ပါတယ္၊  <br>
<a href="https://laravel.com/docs/5.0/facade">https://laravel.com/docs/5.0/facade</a>… ၊</p>

<p>Request Facade ရဲ့ parent class ျဖစ္တဲ့ Illuminate\Support\Facades\Facade; မွာေတာ့ က်ေနာ္တို့ရွာေနတဲ့ သဲလြန္စကို ေတြ့နိုင္ပါတယ္၊  <br>
__callStatic method သည္ php magic method တစ္ခုျဖစ္ျပီး class ထဲ ၇ိွ မသတ္မွတ္ထား သည့္ static method မ်ားကို ေခါသည့္အခါ invoke လုပ္မည့္ method တစ္ခုျဖစ္သည္၊ </p>

<p><img src="{{ site.url }}img/facade-3.jpg" alt="enter image description here" title=""></p>

<p>ဒါဆို က်ေနာ္တို့ ဘယ္လို အလုပ္လုပ္သြားလဲ ျပန္ျပည့္ရေအာင္၊</p>

<pre><code>Request::except(‘token’);  
</code></pre>

<p>သံုးလိုက္တဲ့ အခ်ိန္မွာ Request Class မွာ  <br>
public static function except() မရိွတဲ့ အတြက္ေျကာင့္ __callStatic() method invoke အလုပ္လုပ္ပါတယ္၊  <br>
ထို့ေနာက္ </p>

<pre><code>$instance = static::getFacadeRoot(); // $request 
</code></pre>

<p>ဆိုတဲ့ method call ျပီး IOC container ထဲမွွာ ‘request’ ဆိုတဲ့ binding name  <br>
[ပံု(2)တြင္ bind ထားျခင္းကိုေတြ့နိုင္သည္] <br>
နဲ့ ရွာျပီး instantiated လုပ္ျပီးသား Request object ကို $instance variable ထဲထည့္လိုက္ပါတယ္</p>

<p>ထို့ေနာက္ Request Facade ကို ေခါသံုးစဥ္က အသံုးခ်ခဲ့သည္ static method နာမည္ျဖင့္ <script type="math/tex" id="MathJax-Element-31">instance object ေပါတြင္ထပ္မွန္ေခါယူျခင္းျဖင့္ အမွန္တကယ္ ေခါယူသင့္သည္ method ကို laravel မွ resolve လုပ္ေပးသြားျခင္းျဖစ္ပါသည္၊  
</script>instance-&gt;<script type="math/tex" id="MathJax-Element-32">method(…args); // </script>request-&gt;except(‘_token’); </p>

<hr>

<p>Request::except(‘token’);  ၏အမွန္တကယ္ အလုပ္လုပ္သြားပံုကေတာ့ ေအာက္ပါအတိုင္းျဖစ္ပါသည္</p>

<pre><code>$request = app('request'); // resolve Request Object from IOC container
$request-&gt;except(‘_token’); // get static method name and apply on object with params.
</code></pre>

<h1 id="note">Note</h1>

<p>သင့္အေနျဖင့္ Laravel ၏ Facade Pattern နွင့္ အျခားေသာ Facade Pattern ကြဲျပားျခားနားမွုရိွသည္ကို သတိခ်ပ္သင့္ေပသည္</p>

<h1 id="protip">ProTip</h1>

<p>Facade is bad for testing.</p>
