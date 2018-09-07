# fetching-data-from-apis
A workshop on fetching data from public APIs &amp; comparison to other scraping/fetching techniques

*Note: We recommend downloading and using the most recent version of [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/new/) in this workshop. Firefox has some great tools for developers, including easy viewing of files in JSON formatting.*

## Resources

[List of Public APIs](https://github.com/toddmotto/public-apis)

[API for Public API collection - meta!](https://github.com/davemachado/public-api)

[Developer access to data.ny.gov datasets](https://data.ny.gov/developers)

[A technical introduction to APIs](https://restful.io/an-introduction-to-api-s-cee90581ca1b)

[Dog API](https://dog.ceo/dog-api/)

## Learning Goals

At the end of this workshop, you will be able to:
* Explain the concept of a public API and identify a few use-cases relative to your work/studies/personal curiositiy
* Use query strings with parameters in a URL to fetch subsets of data from an API
* View and parse JSON data, and recognize the difference between JSON and CSV data
* Identify the basic categories of APIs
* Identify at least one use-case for interfacing with an API using a programming language like Python (beyond the scope of this specific workshop, but helpful to recognize out in the wild)


## Outline

1. Why fetch data with a public API?
2. What is a Public API? (NY State Public API)
3. A glimpse under the hood: what is the request response cycle?
4. Types of APIs (hint: they're everywhere!)
5. Understanding the structure of data (parsing the JSON tree)
6. Future directions: accessing with Python, comparison to web scraping, etc.


### 1. Why fetch data with a public API?

Whether you are a student, researcher, librarian, or developer, you are already in the habit of seeking out data to answer questions that matter to you. This might look like: finding a specific e-mail in your inbox, typing search terms into a search engine, looking up historical materials in an archive, entering an address into a mapping app, searching for key words within a journal article, and so on.

Note that in each of these examples, we could type our search terms or our **query** into a search box, which is often visually represented on a web page, toolbar, or phone app interface. 

Each of these queries usually results in one of the following: a specific point of data (such as the latitude and longitude of a restaurant), a sub-section of a longer document (like sentences in a journal article that match your search term), or a set of documents within a much larger collection (like a list of 900,000 search results from the hundreds of trillions of web pages indexed by Google.) We might imagine that, behind the scenes, there is some process that goes into filtering and selecting a giant collection of data, perhaps structure into a database or many databases, and returning just the unique data that matches our search query conditions.

Today, we are going to introduce you to a new way of querying data from larger collections: **Public APIs**. APIs solve an important problem: how can the facilitators of databases and datasets enable future users to access their data? And specifically, how can this data be made accessible *without knowing the specific desired use-cases ahead of time*, and *without requiring all users to use visual, closed interfaces like database searches?*.

### 2. What is a Public API?

A Public API is a service that supports free, open access to some kind of data. "API" stands for Application Programming Interface. In other words, the API takes some kind of query from the user - it can be as general as "show me all of your data" or as specific as "only show me data from August 1st, 2018, at 9am, if it contains the words "cute dog". The API, in turn, interfaces with the dataset/database to grab the data that matches the user's query. Finally, the API returns the data to the user in some format that will be useful. At the moment, JSON is the most common format for data returned from an API (more on JSON later).

Let's dive right in and see an API in action! Take a look at the [Dog API](https://dog.ceo/dog-api/). Try clicking the "Fetch" button next to the URL in the middle of the page. As you may expect upon seeing the word "random", this button fetches a random dog which displays in the bottom right.

You'll also notice a box labeled **JSON** filling up with some important-looking data.

An API query can take several forms. Quite often, an API will be accessible through an **endpoint**, or a URL that is formatted in a specific way to get the data we want.

While the Dog API gives us some fancy preview features, we actually don't need any of them to query the Public API directly. Try copy and pasting the following URLs into your browser address bar (ideally in a new tab):

https://dog.ceo/api/breeds/image/random
https://dog.ceo/api/breed/husky/images
https://dog.ceo/api/breeds/list/all 

Let's also try something non-dog-related. Here is New York State's Deparment of Health [dataset on recent food service establishment inspections.](https://health.data.ny.gov/Health/Food-Service-Establishment-Last-Inspection/cnih-y5dw)

New York State partners with a service called Socrata to make every dataset in its collection available through APIs. [Here is documentation about using the API](https://dev.socrata.com/foundry/health.data.ny.gov/f285-x9ha)

Or, you can copy the API endpoint and paste it in your browser: https://health.data.ny.gov/resource/f285-x9ha.json

And specifically for Tompkins County:  https://health.data.ny.gov/resource/f285-x9ha.json?county=TOMPKINS

### 3. A glimpse under the hood: what is the request response cycle?

So far, we've used words like "querying", "fetching", and "requesting" to describe the process of getting data via an API. Here, we are going to step back and look at the big picture process behind these exchanges: the **request response cycle**.

Nearly everything you do on the web is a product of the request-response cycle. Consider when you type in https://github.com/ into the browser window. You may conceptualize "going to a website" as navigating to a fully-formed, pre-existing space. In fact, typing a URL into an address bar and hitting enter is actually closer to sending a request over the Internet. Your web browser automatically adds some extra information to this request - it specifies what types of responses will be permissible, and what types to ignore or block. This data is stored into **headers**, using a method called **POST**.

Somewhere in the distance, a sever will receive your request and choose whether or not to emit a response. Generally this response has a few pieces: a status code (if all goes well, this will be 200, which means "success! all ok!"), headers (generally telling your web browser what type of information to expect), and the data itself (this is the most familiar: the content of the web page, generally as a .html file).

For a simpler or "static" website, this .html file (let's say, dogs.html) is essentially a replica of a dogs.html file that exists in the server's memory. However, it is much more common now that the server is actually generating these .html files on-the-fly based on a combination of factors (perhaps it starts with a template, but actually grabs more up-to-date data from a database, checks if you are logged in, and so on). This is sometimes called a **dynamic web page**.

This request response cycle is at the heart of how a API works. The information you request via an API is almost never sitting there, fully formed, ready to go. Instead, it requires you to submit a **request** using a set of conditions or **parameters**. The API must be prepared to interpret the parameters in the way you've written them – this is why reading the documentation for a given API is so important. When an API approves, it will submit a response to you. Quite commonly, this is a mixture of a status code (such as 200, all good!), specification of how data is formatted (quite often, JSON), and the JSON data itself, which is essentially one long collection of text or **string**.

(You can read a more detailed explanation of the request response cycle [here](https://restful.io/an-introduction-to-api-s-cee90581ca1b))

### 4. Types of APIs

Not every API accepts the same kinds of requests, or responds in the same way.

### 5. Understanding the structure of data

### 6. Future directions: accessing with Python, comparisons to web scraping, etc.
