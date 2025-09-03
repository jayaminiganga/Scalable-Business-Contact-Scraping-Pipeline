# Scalable-Business-Contact-Scraping-Pipeline
Scalable Business Contact Scraping Pipeline automates the extraction of business emails from Europages using Selenium and BeautifulSoup. Modular, multilingual, and filters out generic emails to deliver high-quality, verified contacts for lead generation and business intelligence.

# Scalable Web Scraping Pipeline – Wine Producers (Europe)

## Overview
This project implements a pipeline to collect business emails for wine producers in Europe using Europages. 
It extracts company profile URLs, visits websites, finds contact/impressum pages, and collects emails with company name and country.


## Workflow

1. Directory Crawling

    I started from the Europages search page and Used Selenium with headless Chrome to load pages with JavaScript.
    Then, I used BeautifulSoup and regex patterns to extract company profile URLs.
    Handles pagination (currently limited to MAX_PAGES = 5).
    These URLs were saved in a CSV file called links_wine.csv

3. Profile Scraping

    For each company profile, I extracted the company name and country from the profile page.
    I followed the ‘Visit Website’ link to the company’s own website.
    Searches for a contact or impressum page using multilingual keywords.
    On the website, I searched for contact or impressum pages using multilingual keywords like contact, kontakt, contatti, impressum.
    Emails were extracted using regex, with generic emails like info@ or contact@ filtered out.
    The final cleaned dataset was saved in emails_wine.csv.”

5. Email Extraction

    Extracts emails via regex.
    Filters generic emails (info@, contact@, sales@, admin@).
    Deduplicates entries.


## Challenges and Mitigation

| Challenge                             | Mitigation                                                      

Missing Website Links                     Some company profiles do not provide a “Visit Website” link. Fallback to Europages profile page.     
Multi-language Contact Info               Scraper searches for multilingual keywords (contact, kontakt, contatti, impressum). 
Contact Forms Instead of Emails           Only direct emails are extracted; forms are skipped. That is a limitation. Future improvement: parse forms.
Generic Emails                            Filter info@, contact@, sales@, admin@.                         
Website Access Issues                     Sites fail to load or are unreachable. Errors logged; pages skipped. Future: retries/timeouts.        
Slow Loading Pages                        time.sleep() ensures pages load fully before scraping
Language-specific Menus                   Scraper relies on multilingual keywords


## Outputs

- `outputs/links_wine.csv` → Profile URLs.  
- `outputs/emails_wine.csv` → Emails with company name and country.

## Scalability

- The pipeline is modular — by just changing the search query and sector variable, it can work for any other industry.
- It separates crawling from extraction, which makes it reusable

## Insights

- Some companies provide multiple emails; others have missing country info.
- Multi-step scraping (profile → website → contact page) improves email discovery.
- Regex patterns work well for Europages URLs and email extraction.
- The pipeline is reusable for other sectors by changing the START_URL and SECTOR.


## Future Improvements
- Predict emails from company domains using ML/LLMs.  e.g., firstname.lastname@domain.com
- Detect contact pages automatically with ML.  
- Clean and standardize company names and countries.
- Retry logic for failed pages.
- Automating parsing of contact forms for email addresses
