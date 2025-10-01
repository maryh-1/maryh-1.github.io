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

The data was scraped from the product listings on the search results page rather than individual product pages. The following data was included:



