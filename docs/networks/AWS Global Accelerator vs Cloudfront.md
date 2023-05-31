## AWS Global Accelerator

- Move the **AWS network closer** to customers'
- connections **enter at edge** using **anycast** **IPs**
- can be used for non HTTPS (TCP/UDP)
- move AWS network entry point as close as possible to the customer using edge locations while minimizing network hops.
- If you need global **TCP** or **UDP** network optimization.
- Improves performance for a wide range of applications over **TCP** or **UDP**
- Proxying packets at the edge to applications running in one or more AWS Regions.
- Good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT) or voice over IP.

## CloudFront

- Global cache for **static content**
- only caches **HTTP** and **HTTPS** content.
- If you require delivery of **content** or manipulation of that **content**.
- Improves performance for both cacheable content (such as images and videos)
- dynamic content (such as API acceleration and dynamic site delivery)
- content is served at the edge