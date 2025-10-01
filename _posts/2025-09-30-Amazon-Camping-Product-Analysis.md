---
title:  "Amazon Camping & Hiking Products Analysis"
mathjax: true
layout: post
categories: media
---

## Overview

This project aims to extract insights about products sold on Amazon using publicly available data found in Amazon product listings. Due to the immense amount of products available on Amazon, I narrowed down the project to focus on Camping & Hiking related products. The goal is to identify characteristics that differentiate best selling products from the rest, which could serve as useful information for Amazon sellers. The process involved scraping the intial datset from Amazon.com, cleaning and preprocessing the scraped data, and finally analyzing it for insights.

### Data Scraping

I used the requests_html library in python to scrape the product data. The data was scraped using three different URL's: one found by typing "Camping & Hiking" in to the Amazon search bar, another found by using the drop-down navigation options in Amazon get to Camping & Hiking products, and another which listed only the top one hundred bestselling Camping & Hiking products. I found it necessary to include the last link because regular searches only inlcude a small amount of bestselling products on their results' page, and I wanted to have more bestselling products in the dataset for analysis. The URL found by navigating to Camping & Hiking products included many more pages of results than by searching directly in the search bar, so using two URL's to search for regular products (by regular I mean not bestselling) helped to add more products to the dataset.

The data was scraped from the product listings on the search results page rather than individual product pages. The following data was included for all products when available:
* Product Title
* ASIN (a unique identification number for each Amazon product)
* Price
* Star Rating (out of 5 stars)
* Number of Reviews
* Best Seller indicator (for products not found on the best sellers page, this was marked by a "Best Seller" tag in the product image)

Products listed on the best sellers page included a little less information in their listings. The following are data that was collected for products on regular search results pages but not the best sellers list. Because this data was only available for a portion of the dataset, I focused my analysis on the previously listed variables and used the following data variables as supplementary information.
* Number of the product bought in the past month
* Free delivery availability (products listed as having free delivery)
* Coupon availability (products that included a coupon)
* Page Number (this information was technically available for products on the bestsellers page but wasn't as meaningful to collect since the bestsellers page was an ordered list of products from 1 to 100)

Some of the data was extracted using patterns in the product text and the requests_html {% highlight python%}.search(){% endhighlight%} functionality. For example, product star ratings were always written in the form "{rating} out of 5 stars", so this information was easy to extract directly in python before putting the data in a dataframe. Other information like free delivery and coupon availability was extracted from the entire text output in the cleaning and preprocessing stage. Most of the data was extracted from each product listing's text output except for the title and ASIN. The ASIN was not displayed in the product text, so I pulled into from another part of the html. The title was displayed in the product text but due to each title's differing length and verbage, I found it easier to extract the complete title from another part of the html. "Try" and "except" was used to keep the scraper running when a product didn't display certain information, and 'NA' was inserted for unavailable data. 

  {% highlight python linenos %}
  response = session.get(url)
  response.html.render(sleep=2)
  products = response.html.find(parent_selector)

  while page_number < 50:
  
    for product in products:
          product_inf = {}
          try:
              asin = str(product)
              asin = asin[asin.find('amzn1.asin.')+11:]
              asin = asin[:asin.find("'")]
              product_inf['asin'] = asin
          except:
              product_inf['asin'] = 'NA'
          try:
              title = product.find(title_sel)
              title = str(title)
              title = title[title.find('label=')+7:title.find('class=')-2]
              product_inf['title'] = title
          except:
              product_inf['title'] = 'NA'
          try:
              number_bought = str(product.search('{number} bought in past month')['number'])[-4:]
              product_inf['number_bought'] = number_bought
          except:
              product_inf['number_bought'] = 'NA'
          try:
              rating = str(product.search('{number} out of 5 stars')['number'])[-3:]
              product_inf['rating'] = rating
          except:
              product_inf['rating'] = 'NA'
          try:
              number_reviews = str(product.search('aria-label="{number} ratings"')['number'])[-9:]
              product_inf['number_reviews'] = number_reviews
          except:
              product_inf['number_reviews'] = 'NA'
          try:
              product_inf['page_number'] = page_number
              product_inf['text'] = product.text
          except:
              product_inf['text'] = 'NA'
          data.append(product_inf)
      page_number += 1
      url = response.html.next()
  else:
    df = pd.DataFrame(data)
  {% endhighlight %}


## Cleaning and Preprocessing

Cleaning and preprocessing this dataset involved removing excess characters from the html element attached to pieces of the data, creating columns for data extracted from the full product text string, and converting number types from string to integers or floats. The final result of cleaning and preprocessing was two datasets: one dataset with the variables available for all products including products from the best sellers list, and another datset without products from the best sellers list with additional variables like number bought, coupon availability, and free delivery availability. 

The columns for products offering free delivery and coupons were binary 1 and 0 columns. A 1 in the free delivery column meant that free delivery was available, and a 1 in the coupon column meant that a coupon was available. The column indicating if a product was a best seller was also a binary 1 and 0 column, with 1 indicating that the product was a best seller. These features were determined by looking for the terms 'FREE Delivery', 'coupon', and 'Best Seller' in the full product text string.

The price, rating, number of reviews, and number of a product bought in the past month needed to be converted to integer and float values from their original text data types. Additionally, the number bought in the past month was usually written in the format "8k+" for thousands and "300+" for hundreds. Additional chracters like the "k" and "+" needed to be removed, and numbers in the thousands needed to be converted from the "8k" format to "8000" while changing the data type to an integer.

Another column that I added was a column for the number of words in each product title. I did this by splitting the title string into words and counting the number of words. This will be used later to evaluate if products with longer titles including more keywords are more likely to be best sellers.

Lastly, when datasets that were extracted from different URL's were merged, the ASIN was used to removed duplicate products.

Each dataset was stored as a pandas dataframe. The original, non-cleaned datasets of scraped data were retained as backups, and cleaned datasets were stored as new dataframes. A snippet of each cleaned and preprocessed dataframe can be seen below.



## Analysis



  







