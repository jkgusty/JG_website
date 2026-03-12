---
title: "Exploring the World’s Best-Selling Books: Data Acquisition and Analysis"
---

## Introduction

Books have fascinated humans for centuries, serving as windows into different cultures, histories, and ideas. But beyond their cultural and literary value, books also have measurable popularity, reflected in sales numbers that reach millions, or even hundreds of millions, of copies. Studying these best-selling books provides a unique opportunity to understand trends in readership, publishing, and literary tastes over time.  

By scraping and combining data, we can explore how metadata such as author, genre, original language, and page count relate to book popularity. Additionally, the dataset provides practice for data cleaning, scraping, and enrichment techniques which are all critical skills in modern data science.

---

## Motivating Question

The main question driving this project is: **what factors contribute to a book’s widespread success?**  

While a dataset of best-selling books cannot capture every facet of literary success, it can offer interesting insights. For example:  

- Do longer books sell more, or is there an ideal page range for mass-market appeal?  
- Are certain genres more likely to achieve multi-million sales?  
- Does the original language of a book influence its global popularity?  

These questions motivated the creation of a dataset that combines original metadata with information such as page counts from Open Library.

---

## Ethics and Responsible Data Acquisition

Before collecting any data, it was essential to ensure that the project adhered to ethical and legal standards. The Wikipedia pages used for initial data acquisition are freely accessible under **Creative Commons licenses**, allowing users to view and reuse content. All data collection followed **responsible scraping practices**, including:  

- **Limited request rates:** Automated scripts included delays to avoid overwhelming servers.  
- **Use of public APIs:** Open Library’s API was used to fetch page counts, respecting their guidelines and limits.  
- **No private or sensitive data collected:** Only publicly available metadata was used.  

By combining these sources responsibly, the project avoids ethical or legal issues while still providing meaningful data.

---

## Steps to Get Started

If you want to create a similar dataset, here’s a high-level overview of the workflow:  

1. **Identify a reliable data source:** Wikipedia’s “List of best-selling books” provides structured tables for top-selling books.  

2. **Scrape or extract the data:**  
   - The initial data can be copied directly from tables or scraped programmatically using Python libraries like `pandas.read_html()`.  
   - Focus on relevant columns such as **Book**, **Author(s)**, **Original Language**, **First Published**, **Genre**, and **Sales**.  

3. **Clean the raw data:**  
   - Remove references, footnotes, and brackets from sales numbers (e.g., ">200 million[20]" → ">200 million").  
   - Standardize text formats (trimming whitespace, consistent capitalization).  
   - Handle missing values using `NaN`.  

4. **Enrich the data:**  
   - Use Open Library’s API to fetch page counts.  
   - For each book, query the API by title and author, then retrieve the maximum realistic page count from all editions.    
   - This step enhances your dataset and makes it more useful for analysis.  

5. **Save the dataset:**  
   - After cleaning and enrichment, export your final DataFrame to a CSV file.  
   - This makes it easy to share or use in further analysis.

---

## Overview of the Final Dataset

The final dataset, saved as `books_data.csv`, contains **205 rows** (books) and **7 columns**:  

| Column | Description |
|--------|-------------|
| **Book** | Title of the book |
| **Author(s)** | Name(s) of the author(s) |
| **Original Language** | Language in which the book was originally published |
| **First Published** | Year of the first publication |
| **Genre** | Literary genre of the book |
| **Sales** | Approximate number of copies sold (brackets removed) |
| **Pages** | Approximate page count (from Open Library) |

**Data Quality Considerations:**  
- Some page counts remain missing (`NaN`) if Open Library had no editions with valid information.  
- Sales figures are approximate and can vary across sources.  
- No duplicates exist because each row represents a unique book.  
- Textual inconsistencies (e.g., variations in author names) were minimized during cleaning.  

---

## Lessons Learned and Challenges

Working with multiple sources highlights some common data challenges:  

- **Inconsistent or missing data:** Not all books had page counts or complete metadata. Using multiple editions and taking the max page count helped mitigate this.  
- **Data cleaning is critical:** Simple transformations like removing brackets from sales figures or trimming whitespace can dramatically improve usability.  
- **APIs have limits:** Google Books API imposes daily quotas, making Open Library a better alternative for bulk enrichment.  

These lessons are useful for anyone attempting a similar project, as they demonstrate the importance of planning for missing or inconsistent information.

---

## Resources and Links

- Wikipedia article: [List of best-selling books](https://en.wikipedia.org/wiki/List_of_best-selling_books)  
- Open Library API: [https://openlibrary.org/developers/api](https://openlibrary.org/developers/api)  
- Python libraries used: `pandas`, `requests`, `io.StringIO`, `time.sleep` 

**Code Repository:**  
- All code used to create and enrich this dataset is available on GitHub: [data_acquisition_blog](https://github.com/jkgusty/data_acquisition_blog)  

---

## Conclusion

This project demonstrates how publicly available information about books can be combined, cleaned, and enriched to create a usable dataset for statistical analysis. While some data is approximate or incomplete, the dataset provides a strong foundation for exploring questions about book popularity, genres, and publication trends.  

By following the steps outlined here, namely ethical data acquisition, thoughtful cleaning, and API enrichment, others can replicate or expand on this work, exploring similar questions in literature, publishing, or other domains where public datasets exist.  