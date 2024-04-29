# NextJS Open Redirect Functionality

## Description

On April 17, 2024, I caught a request to my web server to the /_next/image endpoint, which is not something we use. Based on a Google search, I determined this was likely a request for a [component / endpoint of NextJS](https://nextjs.org/docs/pages/api-reference/components/image). I reached out to Vercel, the vendor, to report what appears to be an open redirect weakness:

```
big.data (45.77.151.195) - - [17/Apr/2024:11:16:45 -0600] "GET /_next/image?url=https://attrition.org.l3v.ru/xxx&w=32&q=75 HTTP/1.1" 404 741 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:103.0) Gecko/20100101 Firefox/103.0"
```

The vendor promptly replied the next morning and asked a few questions. Within a few days and several emails, they confirmed that the functionality is present in NextJS, but it is **intended**. Here are the relevant quotes from the vendor, slightly re-ordered, to include everything and demonstrate that this is not a vulnerability in their eyes:

*The functionality of being able to pass in external URLs to next/image is intended - the feature allows images to be retrieved from remote sources (such as CDNs).
The feature simply retrieve remote images, it is not intended to perform any manner of redirection. Domains must also be configured in next.config.js to be reachable by next/image so this will not work "out of the box" with any arbitrary domain.
The documentation states that you must allowlist the external URL in your next.config.js file.
We have no reason to believe that there is a security vulnerability in this feature based on the evidence you have provided and the mitigating controls I've mentioned above.*

I'm sharing this here for administrators who see similar requests in their logs, so they can more quickly determine the issue.
