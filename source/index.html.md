---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>AI4Govt 2021</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

This is the documentation of IRS API endpoint.

# Labor rate

## Get All Job Titles



```shell
curl "https://demo.ai4govt.com/api/jobTitle/engineer"
```

This endpoint retrieves all job titles.

> The above command returns JSON structured like this:

```json
[
    "(Mechanical) Engineer Iii",
    "(Systems) Support Engineer",
    "* Engineering Tech I",
    "* Engineering Tech Iv",
    "**Junior Engineering Technician(Sca)",
    ".Net Developer/ Applications Systems Engineer",
    ".Net Developer/Software Engineer",
    ".Net Engineer 2",
    ".Net Production Support Engineer",
    "0039 Software Engineer Iv",
    "0040 Software Engineer Iii",
    "0042 Software Engineer I",
]
```


### HTTP Request

`GET https://demo.ai4govt.com/api/jobTitle/{jobTitle}`



### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
jobTitle | false | keyword of job title. Must be great than 3 characters

## Get Labor Rate

```shell
curl "https://demo.ai4govt.com/api/labor" 
```

> The above command returns JSON structured like this:

```json
{
    "Labors": [
        {
            "JobTitle": "Software Engineer",
            "JobCode": "",
            "NaicsCode": 51913,
            "Company": "FACEBOOK INC.",
            "DefaultPrice": 81.52019230769231,
            "EducationLevel": "",
            "MinimalYearExp": 0,
            "Location": {
                "City": "Menlo Park",
                "County": "SAN MATEO",
                "State": "CA",
                "ZipCode": "94025",
                "Source": ""
            },
            "Price": {
                "HourlyWageMean": 81.52019230769231,
                "AnnualWageMean": 169562,
                "CurrentYearPrice": 0,
                "NextYearPrice": 0,
                "SecondYearPrice": 0,
                "TotalAmountInvoiced": 0,
                "TotalContractHourInvoiced": 0,
                "TotalFullTimeEquivalentFTE": 0
            },
            "DataSource": {
                "Name": "lca"
            },
            "Skills": ""
        },
        {
            "JobTitle": "Software Engineer 3",
            "JobCode": "",
            "NaicsCode": 454110,
            "Company": "eBay Inc.",
            "DefaultPrice": 69.8298076923077,
            "EducationLevel": "",
            "MinimalYearExp": 0,
            "Location": {
                "City": "San Francisco",
                "County": "SAN FRANCISCO",
                "State": "CA",
                "ZipCode": "94105",
                "Source": ""
            },
            "Price": {
                "HourlyWageMean": 69.8298076923077,
                "AnnualWageMean": 145246,
                "CurrentYearPrice": 0,
                "NextYearPrice": 0,
                "SecondYearPrice": 0,
                "TotalAmountInvoiced": 0,
                "TotalContractHourInvoiced": 0,
                "TotalFullTimeEquivalentFTE": 0
            },
            "DataSource": {
                "Name": "lca"
            },
            "Skills": ""
        },
    ],
    "Price": {
        "Min": 20.320192307692306,
        "Max": 115.78990384615386,
        "Mean": 50.863060589250765,
        "Stdev": 12.732518693408466,
        "Median": 46.27019230769231,
        "Wrap": 106.8124272374266,
        "MaxCalc": 201.29
    },
    "Geo": {
      "CA": {
            "Price": {
                "Min": 34.285096153846155,
                "Max": 115.78990384615386,
                "Mean": 62.30504096989966,
                "Stdev": 13.033876963590437,
                "Median": 81.52019230769231,
                "Wrap": 130.8405860367893
            },
            "Row": 230
        }
    }
```

This endpoint retrieves all labor rate match with the search criteria.

### HTTP Request

`GET https://demo.ai4govt.com/api/labor`

### Query Parameters

Parameter | Data Type | Description
--------- | ------- | -----------
dataSource |  String | Value of oes, sca, sci, perm, dba, lca
limit | Integer | Specify max return results
offset | Integer | Result start offset
jobTitle | String | job titles
jobCode | String | OES job code
location | String | location - format: city, state

<aside class="success">
Actual return size is limit * number of data sources
</aside>