<h1>Multi Threaded Proxy Server with Cache</h1>

This project is implemented using `C` and Parsing of HTTP referred from <a href = "https://github.com/vaibhavnaagar/proxy-server"> Proxy Server </a>


## Index

- [Project Theory](https://github.com/asif-0007/ProxyServerClient#project-theory)
- [How to Run](https://github.com/asif-0007/ProxyServerClient#How-to-Run)
- [Demo](https://github.com/asif-0007/ProxyServerClient#Demo)

## Project Theory

[[Back to top]](https://github.com/asif-0007/ProxyServerClient#index)

##### Introduction

##### Basic Working Flow of the Proxy Server:
![](https://github.com/asif-0007/ProxyServerClient/blob/main/ProxyServerClient/images/UML.png)

##### How did we implement Multi-threading?
- Used Semaphore instead of Condition Variables and pthread_join() and pthread_exit() function. 
- pthread_join() requires us to pass the thread id of the the thread to wait for. 
- Semaphore’s sem_wait() and sem_post() doesn’t need any parameter. So it is a better option. 
- The main function creates a thread for each client connection using pthread_create.
- Each thread executes the thread_fn function, which handles the client request.
- Mutex locks are used to synchronize access to shared resources, such as the cache.
- pthread_join is used to wait for threads to finish before exiting the program.

##### Motivation/Need of Project
- To Understand → 
  - The working of requests from our local computer to the server.
  - The handling of multiple client requests from various clients.
  - Locking procedure for concurrency.
  - The concept of cache and its different functions that might be used by browsers.
- Proxy Server do → 
  - It speeds up the process and reduces the traffic on the server side.
  - It can be used to restrict user from accessing specific websites.
  - A good proxy will change the IP such that the server wouldn’t know about the client who sent the request.
  - Changes can be made in Proxy to encrypt the requests, to stop anyone accessing the request illegally from your client.
 
##### OS Component Used ​
- Multithreading
- Locks 
- Semaphore
- Cache (LRU algorithm is used in it)

##### Limitations ​
- If a URL opens multiple clients itself, then our cache will store each client’s response as a separate element in the linked list. So, during retrieval from the cache, only a chunk of response will be send and the website will not open
- Fixed size of cache element, so big websites may not be stored in cache. 

##### How this project can be extended? ​
- This code can be implemented using multiprocessing that can speed up the process with parallelism.
- We can decide which type of websites should be allowed by extending the code.
- We can implement requests like POST with this code.


# Note :-
- Code is well commented. For any doubt you can refer to the comments.


## How to Run

```bash
$ git clone https://github.com/asif-0007/ProxyServerClient.git
$ cd ProxyServerClient
$ make all
$ ./proxy <port>
```
`Open http://localhost:port/https://www.academics.mnnit.ac.in/new`

- After opening this link the response from the server will be stored in cache
- Open the link again and the request will be directly handled from the cache instead of hitting another request on server

# Note:
- This code can only be run in MacOS/Linux Machine. Please disable your browser cache as shown in the image

## Demo
![](https://github.com/asif-0007/ProxyServerClient/blob/main/ProxyServerClient/images/website.png)
![](https://github.com/asif-0007/ProxyServerClient/blob/main/ProxyServerClient/images/working_cache.png)
- When website is opened for the first time (`url not found`) then cache will be miss.
- Then if you again open that website again then `Data is retrieved from the cache` will be printed.

