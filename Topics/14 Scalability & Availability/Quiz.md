![[Pasted image 20240331151130.png]]
![[Screenshot 2024-03-31 at 2.54.14 PM.png]]![[Screenshot 2024-03-31 at 2.54.58 PM.png]]

![[Screenshot 2024-03-31 at 2.55.54 PM.png]]

![[SAA Notes/Topics/15 RDS Aurora + ElastiCache/images/Screenshot 2024-03-31 at 2.56.29 PM.png]]

![[Screenshot 2024-03-31 at 2.57.23 PM.png]]

![[Screenshot 2024-03-31 at 2.57.45 PM.png]]

![[Screenshot 2024-03-31 at 2.58.09 PM.png]]
![[Screenshot 2024-03-31 at 2.58.31 PM.png]]
![[Screenshot 2024-03-31 at 2.58.57 PM.png]]
![[Screenshot 2024-03-31 at 2.59.26 PM.png]]

![[Screenshot 2024-03-31 at 3.00.20 PM.png]]

![[Screenshot 2024-03-31 at 3.00.40 PM.png]]

![[Screenshot 2024-03-31 at 3.01.33 PM.png]]

![[Screenshot 2024-03-31 at 3.02.15 PM.png]]

![[Screenshot 2024-03-31 at 3.02.55 PM.png]]

![[Screenshot 2024-03-31 at 3.03.51 PM.png]]![[Screenshot 2024-03-31 at 3.04.32 PM.png]]

![[Screenshot 2024-03-31 at 3.06.47 PM.png]]

![[Screenshot 2024-03-31 at 3.07.36 PM.png]]

### What is the difference between setting an HTTP to HTTPS redirect at the DNS vs setting it up at the Application Load Balancer ?

Setting up an HTTP to HTTPS redirect at the DNS level versus doing it at the Application Load Balancer (ALB) involves different mechanisms and layers of the network stack. Here's a breakdown of the differences:

1. **DNS-Level Redirect**:
   - At the DNS level, you don't really perform an actual HTTP to HTTPS redirect. DNS, by its nature, resolves domain names to IP addresses and doesn't deal with protocols (HTTP or HTTPS). However, you can use services like AWS Route 53 to configure a sort of redirection by using DNS responses to guide clients to a different hostname.
   - When a user tries to access your site, the DNS service can respond with a URL in an HTTP frame, essentially instructing the client's browser to request a different URL using HTTPS.
   - This method is not a true redirect at the HTTP level; it's more of a workaround and can introduce extra DNS lookups and HTTP request/response cycles, potentially impacting performance.

2. **ALB-Level Redirect**:
   - Setting up an HTTP to HTTPS redirect at the ALB is more direct and efficient. The ALB can inspect the incoming HTTP traffic and, based on rules you set, perform a redirect to HTTPS.
   - This method is protocol-aware, meaning the ALB understands and manipulates HTTP headers and status codes to perform a proper redirect. For example, it can respond to an HTTP request with a 301 (Permanent Redirect) or 302 (Temporary Redirect) status code along with the new location using HTTPS.
   - The redirect at the ALB happens before the traffic reaches your backend servers, offloading them from handling this task and allowing for a centralized redirection strategy that's easier to manage.

**Performance and Security Considerations**:
- **Efficiency**: An ALB-level redirect is typically more efficient since it's a direct response to the HTTP request, avoiding additional DNS lookups or HTTP frames that could introduce latency.
- **Security**: By using an ALB-level redirect, you ensure that encryption is enforced as early as possible in the request path, minimizing the window where data is transmitted in clear text.
- **Scalability**: Redirects at the ALB level can be easily scaled and managed as part of your overall load balancing strategy, providing a centralized point of control.

In most cases, performing the redirect at the ALB is the preferred approach, as it's more aligned with HTTP protocol standards, provides a better performance profile, and offers a more scalable and secure solution. The DNS "redirect" is more of a redirection mechanism and not a true HTTP-to-HTTPS redirect, which could lead to some unexpected behavior or additional latency.