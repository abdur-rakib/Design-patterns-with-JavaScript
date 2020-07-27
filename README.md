# What is Design Pattern?
কোনো application তৈরী করার সময়, আমরা ভিন্ন ভিন্ন জায়গায় কিছু একই রকম সমস্যার সম্মুখিন হলে, সমস্যাগুলোর সমাধান এর জন্য যদি একটা reusable pattern design করা যায়, যা ঐ সমস্যাগুলোর জন্য একটা ভালো সমাধান দিতে পারে। তবে advanced এই সমাধানকেই আমরা Design pattern বলি।
সহজ কথায়, **Design pattern হলো একটা কমন সমস্যার জন্য তৈরী করা reusable সমাধান।** ডিজাইন প্যাটার্ন বোঝা বা এর সাথে পরিচিত হওয়াটা বেশ প্রয়োজন কেননাঃ 
* Pattern হলো নির্দিষ্ট সমস্যার জন্য প্রমানিত সলুশান।
* Application development processএর সময় এটা ছোটো খাটো issue থেকে বাচাতে সাহায্য করে যেটা ভবিষ্যতে application এর বড় ক্ষতি করতে পারতো
* নির্দিষ্ট Pattern আমাদের  application এর ওভারওল কোডের সাইজকে ছোটো করে। একই সাথে কোডকে আরো বেশি readble করে।
* এটা reusable


# Categories Of Design Pattern
৩ টা ক্যাটাগরিতে মোটামুটি ২৩ টা প্যাটার্নকে ডিজাইন প্যাটার্নের ফাউন্ডেশান ধরা হয় [এদেরকে 23 Gang of Four (GoF) patterns বলা হয় ]। ক্যাটাগরিগুলো হলোঃ
* [**Creational**](#Creational-Design-Patterns)
    - [Abstract Factory](#Abstract-Factory)
    - [Builder](#Builder)
    - Factory Method
    - Prototype
    - Singletone
* **Structural**
    -  Adapter
    - Bridge
    - Composite
    - Decorator
    - Facade
    - Flyweight
    - Proxy
* **Behavioral**
    - Chain of Resp
    - Command
    - Interpreter
    - Iterator
    - Mediator
    - Memento
    - Observer
    - State
    - Strategy
    - Template Method
    - Visitor



# #Creational Design Patterns
Creational pattern মূলত object তৈরীর মেকানিজমগুলোর নিয়ন্ত্রন প্রক্রিয়ার উপর ফোকাস করে।
কোনো উদ্ভূত সমস্যার জন্য এই প্যাটার্নের basic approach টা হচ্ছে, প্রোজেক্টে কিছু কপ্লিক্সিটি (যাকে আমরা প্যাটার্ন বলছি) যুক্ত করে object creation process টা controll করা যাতে করে সমস্যার একটা সুষ্ঠ সমাধান দেয়া সম্ভব হয়। এই ক্যাটাগরীর অন্তর্ভূক্ত pattern গুলো হলোঃ Abstract Factory, Builder,  Factory Method, Prototype and Singleton.



## Abstract Factory
Abstract factory, একই বিষয়ের দ্বারা সম্পর্কযুক্ত বিভিন্ন অব্জেক্ট তৈরী করে। সহজ কথায়, এটা এমন একটা প্যাটার্ন যেখানে একটি Factory object থাকবে - যার কাজ হলো অন্য আরেক রকমের অব্জেক্ট তৈরী করা।

কিন্তু প্রশ্ন হচ্ছে, আমরা কেনো একটা Factory object ব্যবহার করে অন্যান্য object তৈরী করবো! যখন আমরা এই কাজটা সরাসরি **new** keyword ব্যবহারের মাধ্যমে constructor ফাংশন call করেই করতে পারি?\
এর কারন, একটা object তৈরীর পুরো পদ্ধতির উপর constructor ফাংশনের খুব অল্প নিয়ন্ত্রন থাকে। তার মানে,একটা অব্জেক্ট তৈরীর জন্য যে বেসিক কাজগুলো করতে হয় কন্সট্রাক্টর ফাংশন তা করে আমাদেরকে একটা অব্জেক্ট তৈরী করে দেয়। কিন্তু, অনেক সময় দেখা যায় একটা ওব্জেক্ট তৈরীর জন্য আমাদের আরো কিছু বিষয়ের উপর নিয়ন্ত্রনের প্রয়োজন হচ্ছে। সেক্ষেত্রে আমরা কন্সট্রাক্টর ফাংশনের উপর নির্ভর না করে, এমন একটা অব্জেক্টকে এই অব্জেক্ট তৈরীর দায়িত দেই যা ঐ বিষয়গুলো কিভাবে নিয়ন্ত্রন করতে হয়ে তা জানে।

### Example :
মনেকরি, মোঃ মফিজ সাহেবের আইস্ক্রিম ও কেক বানানোর দুইটা আলাদা কারখানা আছে। তিনি চাচ্ছেন, তার দুই কারখানার সব কাস্টমারকে একজায়গায় আলাদা আইডেন্টিটি দিয়ে রাখবেন। এবই কাস্টোমারের ঐ লিস্টে, আইস্ক্রিম কারখানার সাথে সম্পর্কযুক্ত কাস্টমারগুলোকে বলা হবে IcecreamCustomer আর কেক কারখানার সাথে সম্পর্কযুক্ত কাস্টমারদের বলা হবে CakeCustomer
``` javascript
function IcecreamCustomer(name) {
    this.name = name;
    this.say = function () {
        console.log(name + " is a icecream customer ");
    };
}
 
function IcecreamFactory() {
    this.addCustomer = function(name) {
        return new IcecreamCustomer(name);
    };
}
 
function CakeCustomer(name) {
    this.name = name;
    this.say = function () {
        console.log(name + " is a cake customer ");
    };
}
 
function CakeFactory() {
    this.addCustomer = function(name) {
        return new CakeCustomer(name);
    };
}
 
function run() {
    var customer = [];
    var icecreamFactory = new IcecreamFactory();
    var cakeFactory = new CakeFactory();
 
    customer.push(icecreamFactory.addCustomer("Ahmed Abdul Barkik"));
    customer.push(icecreamFactory.addCustomer("Sabbir Hasan"));
    customer.push(cakeFactory.addCustomer("Tanzid Hasan"));
    customer.push(cakeFactory.addCustomer("Abdur Rakib"));
 
    for (let i = 0, len = customer.length; i < len; i++) {
        customer[i].say();
    }
}
run();
```

## Builder
বিভিন্ন কমপ্লেক্স object-এর বিস্তারিত ডেফিনেশন না জেনে, শুধুমাত্র টাইপ ও কনগটেন্ট জেনেই ঐ কমপ্লেক্স object-গুলো তৈরী করতে পারে যে pattern তাকে Builder pattern বলে।

-"builder" বিভিন্ন কমপ্লেক্স object তৈরী ও object-গুলোর বিভিন্ন intermediate state মেইন্টেইন করতে পারে। আর অব্জেক্ট তৈরী এবং তাকে মেইন্টেইন এর মাধ্যমে তৈরী করে বিভিন্ন প্রোডাক্ট। আর প্রোডাক্ট তৈরী শেষ হলে ক্লায়েন্ট সেই ফলাফল (তৈরীকৃত প্রোডাক্ট) "builder" থেকে retrieve করতে পারে।

এভাবে object তৈরীর মূল উদ্দেশ্য হলো, client সাইটে বিভিন্ন অপারেশনগুলো সহজ করা। আর উপকারিতা হলো, একজন client বিভিন্ন কমপ্লেক্স object-গুলোর ডেফিনেশাঙ্গুলো না জেনেউ সে object-কে সহজে ব্যবহার করতে পারবে।

### Example :
মনেকরি, মোঃ মফিজ সাহেব, তার আইস্ক্রিম ও কেকের কারখানায় জন্য 'আব্দুস সালাম' নামের একজন লোককে ম্যানেজার হিসেবে নিয়োগ করেছে। এখন এটা স্বাভাবিক যে সালাম ভাই এর জন্য প্রতিটা কারখানায় আইস্ক্রিম আর কেক আলাদা আলাদা ভাবে তৈরীর প্রতিটা স্টেপ মেইন্টেইন করা সম্ভব না। 
সালাম ভাই এর কাজ হলো, কিভাবে কেক বানানো হয় বা কিভাবেই বা আইস্ক্রিম বানানো হয় তা নিয়ে মাথা না ঘেমে, বরং প্রোডাক্টগুলো (আইস্ক্রিম বা কেক) ঠিক ভাবে শিডিওল অনুযায়ী তৈরী হচ্ছে কিনা সেদিক খেয়াল করা।
এখেত্রে সালাম সাহেব যেটা করতে পারেন তা হলোঃ 
* সালাম সাহেব কর্মিদের বলবে, সবাই উপদানা প্রস্তুত করো। কর্মিরা নিজ নিজ কারখানার প্রোডাক্টের জন্য প্রয়োজনীয় উপদান গুলো প্রস্তুর করে রাখবে।
* এরপর সালাম সাহেব বলবে, উপাদাঙ্গুলো দিয়ে প্রোদাক্ট গুলো তৈরী করো। কর্মিরা আবার নিজ নিজ কারখানায় তৈরীকৃত পন্যের উপাদানগুলো ব্যবহার করে পণ্য তৈরী করবে। 
* এরপর সালাম সাহেব যখন বলবে পন্য প্যাকেট করো। কর্মিরা নিজ নিজ কারখান্য তৈরী প্রোডাক্ট প্যাকেট করবে।

এক্ষেত্রে কিন্তু সালাম সাহেবের জন্য দুইটা ভিন্ন কারখানায় পণ্যের জন্য কি কি উপাদান লাগবে, কিভাবে বানাবে বা কিভাবে প্যাকেট করতে হবে তা জানার প্রয়োজন নাই। তিনি শুধু কমপ্লেক্স এই কাজগুলোর জন্য কর্মি ঠিক করে (object তৈরী করে) বাহিরে থেকেই বিভিন্ন কাজগুলো(কমপ্লেক্স অপারেশঙ্গুলো) নিয়ন্ত্রন করতে পারবে। যেটা Builder প্যাটার্ন এর একটি উদাহরণ।

``` javascript
function Manager() {
    this.productControll = function(builder) {
        builder.collectIngridents();
        builder.makeProducts();
        builder.productPakaging();
    }
}

function IcecreamShef() {
    this.icecream = null;
 
    this.collectIngridents = function() {
        this.icecream = new Icecream();
        console.log("Ingridents collected for Icecream!");
    };

    this.makeProducts = function() {
        this.icecream.makeIcecream();
    };

    this.productPakaging = function(){
        this.icecream.pakaging();
    }
}

function CakeShef() {
    this.cake = null;
 
    this.collectIngridents = function() {
        this.cake = new Cake();
        console.log("Ingridents collected for Cake!");
    };

    this.makeProducts = function() {
        this.cake.makeCake();
    };

    this.productPakaging = function(){
        this.cake.pakaging();
    }
}

function Icecream(){
    this.ingredients = ["milk", "sugar", "almond", "flavour"];
    this.makeIcecream = () => {console.log("Icecream is made with: " + this.ingredients);}
    this.pakaging = () => {console.log("Icecream pakaged!\n")}

}
function Cake(){
    this.ingredients = ["Flour", "sugar", "egg", "salt"];
    this.makeCake = () => {console.log("Cake is made with: " + this.ingredients);}
    this.pakaging = () => {console.log("Cake pakaged!\n")}
}

function run(){
    let SalamVai = new Manager();
    let icecreamShef = new IcecreamShef();
    let cakeShef = new CakeShef();

    SalamVai.productControll(icecreamShef);
    SalamVai.productControll(cakeShef);
}
run();
```
