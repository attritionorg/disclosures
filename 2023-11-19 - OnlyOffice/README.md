# Only Office - Two Server-side Request Forgery (SSRF)

## Description
While monitoring web server logs, I caught over a dozen requests from a server at the Institute for Application Security at Technische Universität Braunschweig, Germany. Their client info provides a link to a server that gives a bit more information. What it doesn't say is that they are scanning for several zero-day vulnerabilities, as best I could tell. Some of the requests were too vague to track down, some were clean matches in software and have since been disclosed. Others seem to be in online services, which was odd.

The two in question are for an OnlyOffice product, as noted in the URI they requested. Two server-side request forgery (SSRF) flaws, one in 'file.php' and the other 'test.php', both with the 'path' parameter affected.
```
plutus.ias.cs.tu-bs.de (134.169.32.26) - - [09/Aug/2022:19:01:34 -0400] "GET /OnlyOffice/file.php?path=https%3A%2F%2F721a8843-8b12-413c-9e5a-bddb188f8cf3.surf.ias-lab.de HTTP/1.1" 404 741 "surf.ias-lab.de" "scalaj-http/2.4.2"
plutus.ias.cs.tu-bs.de (134.169.32.26) - - [09/Aug/2022:19:01:34 -0400] "GET /OnlyOffice/test.php?path=https%3A%2F%2F2dbbb279-b377-46a3-8317-e1ad69ef63dd.surf.ias-lab.de HTTP/1.1" 404 806 "surf.ias-lab.de" "scalaj-http/2.4.2"
```

## Solution
Unknown, vendor did not provide fixing information.

## References
Vendor: https://www.onlyoffice.com/
VulnDB: 14462 
CVE: n/a

## Products
Unknown. There are several on-prem OnlyOffice products, and vendor would not confirm which one is impacted.

## Creditee
Unknown

## CVSS
CVSSv3.1 (AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:N/E:F/RL:U/RC:R)
CVSSv2 (AV:N/AC:L/Au:N/C:N/I:P/A:N/E:POC/RL:U/RC:C)

## Disposition
Despite being a zero-day, of sorts, there isn't enough actionable information to go on. That means this does not warrant a CVE ID nor a unique entry in any vulnerability database, else they are padding their statistics.

This is being disclosed in the hopes that someone will have additional information, can test the exploits on their system to verify, and disclose more details.

## Timeline:
2022-10-10 - Initial disclosure to vendor (security@onlyoffice.com)
2022-11-11 - Follow-up ping to vendor
2022-12-04 - Follow-up ping to vendor
2022-12-06 - Vendor ack, "We are aware of the most ssrf issues and have plans to fix them as soon as possible." and "If you'd like, we are ready to send you an invite to the private program on Hackerone where you will be able to work together with others."
2022-12-06 - Asked for rough ETA on resolution
2023-02-25 - Follow-up ping to vendor
2023-05-23 - Follow-up ping to vendor
2023-10-26 - Follow-up ping to vendor, indicate plan to disclose soon
2023-11-19 - Public disclosure
