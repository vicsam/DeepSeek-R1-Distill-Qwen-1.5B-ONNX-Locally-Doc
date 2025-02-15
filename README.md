# DeepSeek-R1-Distill-Qwen-1.5B-ONNX: Running Locally – Issues & Fixes  

This document serves as a personal record of my experience running **DeepSeek-R1-Distill-Qwen-1.5B-ONNX** locally. It includes setup instructions, encountered issues, and their respective solutions.  

## Official Documentation  
Refer to the official repository for additional details: [GitHub - r1-web](https://github.com/sdan/r1-web)  

## Setup  
To get started, ensure the following are installed:  

- **Node.js** (Version: 18.18.0)  
- **npm** (Node Package Manager)  
- **A web browser** with GPU support  

## Challenges  

### 1. Error: A tree hydrated but some attributes of the server-rendered HTML didn’t match the client properties  

This error occurs due to discrepancies between the **server-side rendered (SSR) HTML** and what the client renders during hydration. It is typically caused by:  

- Conditional server/client rendering, e.g., `if (typeof window !== 'undefined')`  
- Dynamic inputs such as `Date.now()` or `Math.random()` that change on each render  
- Date formatting based on the user's locale that differs between the server and client  
- External data that changes between the server and client render but isn't properly passed as a snapshot  
- Invalid HTML tag nesting  

### Fixes  
To resolve this issue:  

- Ensure the **server and client** render the **same initial output**  
- Avoid using **random, time-dependent, or external values** during SSR  
- Use **client-side state (`useEffect`)** for dynamic changes  
- If the issue persists, try running in **incognito mode** or **disabling browser extensions**. Extensions like **Grammarly, ad blockers, or dark mode** extensions often modify the DOM before React hydrates, leading to mismatches.  

