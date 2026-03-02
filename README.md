# CST8915 Lab 1 Readme

## Lab 1 - CST8915: Running Algonquin Pet Store on an Azure VM

Professor : Ramy Mohamed  
Student : Hesheng Yang 041094882


## Contents
Demo Youtube link :	1
Link to git rep:	1
Screenshot:	2
Technical Explanations	6
Service of Product Service (Rust + Warp)	6
Service of Order Service (Node.js + Express + RabbitMQ)	7
Service of Store Front (Vue.js)	7
Challenges and Learnings	8

## Demo Youtube link :  
https://www.youtube.com/watch?v=lxSAWYrbTvI

## Link to git rep:
https://github.com/hycst/CST8915-Lab1




## Screenshot:

rabbitmq-dashboard
Products:
Order-confirmation
Store-front

Setup MQ on Azure:
Check MQ output:
Start Service of Product:
Start service of Orders:
Start service of store:
 
## Technical Explanations

## Service of Product Service (Rust + Warp)
In the project, I rearch and understand is, the part of Product Service is to provide product data. Its job is to publish REST endpoints (using get ), so, the Store Front can get informaiton and then display available items and prices of each prduc.  This service is read only , such like  “catalog” service in a business system.
The service of product is built in Rust using the Warp web framework.  The reason is because Rust is fast, memory-safe, and efficient for small high-performance APIs. 
In the microservices architecture, this service is independen, it can scale, separately from the other two serice of ordering and analytics. It communicates with other services using HTTP/REST only: the Sevice of Store Front calls it directly, in order to load product data.  It does not need RabbitMQ.

## Product Service (Rust + Warp)
In the project, I rearch and understand is, the part of Product Service is to provide product data. Its job is to publish REST endpoints (using get ), so, the Store Front can get informaiton and then display available items and prices of each prduc.  This service is read only , such like  “catalog” service in a business system.
The service of product is built in Rust using the Warp web framework.  The reason is because Rust is fast, memory-safe, and efficient for small high-performance APIs. 
In the microservices architecture, this service is independen, it can scale, separately from the other two serice of ordering and analytics. It communicates with other services using HTTP/REST only: the Sevice of Store Front calls it directly, in order to load product data.  It does not need RabbitMQ.

## Service of Order Service (Node.js + Express + RabbitMQ)
In project, as my understanding, the Order Service is to receive customer orders, and then send the orders to event-driven pipeline. 
When the Store Front submits an order, this Order Service fistly validates the request,  then create an order message, after then publishes to RabbitMQ. This keeps the order workflow asynchronous.
The order service uses Node.js + Express, the reason is, JavaScript is quick for building REST APIs and handling JSON payloads, and, the Node works good with messaging libraries. 
In the microservices architecture, the order service is the entry to transaction. It communicates with the store front with HTTP (POST), and then communicates with next services through MQ, send messages to consumers, so next serive can process orders without blocking the user.

## Service of Store Front (Vue.js)
As my understaning for the store front, it is a web app which face to customer directly.  It is to provide the UI, so customer can select product, set quantity, so got calculated total price, and then, cusomer can place the order.  Its another function is to handles error messages, for example, if system cannot load product informaiton, it will publish errorr message for notify.
It is built with Vue.js, the reason is, Vue is simple for component-based UI development and reactive state. 
From view of architecture, the store front service is the client layer which engage service together. It communicates with backend services using HTTP requests: it calls the Product Service in order to get  products, and then, call the Order Service to place orders.

## Challenges and Learnings

When I worked on the lab1, one of major challenge I met is to be familiar with the azure environments, such as deploy to Azure Static Web Apps, also to set the environment variables for cloud. And, read log files to figure out the problem.
