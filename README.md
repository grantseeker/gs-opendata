# Grantseeker | Open Data Project for Global Charity Data
An AWS OpenData Project maintained by Grantseeker, Inc. featuring developer-friendly IRS exempt organization data.

This is a successor to the "first" AWS IRS 990 OpenData project:  
https://registry.opendata.aws/irs990/  
https://github.com/awslabs/open-data-registry/blob/main/datasets/irs990.yaml  
https://github.com/awslabs/open-data-docs/tree/main/docs/irs-990  

# Getting Started

Current Bucket
> gs private bucket --> to migrate to 'pristine' AWS account once approved

Bucket Schema [Proposed]:
~~~sh
    
    README.md
    LICENSE

    # Folder for developers / users
    /dev
        /utils
        /examples
        /api # documentation of associated open API from Grantseeker & any collaborators
    
    # Core 990 data 
    /990
        /index
            /latest.csv
            /<pub_year>.csv
        /xml
            /<object_id>_public.xml
        /pdf
            /<object_id>_public.xml
    
    # Publication 78 Data
    /pub78
        /latest.csv
        /<yyyy-mm-dd>.csv

    # Extract files (from IRS)
    /extracts
        /bmf
            /latest.csv
            /<year_partition_x>.csv

    # Reference schemas
    /schemata
        /990
            /xml
                /<version-number>.json
            /pdf
                / # to add pdf OCR model/schema
~~~   

# Grantseeker Open API 
Grantseeker Opendata resources can be queried like this - for user convenience:  

https://opendata.grantseeker.io/data/<IRS_OBJECT_ID_FROM_INDEX>_public.xml  

https://opendata.grantseeker.io/data/202103219349100800_public.xml  


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
Fluxx Labs, Inc.    |   https://fluxx.io        | [tbd contact]                     | Advisory Council  

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
ProPublica | NonProfit Explorer | https://projects.propublica.org/nonprofits/ | Good open API; XML files require signed url(?); 12mo behind latest IRS publications 
Candid | GuideStar/Search | https://www.guidestar.org/search | IRS data behind register + paywall; good enriched data; but no access to source 990; some stale
Economic Research Institute | 990 Finder | https://www.erieri.com/form990finder | Basic site; 990 data stale @ FY2019 on 2023-06

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

=======
PROPUBLICA DATA NOTES
https://projects.propublica.org/nonprofits/api
