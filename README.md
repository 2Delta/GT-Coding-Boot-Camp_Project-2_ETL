# GT-Coding-Boot-Camp_Project-2_ETL
Project #2: Extract, Transform, Load

GT-Coding-Boot-Camp
GT-VIRT-ATL-DATA-PT-09-2021-U-C-C
Project 02: ETL

Team: Good enough for Government work

David Dam
Louis Cheng
Jae Park


Proposal:

What is the motivation for this project i.e. if you were going to do the analysis, why this topic?

With the scarcity of enthusiast computer parts over the past year, specifically high end desktop GPUs, we would like to scrape prices from major computer hardware retailers' in order to identify when a reasonably priced (not price gouged) RTX 3090 is available for purchase.


Two datasets (csvs, jsons, API, web scraping, etc.)

We will be web scraping 2 different websites (Newegg.com and BesBuy.com) for product availability and pricing.


What database do you plan on using?

MongoDB was chosen as the final result does not require a relational database as it is merely the inventory status and prices.


Extract:

As both websites have fairly robust search functionality, we can search specifically for the RTX 3090 products that we are looking for. In practice, the search query URL can include an option to exclude 'out of stock' items; however, we did not exercise this option for this project as it would limit the number of results returned.

Search function was used to return the appropriate URL for 'GeForce RTX 3090' on the respective websites. The HTML was then scraped in order to identify the title, price, and link to each item listed as well as the date/time that it was scraped.

BestBuy's website would not respond unless a User-Agent was added to the request.


Transform

Not much transformation was necessary as only the relevant data was pulled during scraping. 

The formatting for the price on Newegg did require scraping separate tags and concatenating in order to extract only the price without other text and dropping and thousand separators to allow the price to be converted to float data type for querying later.

The links provided in BestBuy's items' HREF did not have the complete URL listed, and it was necessary to concatenate with their domain name in order to have a complete URL for each link. Dollar signs and thousand separators were dropped to allow the price to be converted to float data type for querying later.


Load
 
 Title, price, link, and timestamp for each item that was scraped from the websites populated dictionaries to be loaded into MongoDB. The database can then be queried to show only results with prices under a specific amount as retailers and scalpers are price gouging due to scarcity, and we are not interested in seeing these overpriced listings.