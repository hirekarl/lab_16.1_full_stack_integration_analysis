# Lab 16.1: Full-Stack Integration Analysis

[Karl Johnson](https://github.com/hirekarl)  
2025-RTT-30  
<time datetime="2025-09-04">2025-09-04</time>  

## Assignment
### Scenario
Your team has been discussing the architecture for your new MERN stack application. While the core technologies are decided, the practical details of how the React client and Express server will communicate are still being debated. Key concerns have been raised about Cross-Origin Resource Sharing (CORS), managing environment variables securely, and choosing the right data-fetching strategy.

Your tech lead has asked you to research these topics and write a brief analysis to help the team make informed decisions. Your goal is to articulate the challenges and propose solutions, demonstrating a solid understanding of full-stack application architecture.

### Instructions
This lab is a reading and viewing exercise. There is no coding involved. Your task is to carefully review the following resources on full-stack application architecture and then answer the reflection questions in a written document.

#### Task 1: Reading & Viewing Assignment
Please review the following resources. They provide a detailed overview of common challenges and solutions when connecting a separate frontend and backend.

- **Article 1**: [Avoiding Cross-Origin Issues While Hosting Full Projects](https://dev.to/arunangshu_das/avoiding-cross-origin-issues-while-hosting-full-projects-1gi8) 
- **Article 2**: [The Ultimate Guide to Setting Up Your Dev Environment for CORS and Live APIs](https://www.wisp.blog/blog/the-ultimate-guide-to-setting-up-your-dev-environment-for-cors-and-live-apis) 
- **Video**: [React Proxy | Easiest Fix to CORS Error](https://youtu.be/N4yUiQiTvwU?feature=shared)

#### Task 2: Written Reflection
After reviewing the materials, answer the following questions in a clear and concise manner. Your total response should be between 300 and 500 words.

##### 1. CORS Explained
In your own words, explain what a CORS error is and why it occurs in a typical MERN stack application with separate client and server repositories. Describe two different strategies a developer could use to resolve CORS issues during local development.
> A Cross-Origin Resource Sharing (CORS) error is an error that occurs when a browser makes an HTTP request to a server that is different from the requesting server, as differentiated by the scheme (http vs https), hostname, or port. CORS is implemented in browsers to restrict script access to resources so malicious scripts run on one site are not allowed to access resources on another.
>
> Developers working on MERN apps in local development will run into CORS issues when a front-end React app and a back-end Express server are running on different ports on `localhost`. Developers can use either a CORS middleware in Express (i.e., `app.use(cors(...))`), which will explicitly whitelist a set of given URLs for cross-origin resource sharing; or by using a proxy, either in the Vite configuration file or in `package.json`, which effectively "tricks" the browser into thinking requests to the resource server are, in fact, being made from the same origin.

##### 2. Environment Management
Why is it considered a bad practice to hardcode API URLs directly into client-side React code? Explain how environment variables (`.env` files) help solve this on both the client (`REACT_APP_...`) and server (`dotenv` package).
> Harcoding API URLs directly into client-side React code is bad practice for several reasons. For one, hard-coding URLs creates headaches for maintenance, as URLs used in development may be different than those used in production; with hard-coded URLs, developers will have to manually switch URLs on deployment, which is very error-prone. For another, client-side code is visible to end users, and any secrets or other sensitive information embedded in these URLs can be exposed to end users who open the source code.
>
> On the server side, the `dotenv` package allows environment variables stored in a `.env` file to be accessed without committing secrets to the Git repo. This prevents sensitive data from being stolen by actors with access to the repo. On the client side, React exposes only environment variables prefixed with `REACT_APP_` to the public. This helps to prevent developers from accidentally exposing secret keys. These client-side variables are used to configure public-facing information, such as the correct API URL for a given environment (i.e., development vs. production), rather than for storing sensitive information.

##### 3. Data Fetching Trade-offs
The lessons covered both the native fetch API and the axios library for making API requests. Based on the resources and your own understanding, describe one key advantage of using axios over fetch for a complex application.
> One key advantage of the axios library over the fetch API is the way in which axios treats any HTTP responses with status codes in the `4xx` or `5xx` range as errors that can be caught and handled in the `catch` block; it also allows developers to differentiate between API and network errors. The fetch API requires developers to manually test for responses that do not have the `200` status code, making for verbose and error-prone requests.
