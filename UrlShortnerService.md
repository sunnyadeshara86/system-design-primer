# URL Shortner Service

## What is a URL Shortner?

A URL shortener is a tool that takes a long web address (URL) and converts it into a much shorter, more manageable link. This is especially useful for sharing links on platforms with character limits, for creating cleaner and more user-friendly links, or for tracking and analyzing link performance.

Popular URL shorteners include Bitly, TinyURL, and Google's former URL shortener, goo.gl. Some of these services also offer features like link tracking, custom short links, and analytics.

## Role of URL Shortner in Digital Communication

In digital communication, a URL shortener plays several important roles:

* Space Efficiency: Shortened URLs save space, which is crucial on platforms with character limits, like Twitter. This allows users to share links without using up too many characters.
* Aesthetic Appeal: Short URLs are cleaner and more visually appealing. They look less intimidating and are easier to read, which can improve user engagement and click-through rates.
* Tracking and Analytics: Many URL shorteners provide analytics and tracking features. This means users can see how many times a link was clicked, where the clicks are coming from, and other data, which is valuable for measuring the effectiveness of campaigns or understanding audience behavior.
* Link Management: URL shorteners often allow users to manage their links, including editing or updating them after they’ve been created. Some services also offer custom short links, which can be branded or more relevant to the content.
* Avoiding Broken Links: Long URLs can sometimes break when shared in email or on social media, especially if they contain special characters or are not properly formatted. Short URLs are less likely to experience these issues.
* Improved User Experience: Short URLs can make it easier for users to share links verbally or in printed materials. They are simpler to type and remember, which can enhance the overall user experience.
* Enhanced Security: Some URL shorteners offer additional features such as password protection or expiration dates for links, adding an extra layer of security.

Overall, URL shorteners contribute to more efficient, user-friendly, and trackable digital communication.

## Designing a URL Shortner Service

The design of a URL shortener may seem straightforward at first glance, but beneath its seemingly simple facade lies a lot of complexities waiting to be unraveled. From choosing the right algorithms to ensure link uniqueness and stability, to crafting user interfaces that are intuitive and accessible, designing a URL shortener demands a multifaceted approach.

This casestudy aims to delve deep into the intricacies of designing URL shorteners, understanding the functional and non-functional requirements, and exploring the challenges and considerations that developers and designers face in creating these indispensable tools. We’ll examine the technical foundations that underpin URL shorteners, from URL parsing and hashing algorithms to database management and error handling.

This case study covers following topics:

* Real-world use cases
* Functional requirements
* Non-functional requirements
* APIs
* Estimates and calculations
* System design
* Requirements verification

### Real-world use cases

Before we start designing the URL shortener system, let’s take a look at some of the real-world use cases where URL shorteners play a crucial role:
* Social Media Sharing
  * Limited character count: There may be limits to the number of characters in a post, which makes it challenging to share longer URLs
  * Trackable links: Brands and influencers use shortened URLs to track click-through rates and engagement metrics
* Affiliate marketing
  * Track clicks: Affiliate marketers use shortened URLs to track the performance of their campaigns by monitoring click-through rates
  * Cleaner presentation: Shortened URLs make promotional content look cleaner and more professional
* Email marketing
  * Improved user experience: Long URLs can clutter email content, making it less appealing and harder to read
  * Track engagement: Shortened URLs help marketers track which links recipients are clicking on and gauge the effectiveness of email campaigns
* QR codes
  * Reduced complexity: QR codes containing shorter URLs are simpler and quicker to scan
  * Trackable: Businesses can track the number of scans to measure the success of QR code-based campaigns
* Print media and offline marketing
  * Memorable links: Short URLs are easier for consumers to remember and type
  * Track engagement: Similar to other marketing channels, shortened URLs help measure the effectiveness of print media campaigns
* Internal links
  * Ease of sharing: Employees can share internal resources using shortened URLs, making collaboration more efficient
  * Track usage: Organizations can monitor the usage of internal resources and identify popular content
* Mobile applications
  * Improved user experience: Shortened URLs can be more easily displayed within mobile apps without affecting the layout
  * Dynamic linking: Mobile apps use short URLs to deep-link to specific content within the app or direct users to the app store
* Customization and branding
  * Branded links: Companies can use custom domains to create branded short links, enhancing brand visibility and trust
  * Consistent branding: Custom short URLs maintain brand consistency across different marketing channels

By providing a more accessible, trackable, and user-friendly way to share and manage links, URL shorteners have become indispensable tools for marketers, businesses, and everyday internet users alike.

Now Let's understand how to design a URL Shortner Service. We will first brainstorm and document the functional and non-functional requirements.

### Functional Requirements

Below is a list of core requirements:
* Given a long URL, return a short URL
* Given the short URL, return the original long URL
* Short URLs should be unique and the length of the URL should have some cap
* Validate incoming long URL
* Support custom URLs
* Expiry of the short URL: 6 months based on the last usage
* Graceful handling
* The creator should be able to make changes to the long URL
* Deleting the URL mapping
* Support analytics and monitoring
* User account management

### Non-functional requirements

Below is a list of non-functional requirements:
* Availability: The system should be highly available
* Scalability: The system should be highly scalable (100 M users) and be able to tolerate request spikes
* Latency: The read and write requests should have very low latency
* Consistency:
  * Two users trying to access the long URL given a short URL should return the same long URL
  * Two users trying to create a short URL for the same long URL should get the same URL
  * One user created a short URL for a long URL and trying to create a short URL again for the same long URL should get the same short URL
* Durability: Once a short URL is created, we need to ensure that the data is never lost
* Reliability: The system should behave correctly and deliver the functional requirements even in case of failures, request spikes, and other outages

### API Design

The following APIs would be needed to support the core functional requirements of shortened URLs:
* POST/shorturl: Creates a new short URL given a long URL
  * Request body: The long URL
  * Response: The short URL
* GET/shorturls/{shorturl}: Returns the long URL corresponding to the short URL
  *  Response: The long URL
  * String getLongUrl(shortUrl)

### Estimates and Calculations

For calculations, let’s start by asking some questions:
* What characters can we use for short URLs? Our options are as follows:
  * a-z, A-Z, 0-9. So, it’s 62 characters.
  * If you want to use more characters, -, ., _, and ~, so, there’s a total of 66 characters.
  * Let’s stick to just 62 characters.
* What’s the scale we are operating at? Let’s make some assumptions here:
  * We have 1 B users.
  * About 10% create short URLs (100 M users).
  * Each user creates 1 URL per day, so 100 M URLs per day.
  * We store these URLs for 10 years. So, 100 M * 1 * 365 * 10 = 365 B URLs.
* How many characters would we have in the short URL? Now, to have 365 B unique URLs, how many characters do we need to create unique URLs? Let’s see:
  * The number of URLs if we use 6 characters is 62^6 = 56 B URLs, but our requirement is to have 365 B URLs. So, we need to use more characters.
  * If we use 7 characters, we have 62^7 = 3.5 T.
* How much storage do we need? Let’s see:
  * We have 365 B URLs. These are the columns we need to store for this system to work:
    * short URL (20 bytes)
    * long URL (1,000 bytes)
    * created_at (10 bytes)
    * updated_al (10 bytes)
    * created_by (20 bytes)
  * So, overall, the number of bytes would be 1,060. Let’s round it off to 1,500 bytes.
  * So, the data we would store for each URL is 365 B* 1500 bytes ~= 500 TB.
  * If we use a replication factor of 3, then we would need 1.5 PB of storage.
* What’s the read and write RPS? Let’s see:
  * Write RPS: 100 M requests per day = 100 M requests per day/(86,400 seconds/day) =~ 100 M/ 100,000 (approximating 86,400 to 100,000) requests per second = 1000 RPS
  * Read RPS: 100 x write RPS = 100 k RPS

#### Options of characters that We can use for short URLs are as follows:

* a-z, A-Z, 0-9. So, it’s 62 characters.
* If you want to use more characters, -, ., _, and ~, so, there’s a total of 66 characters.
* Let’s stick to just 62 characters.

#### Assumptions regarding scale at which We can operate:

* We have 1 B users.
* About 10% create short URLs (100 M users).
* Each user creates 1 URL per day, so 100 M URLs per day.
* We store these URLs for 10 years. So, 100 M * 1 * 365 * 10 = 365 B URLs.

#### Total characters needed to create Short URLS based on above assumptions

* The number of URLs if we use 6 characters is 62^6 = 56 B URLs, but our requirement is to have 365 B URLs. So, we need to use more characters.
* If we use 7 characters, we have 62^7 = 3.5 T.

### Storage needed to store the Short URLs

* We need to store following columns:
  * short URL (20 bytes)
  * long URL (1,000 bytes)
  * created_at (10 bytes)
  * updated_at (10 bytes)
  * created_by (20 bytes)
* So, overall, the number of bytes would be 1,060. Let’s round it off to 1,500 bytes.
* So, the data we would store for all the URLs is 365 B* 1500 bytes ~= 500 TB.
* If we use a replication factor of 3, then we would need 1.5 PB of storage.

#### Calculation for read and write RPS

* Write RPS: 100 M requests per day = 100 M requests per day/(86,400 seconds/day) =~ 100 M/ 100,000 (approximating 86,400 to 100,000) requests per second = 1000 RPS
* Read RPS: 100 x write RPS = 100 k RPS

Based on the preceding calculations, we definitely need multiple servers to support high read and write RPS. We also found out that we would need seven characters to be able to support the scale of URLs.

## System Design

In this section, we will explore solution options, bottlenecks, problems, mitigations, and high-level architecture diagrams. First, let’s start with identifying what the core challenge here is.

### Core Challenge

The core challenge in this design problem is as follows: how do we generate unique URLs? There can be various solutions. Let’s explore one at a time and see what are the pros and cons of each one and let’s arrive at the most suitable one.

#### Option A – generate a random URL

Given a long URL, generate a random short URL and check whether it exists in the database (DB). If it exists, then generate another random URL and keep doing it until we find that the entry doesn’t exist. If it doesn’t exist, then store this new entry in the DB as a key-value pair: {short_url -> long_url}.

There are a few problems with this approach:

* As you can see, there has to be at least one check done against the DB to find whether the entry already exists, but in some cases, it may multiply back and forth, generating a random URL and checking against the DB. This increases unpredictable delays and adds latency to the write requests.
* The other problem with this approach is that there may be collisions due to concurrency. Imagine a scenario where there are two requests trying to put the short URL at the same time. So, there are two requests, one for long_url1 and another for long_url2 and, coincidentally, the shortened URLs are the same for both the long URLs. Write for long_url1 may win and long_url2 may get corrupted. Here is the flow to understand this collision and corruption:
  * Both the short URLs generated for long_url1 and long_url2 are the same short_url1. So, we have long_url1 → short_url1, long_url2 → short_url1.
  * Now, the request for long_url1 goes to check whether the short_url1 in the DB is present or not. It is absent, but in the meantime, the request for long_url2 also finds out that short_url1 is absent, so it writes as an entry: {short_url1 → long_url2}.
  * Now, long_url1 → short_url1 comes and overrides it and the entry becomes {short_url1 → long_url2}. So, long_url2 is corrupted and lost.

How can We avoid the corruption?

* It can be avoided by using the putIfAbsent kind of functionality, but not all DBs support this.
* The other way to avoid this corruption is after writing, to do a getLongUrl(short_url) read call and check whether long_url is the one that the request was for. This can make sure it’s not corrupted. It may take a few checks sometimes to be successful, and also, for every put, you are at least doing one get.

Conclusion: This option does not seem to be ideal to be deployed in production.

#### Option B - Pre-generate a pool of random strings and use them

Instead of generating short URL from long URL in Option 1, A pool of short URL can be generated and stored in a database and requests for shortening URLs can be catered by picking a pre-generated random string and marking it as used so that the same value is not used again.

Conclusion: This option looks much more robust than the previous options and doesn’t have any major drawbacks.

#### Option C - MD5 Hash

Given a long URL, generate its MD5 hash. The MD5 hash is 128 bits, and we need to have 7 bits with 62 base, which translates to 42 bits (base 2), since 62^7 ~= 2^42. We can take 42 bits from the 128-bit MD5 hash and from that, we can create short_url with 7 base 62 characters.

Let's understand advantages and disadvantages with this approach:
* One advantage of this is space saving; if the same URL is requested again, then you don’t duplicate the short URL.
* The problem with this approach is that since we are picking up fewer bits from the 128 bits, the probability of collision will be much higher. The first 42 characters of the MD5 hash of many URLs will be the same.
* If we use more than 42 bits, then the collision probability is lower, but then that increases the number of characters in the short URL, which is not great. Also, unless we use all 128 bits for short URL generation, we can’t completely avoid this collision.

Conclusion: This option does not seem to be ideal to be deployed in production as well.

#### Option D – counters approach

What if we generate a monotonically increasing counter incrementing the previous number by one? Here, a single host keeps generating this unique counter.

The problem with this approach is that this unique ID generator becomes a single point of failure. If this server dies, the whole system fails.

To mitigate this, We can use multiple hosts, but making a counter unique across multiple servers is tough. What if we have the counter as host id (6 bits), time id (32 bits) + 4 bits (incrementing counter)?

Problems with this approach:
* We will have 6 bits reserved for hosts, so we can only have 64 hosts
* The last 4 bits are for the incremental counter, so if the number of requests is more than 16 in a millisecond, then there would be collisions

Conclusion: This option does not seem to be ideal to be deployed in production as well.

#### Option E – distributed counters approach

The idea is to divide the 3.5 T sequence numbers into multiple ranges of 'k' size. Lets say, k is 1 million, thus, for 3.5T, we will have 3.5M such ranges, because each range is 1M itself.

So, we have 3.5 M such ranges, such as the following:

R1 [0-1M),
R2 [1M-2M),
…
R3 [9M-10M),

We can keep this in a highly available server (let’s call it a Range server). We have multiple counter servers talking to this Range Server and asking for a range. A Range Server assigns a range and stores that in the following map. Let’s assume there are 10 counter servers:

R1 [0-1M) → s1
R2 [1M-2M) → s2
…
R10 [9M-10M] → s10

The counter server increments the counter to generate a unique number across all the counter servers. This unique number is now converted into a 7-character string (a-z, A-Z, 0-9) in the following procedure. Our base 62-character set is abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRS TUVWXYZ0123456789.

For example, say the unique number is 9234529445.

Then, we convert this base 10 number to a base 62 number:

9234529445 ÷ 62 = 148907051 remainder 23 → x
148907051 ÷ 62 = 2401748 remainder 39 → N
2401748 ÷ 62 = 38702 remainder 4 → e
38702 ÷ 62 = 624 remainder 14 → o
624 ÷ 62 = 10 remainder 4 → e
10 ÷ 62 = 0 remainder 10 → k

To summarize, the 9234529445 counter number in base 62 is {10, 4, 14, 4, 39, 23}, which, when mapped to the base 62 character set we chose, becomes keoeNx. So, the URL can be written as urlshortener.com/keoeNx.

This design looks good, but there are a few open questions:
* What happens if the range is exhausted by a counter server? This is what happens:When the range is exhausted by a server, it will ask for the next range from the Range Server.
* What if the counter server crashes? This is what happens:The range is discarded and we lose the entire 1 M range. This may be OK as we have 3.5 M ranges, so just one range getting discarded is not a big deal. Also, given that the counter server failing is not a frequent incident, this may be OK.
* How can we still prevent losing the entire range? Let’s see:We can write to the Range Server periodically, for example, every Nth (let’s say N = 100 or 1000) URL generation, so we can recover from the last entry + N. This way, we just discard only N counters at the maximum per server per failure incident.
* Isn’t Range Server a single point of failure here? Let’s see:Yes, it appears so, but since the Range Server doesn’t have a lot of reads and writes, we can use a highly available, replicated, fault-tolerant service such as ZooKeeper.

Conclusion: This option looks much more robust than the previous options and doesn’t have any major drawbacks.

### Database Selection

If we look at the main data we are storing in this system, the design problem is the short_url -> long_url mapping. This is a key-value pair and an intuitive choice for storing this kind of mapping is Redis. Redis is a fast, highly scalable, durable, and fault-tolerant database.

### High-level solution architecture (Option E)

<image>



