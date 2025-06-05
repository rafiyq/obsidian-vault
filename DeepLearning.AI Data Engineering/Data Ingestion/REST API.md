API mandate originated from Jeff Bezos to all Amazon employees in 2002 addressed a significant problem: prior to its implementation, teams at Amazon (and most other organizations) lacked a consistent and stable method for exchanging data and services, leading to inefficiencies. By establishing APIs as a stable and predictable interfaces between teams, any team could reliably provide data, functionality, and communication to others, regardless of the complexity or internal chaos within their own systems.
![[api_mandate.svg]]
Another key aspect of the API mandate was that these service interfaces had to be designed with the potential to eventually become **public-facing**, accessible to external developers. This shift toward service-oriented architecture laid the groundwork for what would later become **Amazon Web Services (AWS)** and set a global standard for how companies share data and services, both internally and externally.

## What is an API?

An API is a set of rules and specifications that allows you to programmatically communicate and exchange data with an application. *Programmatic communication* means interactions that occur through code. You likely use APIs daily basis—whether you’re searching online, using a mobile app, or making a payment. APIs are embedded in the functionality of a wide range of software applications. 
![[api_application.svg]]

For example:

- Social media apps use APIs to fetch and display data from web servers to users. 
	![[api_social_media.svg]]
- E-commerce platforms rely on APIs to facilitate transactions between websites and payment systems. 
	![[api_payment.svg]]
- Many companies offer **public-facing APIs**, allowing developers to access their data and services and integrate them into their own applications. 
	![[api_data_engineer.svg]]

As a data engineer, you’ll frequently use APIs to connect with and extract data from various sources, such as web services, cloud platforms, or third-party providers. APIs enable you to send requests and receive responses in a standardized format. They also often provide metadata, documentation, authentication, and error-handling features to streamline data extraction.

![[api_sources.svg]]

## REST API

The most common type of API is the **REST API**, where **REST** stands for **Representational State Transfer**. REST APIs use **HTTP (Hypertext Transfer Protocol)** as the basis for communication. Interacting with a REST API is similar to browsing the internet: when you click a link, your browser sends an HTTP request to a server for a specific resource (like a web page), and the server responds by providing that resource. 

![[http_request_server.svg]]

Similarly, with a REST API, you send an HTTP request for a particular resource, and the API responds based on the content of your request.

![[http_request_api.svg]]

## Practical Example

In the conversation with the marketing analysts, we learned that they want to analyze data stored on a third-party platform—**Spotify**—which is accessible via an API. This is a common scenario in data engineering, where the source system you need to extract data from (whether internal or external) is accessible via API.

The best way to understand how API works is to dive in and try it yourself—which is exactly what you’ll do in the next lab.