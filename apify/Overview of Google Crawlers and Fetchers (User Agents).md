# Overview of Google Crawlers and Fetchers (User Agents)

Google utilizes various **crawlers** and **fetchers** to support its products, performing automated tasks or triggered actions based on user requests. These tools are crucial for discovering and scanning websites, whether to improve Google Search or facilitate other services.

This article provides an in-depth look into the technical properties, supported protocols, and best practices for handling Google’s crawlers and fetchers.

---

## What Are Google Crawlers and Fetchers?

### Crawlers
A **crawler** (also referred to as a "robot" or "spider") is a program that automatically discovers and scans websites. These are vital for ensuring Google can index the web effectively. Examples include [Googlebot](https://developers.google.com/search/docs/crawling-indexing/googlebot).

### Fetchers
A **fetcher** acts more like a tool that makes a single request on behalf of a user. Fetchers are part of Google tools and product functions where the end user triggers a fetch, such as the [Google Site Verifier](https://support.google.com/webmasters/answer/9008080).

### Categories of Google Clients:
1. **[Common Crawlers](https://developers.google.com/search/docs/crawling-indexing/google-common-crawlers)**  
   Used across various Google products, these respect robots.txt rules for automated crawls.
   
2. **[Special-Case Crawlers](https://developers.google.com/search/docs/crawling-indexing/google-special-case-crawlers)**  
   Designed for specific Google products, these crawlers operate with agreements between Google and website owners. For example, `AdsBot` may bypass global robots.txt rules under certain conditions.

3. **[User-Triggered Fetchers](https://developers.google.com/search/docs/crawling-indexing/google-user-triggered-fetchers)**  
   These fetchers are activated by users, such as verifying site ownership or testing how Google fetches a URL.

---

## Technical Properties of Google Crawlers and Fetchers

### Distributed Infrastructure
Google’s crawlers operate across thousands of machines and multiple datacenters worldwide. This setup ensures high performance and scalability as the web grows. For optimal bandwidth usage, requests often originate from IP addresses near the targeted websites.

> **Note:**  
> If a website blocks US-based IP addresses, Google may crawl from IPs located in other countries.

---

### Supported Transfer Protocols
Google crawlers support the following protocols:
- **HTTP/1.1** (default protocol)
- **HTTP/2** (offers improved performance but no ranking boost in Google Search)

You can block HTTP/2 crawling by configuring your server to respond with a `421` status code or by contacting Google’s Crawling Team.

Additional protocol support includes:
- **FTP** and **FTPS**, though these are rarely used for crawling.

---

### Supported Content Encodings
Google supports the following content compressions:
- **Gzip**
- **Deflate**
- **Brotli (br)**

These encodings are advertised in the `Accept-Encoding` header of Google’s requests, such as `Accept-Encoding: gzip, deflate, br`.

---

### Crawl Rate and Host Load
Google aims to balance crawling as many pages as possible without overwhelming your server. If your site struggles to handle the requests:
- Use Google’s [crawl rate settings](https://developers.google.com/search/docs/crawling-indexing/reduce-crawl-rate) to reduce activity.
- Avoid sending inappropriate HTTP response codes, as these may affect how your site appears in Google Search.

---

### HTTP Caching
Google's crawling infrastructure supports:
- **ETag** and **If-None-Match** headers (recommended for avoiding date format issues).
- **Last-Modified** and **If-Modified-Since** headers with standard HTTP date formatting (e.g., `Fri, 4 Sep 1998 19:15:56 GMT`).

> **Tip:**  
> Use both `ETag` and `Last-Modified` headers, as they benefit other tools like CMS platforms.

For optimal results:
- Consider using `max-age` in the `Cache-Control` header to specify when content should be re-crawled (e.g., `Cache-Control: max-age=94043`).

---

## Verifying Google’s Crawlers and Fetchers

Google’s crawlers can be verified using:
1. The HTTP `User-Agent` request header.
2. The source IP address of the request.
3. The reverse DNS hostname of the source IP.

Learn more about verifying Google crawlers [here](https://developers.google.com/search/docs/crawling-indexing/verifying-googlebot).

---

## Advertising Content

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more.  
👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

## Best Practices for Handling Google Crawlers

- **Optimize Server Performance:** Ensure your server can handle increased crawl activity during peak times.
- **Use Robots.txt:** Configure robots.txt rules to specify which parts of your site Google should or shouldn’t crawl.
- **Monitor Logs:** Keep an eye on your server logs to detect crawling issues or unusual activity.
- **Avoid Blocking IPs:** Blocking Google’s IP addresses may hinder your site’s visibility in Search.

---

By understanding how Google’s crawlers and fetchers work, you can optimize your site to ensure smooth indexing while maintaining server performance.
