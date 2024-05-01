---
title: "YC Application Sample"
date: 2022-1-22T18:54:38-08:00
description: "How and why I decided to decline a YC interview"
image: "AI-datapipelines.jpg"
tldr: "Example of sample YC App"
---

{{< figure src="AI-datapipelines.jpg">}}

Here is what we applied to YC with.
 
## Describe what your company does in 50 characters or less.

AI Infrastructure to Automate Data Pipelines 

## What is your company going to make? Please describe your product and what it does or will do.

Our product leverages AI to accelerate the custom data engineering work required to clean, unify, model, and transform raw source data from disparate systems like ERPs, CRMs, POSs, into useful datasets for BI, analytics and other downstream purposes. In the long run, our product dynamically monitors and proposes updates to data pipelines based on changes in source data and business context.

## Why did you pick this idea to work on? How do you know people need what you're making?

After speaking to over 30 businesses, we heard their biggest challenge was access to data and analytics. We believe the main bottleneck is in the transformation step of data pipelines: a veteran BI/data expert stated: “the number one unsolved data problem not addressed by any software today is data congruency across systems and within systems.”

Companies spend years and millions of dollars on tools and people building custom data pipelines. Much of this work is spent mapping unique business processes and domain expertise on top of fragmented and ambiguous data from disparate systems. This labor intensive approach is unsustainable.


## Who are your competitors? What do you understand about your business that they don't?

- Legacy providers (ex: Informatica, Talend)
- Modern data incumbents (ex: dbt, Fivetran, Airbyte, Snowflake, Databricks)
- Services companies (ex: Accenture, Capgemini, Palantir)

We looked at the various layers of the analytics/data stack: ingestion, storage, transformation, and visualization. We think the biggest opportunity for AI is in the transformation layer. Data is only as valuable as an organization's ability to productize it.

The key to making the transformation layer more efficient is finding novel ways to extract and document business knowledge and then layer this information on top of raw data in a way that is interpretable by AI to auto-generate the custom data transformations necessary to productize the data for downstream consumers. Most of the above competition solely targets developers only. In order to solve this problem, business users and their domain expertise must be integrated into the workflow.

{{< figure src="ValueProps.png">}}

## How do or will you make money? How much could you make?
 
We will charge a software fee to data and analytics teams looking to accelerate their data stack, employing a value-based pricing scheme that incentivizes connecting more data sources and managing more data pipelines. An alternative business model would be an AI-enabled hybrid services company that competes with IT services firms.

To size the TAM, we estimated the “total cost of ownership” (“TCO”) for an analytics solution that includes tools, compute and labor; we scaled the TCO based on the number of employees. There are over 100,000 enterprises with more than 100 employees (a threshold we’re using to represent when a company might face this data challenge). Using bottom-up assumptions from a Gigaom research report, we assumed that ~30-40% of the TCO is labor, much of which is related to managing data ingestion and transformation. Based on our bottom up analysis, the annual labor associated with data ingestion and transformation for analytics purposes is over $50 bil in the US. Our AI infrastructure aims to dramatically reduce the amount of data engineering labor required in the transformation step and we should be able to take a portion of this market.

## How do users find your product? 

We currently plan to use a direct sales and marketing-led GTM strategy. However, we think there are opportunities to expand our distribution through strategic channels and partnerships. One example would be to partner with data warehouse providers such as Snowflake whose customers would benefit from use of our product since it would increase the value and usability of the stored data. There are several companies at other layers of the data stack that offer similar synergies for customers. 

We could also partner/distribute with IT service consultants who could recommend our product when providing advice on data/analytics. Managed service providers are also a potential customer/partner because they could leverage our product to add value and make their data integration service offering more efficient.




 
