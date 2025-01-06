
# Instagram Crawler with API (Ruby 爬蟲)

Web scraping Instagram can be tricky due to its constantly changing webpage structures and randomized class names. By leveraging Instagram’s API, you can bypass browser automation issues and achieve efficient and reliable crawling. This guide walks you through the process of analyzing Instagram’s API and creating a functional Instagram crawler in Ruby.

---

## Why Switch to API Crawling?

In a previous article, we discussed [Instagram Crawler with Selenium (Ruby 爬蟲)](https://mgleon08.github.io/blog/2018/11/18/instagram-crawler-with-selenium/1.ins.png). While Selenium provides a way to automate browsers, it comes with certain challenges:
- **Network dependency:** Crawling slows down or fails if the network is unstable.
- **Dynamic webpage structure:** Class names on Instagram are often randomized and may change with every website update, causing crawlers to break.

Switching to an API-based approach resolves these issues by directly accessing structured data without relying on browser interactions.

---

## Step 1: Analyzing Instagram’s API

To begin, navigate to any Instagram profile, for example, [https://www.instagram.com/marvel/](https://www.instagram.com/marvel/). Open your browser's developer tools and observe the network requests. You’ll notice three key API requests, one of which contains the post data we need.

### API Structure
The API response includes a JSON object with a key `edges`, which holds the information for Instagram posts.

#### Key API Parameters:
- **`query_hash` and `variables`:** 
  - `query_hash`: Identifies the API endpoint being accessed.
  - `variables`: A JSON object containing parameters such as `id`, `first`, and `after`.
    - `id`: Likely the `user_id` for identifying the profile.
    - `first`: Determines how many posts to fetch in one request.
    - `after`: A cursor for pagination, corresponding to the `end_cursor` field in the response.

By updating the `end_cursor` parameter with the value returned in the API response, you can iterate through pages of posts.

---

## Step 2: Handling the First API Call

### Where to Find the Initial Cursor?
While subsequent API requests include the `end_cursor` for pagination, the first API call requires manual initialization. This can be found within the webpage’s source code.

Search for `end_cursor` in the page's source (e.g., using `Command + F`), and you’ll find it nested under `window._sharedData`. This data structure provides the parameters required for the initial API request.

---

## Step 3: Fetching the First 12 Posts

Interestingly, the first API request starts from the 13th post. The first 12 posts are directly accessible from `window._sharedData` in the webpage source.

#### Special Cases:
- **Video Posts:** Videos are located under the `og:video` property in the page's metadata.
- **Carousel Posts:** Multiple images in a carousel are found within the `edges` array.

To retrieve post links, extract the `shortcode` parameter from `window._sharedData`. Combine this with the base URL `https://www.instagram.com/p/` to form the full post URL.

---

## Strategies for Data Collection

### General Workflow:
1. Use `window._sharedData` to extract the initial `end_cursor` and data for the first 12 posts.
2. Construct the API URL using the `query_hash` and `variables` parameters.
3. Use the `end_cursor` from the API response for pagination.
4. Retrieve video and carousel posts by accessing individual post URLs and extracting their respective data.

---

## Ruby Gem: Automating the Instagram Crawler

To simplify the crawling process, we’ve packaged the logic into a reusable Ruby gem. This gem automates the process of API analysis, pagination, and data extraction.

### Features:
- Fetch posts, videos, and carousels.
- Automatic handling of pagination.
- User-friendly interface.

### Installation:
You can find the gem here: [instagram-crawler](https://github.com/mgleon08/instagram-crawler)

---

## Conclusion

Switching to an API-based approach for Instagram crawling eliminates common challenges like randomized webpage structures and dependency on browser automation. By analyzing Instagram’s API and leveraging the Ruby gem, you can streamline the process of fetching data for any profile.

---

**Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data.**  
👉 [Start your free trial today!](https://bit.ly/Scraperapi)
