---
layout:	post
title:	"The efficient way of using multiprocessing with pymongo"
date:	2018-11-20
featured-image: 1*F0pBSUqAuDdtfPMncXssBQ.jpeg
---

  ![](/img/1*F0pBSUqAuDdtfPMncXssBQ.jpeg)
  
  
  Mongodb is a database which has it’s positives and negatives but regardless of what the world says knowing how to use it efficiently and to your advantage can save you time and effort and maybe switching to a different database itself(Postgres, anyone?).

[Pymongo ](https://api.mongodb.com/python/current/)is the ORM (Object relational mapper) or a programming interface of choice to interact with python. It is the written in the very friendly python language and has great support.

I faced a problem where I had to compare an input to every document in the database, do a calculation based on the comparison and return the results. This would have been pretty easy if the database contained only a few records, but since it had more than ~120,000 records I knew an alternative was needed. It was an obvious decision then to make parallel calls to the Database; putting those multiple cores(only 8 in my case:/) to work.

When it came down to it, the support in the community for using multiprocessing with pymongo was minimal and the information provided by pymongo’s [documentation](http://api.mongodb.com/python/current/faq.html#is-pymongo-fork-safe) was helpful but too distilled.

*PyMongo is not fork-safe. Care must be taken when using instances of *[*MongoClient*](http://api.mongodb.com/python/current/api/pymongo/mongo_client.html#pymongo.mongo_client.MongoClient "pymongo.mongo_client.MongoClient")* with **fork()**. Specifically, instances of MongoClient must not be copied from a parent process to a child process. Instead, the parent process and each child process must create their own instances of MongoClient.*

Forks and processes are all concepts of multiprocessing and would be a long topic to talk about in this post. In brief, a client is an object which interacts with the mongodb server and if the same client is used in the child process of a parent process, it may lead to a situation called a deadlock where both the parent and child process wait for resources to become available and the program is stuck. Hence, the rule is simple — **each child process should have its own instance of the client.**

Using this principle you can write a simple program using python’s multiprocessing module,

{% gist 4363e1e4a4a7b71512da1253f4170b73 %}

This seems pretty neat except that it takes a lot of time. The reason for that? That the every process is creating a new client and that is being done for every document. So for 120,000 documents the calculate function is called 120,000 times and spawning 120,000 clients. Each client is just making one call to the mongo db database. PEven though these 120,000 calls are shared between 8 processors it is still quite slow. So what can be done so that we can use all 8 processors, but not make a new client for every function call. That’s right, we need to divide these calls among clients and enable every client to handle multiple calls. In other words, we need to create chunks from our input.

### Chunking

The logic is pretty simple. If we chunk our input into blocks and only create one client for each block (simultaneously with multiple processes running in parallel) it would speed up our code without significantly increasing the number of database calls each client has to make. Python provides a great and easy way to chunk your data. To make use of this method we first need to make a single call to the database to get all the ‘\_id’s (identifiers unique to each document) for every document and store them in a list

```
cl = MongoClient('localhost') #make sure the name of this client is different from the one used inside the function  
db = cl.db\_name  
collection = db['table\_name']  
document\_ids = collection.find().distinct('\_id') #list of all ids
```
Now we write a function to chunk this list

{% gist 4a3b21a682ab62496b7bc35ec506dffe %}

This code does exactly the same thing we were doing with the first simple method but using chunking. Now the calls to the chunking function are parallelised instead of calls to the mongodb directly. Hence, this takes much lesser time.

To be exact, the first method took around 20 minutes to complete on a 16GB machine with 8 cores for a simple calculation between input and all documents of 120,000 document large collection whereas the second method just took 19 seconds. The next time (as if) you use mongodb and multiprocessing together think of chunking your calls.

  
