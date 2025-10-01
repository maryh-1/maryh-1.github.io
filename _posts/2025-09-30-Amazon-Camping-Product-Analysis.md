---
title:  "Amazon Camping & Hiking Products Analysis"
mathjax: true
layout: post
categories: media
---

## Overview

This project aims to extract insights about products sold on Amazon using publicly available data found in Amazon product listings. Due to the immense amount of products available on Amazon, I narrowed down the project to focus on Camping & Hiking related products. The goal is to identify characteristics that differentiate best selling products from the rest, which could serve as useful information for Amazon sellers. The process involved scraping the intial datset from Amazon.com, cleaning and preprocessing the scraped data, and finally analyzing it for insights.

### Data Scraping

I used the requests_html libryar in python to scrape the product data. The data was scraped using three different URL's: one found by typing "Camping & Hiking" in to the Amazon search bar, another found by using the drop-down navigation options in Amazon get to Camping & Hiking products, and another which listed only the top one hundred bestselling Camping & Hiking products. I found it necessary to include the last link because regular searches only inlcude a small amount of bestselling products on their results' page, and I wanted to have more bestselling products in the dataset for analysis. The URL found by navigating to Camping & Hiking products included many more pages of results than by searching directly in the search bar, so using two URL's to search for regular products (by regular I mean not bestselling) helped to add more products to the dataset.

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

  {% highlight python linenos %}
  response = session.get(url)
  response.html.render(sleep=2)
  products = response.html.find(parent_selector)
  
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
  {% endhighlight %}
  







