---
layout: post
title: Serialization কি ? 
permalink: /what-is-serialization
---


![Imgur](http://i.imgur.com/6sIPLQw.jpg)


প্রথমেই পাইথন টার্মিনাল ওপেন করি।  person নামের একটি empty dictionary তৈরি করি। এরপর একে একে name, age, favorite_color নামের key যোগ করি - 

	>>> person = {}
	>>> person['name'] = 'Jackie Chan'
	>>> person['age'] = 62
	>>> person['favorite_color'] = ('red', 'blue', 'black')

এখন person অবজেক্ট এর টাইপ দেখতে -

	>>> type(person)
	<class 'dict'>

[dict][python_dictionary] ডাটা টাইপ পাইথন প্রোগ্রামিং এর একটি কমন ডাটা টাইপ। এই ধরনের ডাটা টাইপ প্রোগ্রামে অথবা প্রোগ্রাম রানটাইমে মেমোরিতে সেইভ করে রাখার জন্য সুবিধাজনক। কিন্তু ধরুন আপনার প্রোগ্রাম শাট-ডাউন হওয়ার পর কিছু ডাটা সেইভ করে রাখা দরকার পড়লো, যাতে পরবর্তীবার প্রোগ্রাম চালু হলে তা ব্যবহার করা যায়। 

পাইথন এর [pickle][python_pickle] মডিউল এর জন্য পারফেক্ট! [pickle][python_pickle] এর সাহায্যে পাইথন অবজেক্ট স্ট্রাকচারকে বাইনারী ডাটা তে serialize করা যায় এবং pickle দ্বারা serialize করা ডাটা কে আবার de-serialize করা যায়। person অবজেক্টকে উদাহরণ হিসেবে ইউজ করতে পারি আমরা। একই টার্মিনালেই আমরা পরবর্তী কোডগুলো লিখি। 

	>>> import pickle      
	>>> serialized_person = pickle.dumps(person)
	>>> type(serialized_person)
	<class 'bytes'>

এখানে pickle ব্যবহার করে person অবজেক্টকে serialize করে ```bytes``` টাইপে কনভার্ট করে ফেললাম। 
এখন যদি আমরা serialized_person ভ্যারিয়েবল এর ভ্যালু দেখি -- 

	>>> serialized_person
	
	b'\x80\x03}q\x00(X\x04\x00\x00\x00nameq\x01X\x0b\x00\x00\x00Jackie Chanq\x02X\x0
	e\x00\x00\x00favorite_colorq\x03X\x03\x00\x00\x00redq\x04X\x04\x00\x00\x00blueq\
	x05X\x05\x00\x00\x00blackq\x06\x87q\x07X\x03\x00\x00\x00ageq\x08K>u.'

এখন serialized_person এর ভ্যালুকে আমরা de-serialize করে আবার dict টাইপে নিতে পারবো। 

	>>> deserialized_person = pickle.loads(serialized_person)
	
	>>> type(deserialized_person)
	<class 'dict'>

দেখতে পাচ্ছি serialized_person এর ভ্যালুকে আবার dict টাইপে de-serialize করে ফেলেছি। 
এখন আমরা যদি deserialized_person এর ভ্যালু দেখি-

	>>> deserialized_person
	
	{'name': 'Jackie Chan', 'favorite_color': ('red', 'blue', 'black'), 'age': 62}

জাস্ট প্লেইন সিম্পল পাইথন dictionary!

> pickle ব্যবহার করার কারণে এটি pickling/unpickling নামেও পরিচিত। 

pickle ব্যবহার করে serialization শুধুমাত্র পাইথন প্রোগ্রামের জন্য। কিন্তু ডাটা যদি নেটওয়ার্ক ব্যবহার করে সেন্ড করা হয় এবং ক্লায়েন্ট যদি পাইথন প্রোগ্রাম না হয়ে থাকে তাহলে pickle ব্যবহার করে এই ধরনের serialization কাজে আসবে না। 
উদাহরণ হিসেবে চিন্তা করুন -- ব্যাকএন্ড পাইথনে লেখা একটি REST-api আর ক্লায়েন্ট হতে পারে JavaScript, এন্ড্রয়েড ফোন (Java) ইত্যাদি। এক্ষেত্রে serialize করা ```bytes``` টাইপ কনভার্ট করে একেক ক্লায়েন্টে ইউজ করা করা খুব পেইনফুল একটা কাজ হবে। 
এক্ষেত্রে পাইথন এর বিল্টইন ```json``` মডিউল ব্যবহার করা যায়। ```JSON``` বা ```JavaScript Object Notation``` একটি serialization ফরম্যাট। নাম শুনে মনে হতে পারে এটি শুধুমাত্র JavaScript এ ব্যবহারের জন্য। কিন্তু বেশিরভাগ প্রোগ্রামিং ল্যাঙ্গুয়েজই ```JSON``` সাপোর্ট করে।
চলুন একটি উদাহরণ দেখি। প্রথমে myself নামের একটি dictionary ক্রিয়েট করি - 

	>>> myself = {}
	>>> myself['name'] = 'Ikramul Alam'
	>>> myself['favorite_programming_lang'] = 'python'
	>>> myself['favorite_frameworks'] = ['flask', 'django', 'scrapy']
	>>> myself['hobbies'] = ['reading books', 'playing video games', 'watching movies']
	>>> myself['favorite_frameworks'] = ('flask', 'django', 'scrapy')

এখন myself অবজেক্টটি কে json ফরম্যাটে কনভার্ট করতে আমরা পাইথন এর বিল্টইন ```json``` মডিউল ব্যবহার করবো। 

	>>> import json
	>>> myself_json = json.dumps(myself)
    
এখন আমরা যদি myself_json এর ভ্যালু দেখি - 

	>>> myself_json
	'{"name": "Ikramul Alam", "favorite_frameworks": ["flask", "django", "scrapy"], 		"favorite_programming_lang": "python", "hobbies": ["reading books", "playing pc 		games", "watching movies"]}'
    
```myself``` এর 'favorite_frameworks' ভ্যালু যদিও [tuple][python_tuple], কিন্তু json কনভার্ট করে তা সাধারণ পাইথন [list][python_list] এর মত করে ফেলেছে। 
এখন যদি json এ serialize করা অবজেক্ট এর টাইপ দেখি, তাহলে দেখবো তা ```str``` টাইপ। 

	>>> type(myself_json)
	<class 'str'>
    
আমরা চাইলে serialize করা ডাটা একটি ফাইলে সেইভ করে রাখতে পারি - 

	>>> with open('myself.json', 'w') as f:
	...     json.dump(myself, f)
	... 
    
***
<em>sources:</em>

* [Serializing Python Objects](http://www.diveinto.org/python3/serializing.html)
* [Why Binary Files are Needed](https://chortle.ccsu.edu/java5/Notes/chap86/ch86_6.html)

    
    
[python_dictionary]: https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
[python_pickle]: https://docs.python.org/3/library/pickle.html
[python_tuple]: https://docs.python.org/3/library/stdtypes.html#tuples
[python_list]: https://docs.python.org/3/library/stdtypes.html#lists

 
