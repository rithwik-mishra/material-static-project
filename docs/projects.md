# My Personal Projects

## Pastebin / URL Shortener Web App
As part of the COMP 423: Software Engineering Fundamentals class at UNC Chapel Hill, I lead the creation of a Pastebin / URL Shortener style app that would take either text or URLs and create a shortened link that directs users to that content. The Web App was broken into two parts: 

### 1. RESTful API 
The API for the app was created using three layers: services, data models, and HTTP routing. FastAPI was used for our HTTP routing, Pydantic for data models, and services were injected into our api using dependency injection. Next, our API was deployed to the cloud using a CI/CD workflow, PyTest integration and unit testing, and Kubernetes OKD. My deployment can be accessed by clicking [this link](https://ex01-comp590-140-25sp-rmishra.apps.unc.edu/docs)

### 2. Web Application
The Frontend for the  web application was created by using TypeScript, HTML/CSS, CORS, RxJs Observables, and Angular. The web application allows for the user to seamlessly use all the API routes defined to create and manage Pastebin/URL shortened link resources. The Frontend for the web application can be accessed by clicking [this link](https://comp423-25s.github.io/ex02-link-share-rithwik-mishra/#/)


