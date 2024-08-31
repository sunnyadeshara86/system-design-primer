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
Durability: Once a short URL is created, we need to ensure that the data is never lost
Reliability: The system should behave correctly and deliver the functional requirements even in case of failures, request spikes, and other outages


