# Grantseeker | Open Data Project for Global Charity Data
An AWS OpenData Project maintained by Grantseeker, Inc. featuring developer-friendly IRS exempt organization data.

This is a successor to the "first" AWS IRS 990 OpenData project:  
https://registry.opendata.aws/irs990/  
https://github.com/awslabs/open-data-registry/blob/main/datasets/irs990.yaml  
https://github.com/awslabs/open-data-docs/tree/main/docs/irs-990  


# Target Users & Product Value Proposition

This project aims to provide the most complete, developer-friendly, and open source of IRS 990 data (and related publications).

Users
Anyone who is interested in building / consuming data for the betterment of US nonprofits and the communities around the world they serve.

Core Product  
[ ] S3 | Public storage bucket of raw, cloud-optimized IRS source data, with 100% fidelity, 48hr latency (from date of irs.gov publication)
    - 990 XML Files
    - 990 PDF legacy files
    - Pub 78 File
    - BMF/SOI Extracts
    - Index Files (source + concatenated)

[ ] API | Open and permissionless API index for all resources in hosted storage

[ ] README | Core documentation and community reference implementations for getting started with the datasets

# Project Stewards
Organization | Website | Representative | Role
:---|---|---|---|
Grantseeker, Inc.   |   https://grantseeker.io  | Nathaniel B. Chase @seekerchase   | Lead Sponsor
Fluxx Labs, Inc.    |   https://fluxx.io        | [tbd contact]                     | Co-Sponsor  

...others welcome!  Please reach out to the team:

`opendata@grantseeker.io`

# Project Timeline

PHASE 0: Trial Period (6mo)

Step 0 (June 2023)
Apply for and recieve AWS sponsorship to standup project.  Complete onboarding and transfer full XML file bucket from GS-S3 to new "pristine" project bucket.

Step 1 (July 2023)
Soft launch / announcement to core members of community, past project users / contributors. Formation of basic project governance, including update cadence, 
team roles / redundancy, and core deliverables.

Step 2 (~by September 2023)
Complete first cycle of data updates and product (data) maintenance cycle.  Solicit 2-5 new or legacy AWS 990 OpenData projects to onboard with project.


# Why?

While the IRS data is free and available for download by anyone, it is not in an easily consumable format for anyone looking to build
software or data projects using it.

- 990 Data is held in two seperate datasets - an XML format (for those filing electronically), and a legacy PDF format that is not fully OCR'd or easily machine readable
- the XML 990s are stored in .zip files and grouped chronologically by year, with multiple and varying numbers of files per year and a non-standard naming system across the years
- Index files are stored in .csv (also downloadable), one for each year. These are not easily queriable, leaving the user to make their own index if they want to identify a filing (e.g. by EIN)
- 990 Schemas vary across year and by filing type (e.g. for 990EZ, 990PF, etc), requiring a variable schema mapping if you want normalized data across years

# Continuation of AWS IRS 990 OpenData Project

This project is a successor project to the original AWS Opendata project described here: 
https://registry.opendata.aws/irs990/

On December 31, 2021, the IRS deprecated its support of the IRS open data, in favor of hosting files solely at irs.gov:
https://www.irs.gov/newsroom/irs-makes-tax-exempt-organization-search-primary-source-to-get-exempt-organization-data

AWS OpenData team listed on their deprecation notice their openness to someone taking on stewardship. On June 14, 2023, @seekerchase and pws@amazon.com 
spoke about Grantseeker, Inc. picking up the stewardship for the prior opendata project.


# Source Data Files

- Publication 78 Data (list of currently eligible organizations), updated ~monthly
    https://apps.irs.gov/pub/epostcard/data-download-pub78.zip

- 990 Data (efile and PDF)
    Form 990 - default form
    Form 990–EZ - under $200k annual & under $500k assets 
    Form 990–PF (501(c)(3) Private Foundations) - private foundations
    Form 990–T (990–T returns for 501(c)(3) organizations only) - unrelated business / trust income
    Form 990-N (e-Postcard) - for sub $50,000 in annual gross receipts

    https://www.irs.gov/charities-non-profits/form-990-series-downloads

- SOI Extract (selected extracted data )
    https://www.irs.gov/statistics/soi-tax-stats-annual-extract-of-tax-exempt-organization-financial-data

- Master File Extract (bulk data extract, including financial information)
    https://www.irs.gov/charities-non-profits/exempt-organizations-business-master-file-extract-eo-bmf

### Related Source Data

- Audit Data for filers with >$750k federal funding (provided by https://facdissem.census.gov/)


# Currently Available 990 Data Sources / Services

There are many wonderful and open projects that have parsed and made available 990 data to the public.  

Below is a summary of the leading ones (please PR more!):

Organization | Project | Website | Notes
:---|:---|:---|:---
ProPublica | GuideStar/Search | https://www.guidestar.org/search | IRS data behind register wall + internal paywall; 990 data stale @ FY2019 on 2023-06
Candid | GuideStar/Search | https://www.guidestar.org/search | IRS data behind register wall + internal paywall; 990 data stale @ FY2019 on 2023-06
Economic Research Institute | 990 Finder | https://www.erieri.com/form990finder | Basic site; 990 data stale @ FY2019 on 2023-06

## Detailed Notes / Observations on Leading Sources:

1. IRS themselves (online GUI):   
    - https://apps.irs.gov/app/eos/
    - Allows single search queries; can be a little finky on UX

2. ProPublica: 
    - Web GUI with clean, data-forward formatting
    - Does hit user with fundraising popup on every visit (probably disuading donations)
    - HAS a free API that is easy to use and well constructed: 
    
        https://projects.propublica.org/nonprofits/api

    - API Limitations [ @TODO: REVIEW / UPDATE PER DETAILED REVIEW ]
        - Some stale-ish data (e.g. annual update cadence around August - allowing for up to 12mo of missing data vs IRS filing)
        - Does [NOT?] include contribution data
        - Some areas of the XML data are not parsed or accessible on the GUI / API (e.g. contributions table)

3. Candid (fmr GuideStar + Foundation Center)
    - Clean and well documented web GUI and API
    - REQUIRES registration (no free / open version)
    - REQUIRES paid subscription to view FREE/OPEN DATA FIELDS:
        - Finanicals
        - Associated persons 
    - Stale data (e.g. 990 Data @ FY2019 on 2023-06)
    - Some odd data presentation -> e.g. their own 990 was PDF'd when it was machine readable XML on propublica (ie easier to copy/parse)
    - Is a 501c3 organization themselves
        - $50MM in Net Assets (2020)
        - $3.4MM in annual Net Income (2020) on $42.8MM in Revenue ($29MM of that being service revenue; balance grants/other) 

    - *Needs to work on openness / mission alignment*


# Reference Projects

There have been a number of interesting and productive data munging projects over the years,
probably more than can be listed here.  A few worth noting:

FROM AWS YAML (https://github.com/awslabs/open-data-registry/blob/main/datasets/irs990.yaml)  

DataAtWork:

Tutorials:
- Title: Tutorial on using the IRS 990 e-file dataset
    URL: https://appliednonprofitresearch.com/posts/2018/06/the-irs-990-e-file-dataset-getting-to-the-chocolatey-center-of-data-deliciousness/
    AuthorName: Applied Nonprofit Research
    AuthorURL: https://www.appliednonprofitresearch.com/

Tools & Applications:
- Title: Parse 990 XML using IRSx
    URL: https://github.com/jsfenfen/990-xml-reader
    AuthorName: Jacob Fenton
    AuthorURL: http://jacobfenton.com/

- Title: aws-irs-990-explorer
    URL: http://irs-990-explorer.chrisgherbert.com
    AuthorName: Chris Herbert
    AuthorURL: http://chrisgherbert.com/

- Title: 990_long
    URL: https://github.com/CharityNavigator/990_long
    AuthorName: Charity Navigator
    AuthorURL: https://www.charitynavigator.org/

- Title: Non Profit Light
    URL: http://nonprofitlight.com
    AuthorName: Non Profit Light

- Title: Guide to Open Data for Nonprofit Research
    URL: https://lecy.github.io/Open-Data-for-Nonprofit-Research/
    AuthorName: lecy
    AuthorURL: https://github.com/lecy

- Title: Nonprofit Explorer
    URL: https://projects.propublica.org/nonprofits/
    AuthorName: ProPublica
    AuthorURL: https://propublica.org

- Title: Open990
    URL: https://www.open990.com/
    AuthorName: 990 Consulting, LLC
    AuthorURL: https://www.990consulting.com/

- Title: Grantmakers.io
    URL: https://www.grantmakers.io
    AuthorName: Chad Kruse
    AuthorURL: https://www.chadkruse.com/

- Title: "npo_classifier: Automated coding using machine-learning and remapping the U.S. nonprofit sector"
    URL: https://github.com/ma-ji/npo_classifier
    AuthorName: Ji Ma
    AuthorURL: https://jima.me/

- Title: Nonprofit Organization NTEE Code Finder & UN SDG Classification
    URL: https://x4i.org/nonprofit-ntee-code-finder
    AuthorName: X4Impact
    AuthorURL: https://x4i.org

# Ideas

[] Source Data Integrity (SDI) - sha1sum checks

...welcome ideas!


=======
PROPUBLICA DATA NOTES
https://projects.propublica.org/nonprofits/api

Get the Data

For those interested in acquiring the original data from the source, here’s where our data comes from:

    Raw filing data. Includes EINs and summary financials as structured data.
    Exempt Organization profiles. Includes organization names, addresses, etc. You can merge this with the raw filing data using EIN numbers.
    Form 990 documents. Prior to 2017, these documents were obtained and processed by Public.Resource.org and ProPublica. Bulk PDF downloads since 2017 are available from the IRS.
    Form 990 documents as XML files. Includes complete filing data (financial details, names of officers, tax schedules, etc.) in machine-readable format. Only available for electronically filed documents. Electronic data released prior to October 2021 is also available through Amazon Web Services.
    Audits. PDFs of single or program-specific audits for nonprofit organizations that spent $750,000 or more in Federal grant money in a single fiscal year. Available for fiscal year 2015 and later.