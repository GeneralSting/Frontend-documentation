# Search Engine Optmization, SEO

## optimizaiton

- whether the word is in the title of the page
- whether the word is in the title of the text
- whether the links to that page contain the specified word
- whether the typed word is among the keywords of the page which is entered by the author,
  but visitors to the site usually do not see it (the so-called meta tags)
- whether that word is in the page address
- number of links to his page and content and the relevance of the pages on which these links are located
  - It is especially important that the text on the links has to do with the content of the linked page,
    and even better that it contains typical keywords that potential visitors might search
- WordPress Yoast SEO

### CTR

- click-through rate
- higher is better
- defines how likely a user is to click on your link dispalyed on Search Engine Ranking Page - SERP
  - relevent title and description

### bounce

- relates to the percentage of single-engagement visits to your site
- lower is better
- Google Analytics tracks the number of people who visit your page and leave without viewing other pages on your site

### dwell time

- time client spend on your page before going back to the search results
- longer the better

### session duration/pages per session

- best possible situation -> client clicks on your page and never leaves it

### can be used by search engine and screen readers for those with disabilities:

- alt attribute on image (img) tag
- aria attribute-> Accessible Rich Internet Application
- title tag
- meta tags
  - featured image
  - author
  - canonical url
  - description
  - social network links

### load content fast:

#### client-side rendering:

- problem: single page application -> dynamic web sites

1. build pages in advance
2. cache on CDN

- so the first thing client sees is fully rendered content (html) then javascript loads after that

#### server-side rendering:

- problem: less efficient
- render on demand
- fresh content

#### ISR

- Incremental Static Regeneration
  - next.js
  1. build pages in advance
  2. cache on CDN
  3. fly continously
  - dynamic pages gets performance benefits of static page (client-side rendering)
  - pages contains fresh data (server-side rendering)
  - still there are some other problems

#### Hybrid rendering

- Angular, next.js
