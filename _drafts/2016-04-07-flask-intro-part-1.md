---
layout: post
title: ফ্লাস্কে হাতেখড়ি - পর্ব ১
permalink: /flask-intro-part-1
---
### ফ্লাস্ক কি?
[ফ্লাস্ক][flask] পাইথন বেইজড একটি মাইক্রো ওয়েব ফ্রেমওয়ার্ক। 
এটিকে কেন [মাইক্রো][why-called-micro] বলা হয় ওই প্রশ্নে যাচ্ছি না।  মাইক্রো শুনে এমন মনে করার কোন কারণ নেই যে এটি পাওয়ারফুল নয়! [Pinterest][pinterest] তাদের এপিআই'র জন্য [ফ্লাস্ক ব্যবহার করে][pinterest-use-flask-quora]। এছাড়াও হ্যাকাথনে সবচেয়ে বেশি ব্যবহার হওয়া ফ্রেমওয়ার্কের মধ্যে ফ্লাস্ক আছে [দ্বিতীয়][flask-in-hackathon] স্থানে! 

### ফ্লাস্ক কেন?
কারণ ফ্লাস্ক সিম্পল! আর তার চেয়েও বড় কথা হচ্ছে ফ্লাস্ক পাইথনে লেখা। :D
এখন ভ্রু কুচকানো প্রশ্ন আসতে পারে "সিম্পল বলে আসলে বুঝাচ্ছেন?"
তাই চলুন কথা না বাড়িয়ে কাজে নেমে পড়ি। 

### কি কি লাগবে?

#### পাইথন  

সর্বপ্রথম আপনার পিসিতে পাইথন ইন্সটল করা থাকতে হবে। ডাউনলোড করে ইন্সটল করে নিন [এখান][download-python] থেকে। 
আর যদি আপনি আমার মত লিনাক্স ব্যবহার করে থাকেন তাহলে আপনার এই ধাপটি নিয়ে চিন্তা না করলেও চলবে। ctrl+alt+t প্রেস করে টার্মিনাল ওপেন করুন, টাইপ করুন `python --version`। 	

```bash	
$ python --version
Python 2.7.10
```

এর মানে আপনার মেশিনে পাইথন ইন্সটল করা আছে। আমরা এখানে `python 2` ব্যবহার করবো। 

#### ভার্চুয়াল এনভায়রনমেন্ট অথবা virtualenv ??!

[virtualenv][virtualenv] একটি টুল যা আপনার পাইথন প্রজেক্টকে সিস্টেম পাইথন থেকে আলাদা করে রাখে। এটাকে আপনি মনে করতে পারেন একটি সাউন্ড প্রুফ রেকর্ডিং রুমের মত, যেখানে আপনি যত রকমের শব্দই করুন না কেন তা বাইরে আসবে না তেমনি এই ভার্চুয়াল এনভায়রনমেন্টের মধ্যে আপনি যাই করুন না কেন তা আপনার মেইন সিস্টেম পাইথন এর উপর অথবা আপনার অপারেটিং সিস্টেম এর উপর কোন প্রভাব ফেলবে না। 

> **virtualenv কেন ব্যবহার করবো?**  
> বিভিন্ন প্রজেক্টে বিভিন্ন প্যাকেজ ইন্সটলের দরকার হতে পারে, যেসব প্যাকেজ হয়তো শুধুমাত্র ঐ প্রজেক্টেই কাজে লাগবে। তাহলে আপনি কেন ঐসব প্যাকেজ পুরা অপারেটিং এর জন্য ইন্সটল করবেন? এমনও হতে পারে আপনি এক্সপেরিমেন্ট এর জন্য কোন পাইথন প্রজেক্ট নিয়ে কাজ করছেন যার জন্য বেশ কিছু প্যাকেজ ইন্সটলের দরকার হল এবং এক্সপেরিমেন্ট শেষে ওসব প্যাকেজ আপনার আর কাজে আসবে না। এক্ষেত্রে আপনি ঐসব ইন্সটল করা প্যাকেজ একটি একটি করে আন-ইন্সটল করতে পারেন। কিন্তু আপনার যদি অসংখ্য প্যাকেজ থেকে থাকে তাহলে তা হতে পারে আপনার জন্য দুঃস্বপ্নের মত! কিন্তু virtualenv তে আপনি এক্সপেরিমেন্ট চালালেন আর কাজ শেষে যখন আর দরকার পড়লো না তখন পুরা এনভায়রনমেন্ট টা ডিলিট করে দিলেন (আসলেই এত সহজ!)। 


**virtualenv ইন্সটল** 
টার্মিনাল ওপেন করে টাইপ করুন `sudo pip install virtualenv` এবং enter চাপুন।  

```bash   
$ virtualenv venv
New python executable in venv/bin/python
Installing setuptools, pip...done.
```


#### ফ্লাস্ক ইন্সটল   
* টার্মিনাল ওপেন করে টাইপ করুন `mkdir simple-flask` , simple-flask নামের একটি ফোল্ডার তৈরি হবে।
*  `cd simple-flask` টাইপ করে ঐ ফোল্ডারে ঢুকুন।
*  এখন আমরা একটি ভার্চুয়াল এনভায়রনমেন্ট তৈরি করবো।  
   `virtualenv venv`  এই কমান্ডের সাথে সাথে একটি ভার্চুয়াল এনভারনমেন্ট তৈরি হবে। এখানে venv এর বদলে যে কোন নাম দেওয়া যাবে।  
*  ভার্চুয়াল এনভায়রনমেন্ট এক্টিভেট করতে `source venv/bin/activate`
*  এখন আমরা ফ্লাস্ক ইন্সটল করবো। 
   টাইপ করুন `pip install flask` ।
   কয়েক সেকেন্ডের মধ্যে ফ্লাস্ক ইন্সটল হয়ে যাবে। 


এখন আমাদের লাগবে একটি টেক্সট এডিটর। [Sublime Text][sublime-text] ডাউনলোড করে ইন্সটল করে নিন। 


### Hello World!

`simple-flask` ফোল্ডারে একটি `app.py` নামের একটি ফাইল তৈরি করুন। 

ফাইলটিতে নিচের কোড টাইপ করুন:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
	return "Hello World!"

if __name__ == '__main__':
	app.run()
```

এবং সেইভ করুন।

* প্রথম লাইনে `from flask import Flask` এর সাহায্যে ফ্লাস্ক প্যাকেজ ইম্পোর্ট করা হয়েছে।   
*  দ্বিতীয় লাইনে ফ্লাস্ক এর ইন্সট্যান্স তৈরি করা হয়েছে। (আপাতত এই অংশটুকু নিয়ে মাথা না ঘামালেও চলবে) 
*  `@app.route('/')` [ডেকোরেটর][python-decorator] দিয়ে একটি রুট ডিফাইন করা হয়েছে। 
*  `hello` মেথডটি শুধুমাত্র একটি স্ট্রিং রিটার্ন করছে, যা আমরা আমাদের অ্যাপটি রান করলে ব্রাউজারে দেখতে পারবো। 
*  `app.run()` আমাদের অ্যাপটি রান করবে। 

টার্মিনালে `python app.py` টাইপ করুন। 

```bash
$ python app.py
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)

```  

এখন ব্রাউজারে [127.0.0.1:5000][localhost:5000] ওপেন করুন।  
**Hello World!**  
ctrl+c প্রেস করে টার্মিনাল থেকে ক্লোজ করতে পারবেন। 

voilà! ফ্লাস্ক ব্যবহার করে আমরা ছোটখাট একটি অ্যাপ তৈরি করলে ফেললাম! :) 










[flask]:  http://flask.pocoo.org/
[why-called-micro]:  https://en.wikipedia.org/wiki/Microframework
[pinterest]:  https://www.pinterest.com/
[pinterest-use-flask-quora]: https://www.quora.com/What-challenges-has-Pinterest-encountered-with-Flask/answer/Steve-Cohen?srid=hXZd&share=1
[flask-in-hackathon]: http://techcrunch.com/2015/07/28/which-programming-languages-get-used-most-at-hackathons/
[download-python]: https://www.python.org/downloads/
[virtualenv]: https://virtualenv.pypa.io/en/latest/
[sublime-text]: https://www.sublimetext.com/
[python-decorator]: https://realpython.com/blog/python/primer-on-python-decorators/
[localhost:5000]: http://127.0.0.1:5000/
