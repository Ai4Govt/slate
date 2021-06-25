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
--------- | --------- | -----------
dataSource |  Array of String | oes, sca, sci, perm, dba, lca
limit | Integer | Specify max return results
offset | Integer | Result start offset
jobTitle | String | job titles
jobCode | String | OES job code
location | String | format: city, state. Example: Ann Arbor, MI
rateType | String | "wrap" or "unburdened". Default value is "wrap"

### Sample Request in Curl
`curl https://demo.ai4govt.com/api/labor?dataSource=perm&dataSource=lca&dataSource=calc&limit=10&jobTitle=solar&location=Ann Arbor, MI&rateType=wrap`


### Response Model
Field name | Data Type | Description
-----------|---------- | -----------
Labors| array of Labor rate model | returns null if no labor rate is found
Price | Price model | return with value in 0 if no labor rate is found
Geo | Map: key is string, value is Geo model | return null if no labor rate is found
Count | Long | return 0 if no labor rate is found
Related| Related model | ommitted if labor rate is found


### Labor rate model
Field name | Data Type
-----------|----------
JobTitle | string
JobCode | string
NaicsCode | int 
Company | string
DefaultPrice | float64
LastRevisionDate | string like 2020-05-09T17:00:00-07:00
EducationLevel  | string 
MinimalYearExp |   int
Location |   Location model
Price |  Price model
DataSource | DataSource model
Skills | string


### Price model
Field name | Data Type
-----------|----------
HourlyWageMean | float64
AnnualWageMean | float64
CurrentYearPrice | float64
NextYearPrice  | float64
SecondYearPrice | float64
TotalAmountInvoiced | float64
TotalContractHourInvoiced  | float64
TotalFullTimeEquivalentFTE | float64



### Location model
Field name | Data Type
-----------|----------
City  | string
County | string
State | string
ZipCode | string
Source  | string


### DataSource model
Field name | Data Type
-----------|----------
Name| string


### Geo model
Field name | Data Type
-----------|----------
Price | Geo price model (not the same as price model)
Row  | int

### Geo price model
Field name | Data Type
-----------|----------
Min  | float64
Max  | float64
Mean | float64
Stdev | float64
Median | float64
Wrap | float64
MaxCalc | float64
Multiplier | float32


### Related model
Field name | Data Type
-----------|----------
Area | string
Count | long


<aside class="success">
Actual return size is limit * number of data sources
</aside>


## Upload IGCE spreadsheet

<aside class="success">
The spreadsheet is in Excel 97-2003 binary format (.xls)
</aside>

### HTTP Request
`curl -F "file=@igce1.xls" http://localhost:8080/api/igce/upload`


> Sample response

```json
[
    {
        "Occupation": "Software Engineer",
        "Records": 436,
        "Code": "",
        "Location": "",
        "Sources": [
            {
                "Name": "perm"
            }
        ],
        "Rate": 30.289903846153845,
        "WrapRate": 63.60879518825274,
        "WrapRateMultiplier": 2.1,
        "MaxCALC": 201.29,
        "Quantity": 120,
        "Base": 0,
        "YearlyRate": null
    },
    {
        "Occupation": "Accountant",
        "Records": 2844,
        "Code": "",
        "Location": "",
        "Sources": [
            {
                "Name": "oes"
            },
            {
                "Name": "perm"
            }
        ],
        "Rate": 25.89,
        "WrapRate": 54.36899753093719,
        "WrapRateMultiplier": 2.1,
        "MaxCALC": 108.24,
        "Quantity": 20,
        "Base": 0,
        "YearlyRate": null
    },
    {
        "Occupation": "Project Manager",
        "Records": 1408,
        "Code": "",
        "Location": "",
        "Sources": [
            {
                "Name": "perm"
            }
        ],
        "Rate": 45.7,
        "WrapRate": 95.96999564170838,
        "WrapRateMultiplier": 2.1,
        "MaxCALC": 1069.1,
        "Quantity": 80,
        "Base": 0,
        "YearlyRate": null
    }
]
```


## Upload Vendor Proposal spreadsheet

<aside class="success">
The spreadsheet is in Microsoft Excel Open XML Spreadsheet (XLSX) format
</aside>

### HTTP Request
`curl -F "file=@use_case_3.xlsx" http://localhost:8080/api/vendorSheet/upload`


> Sample response

```json
[
    {
        "Vendor": "BRASCO DATA INTEGRATION SERVICES ",
        "Period": "12 month Base + 6 month Option",
        "ContractType": "Firm Fixed Price",
        "Location": "California",
        "Base": {
            "LaborCategory": [
                {
                    "Title": "Project Manager",
                    "Rate": 120,
                    "Hours": 1000,
                    "Employees": 1,
                    "Total": 120000,
                    "BelowMinRate": false
                },
                {
                    "Title": "Database Administrator",
                    "Rate": 122,
                    "Hours": 1920,
                    "Employees": 2,
                    "Total": 468480,
                    "BelowMinRate": false
                },
                {
                    "Title": "Data Architect",
                    "Rate": 98,
                    "Hours": 1920,
                    "Employees": 1,
                    "Total": 188160,
                    "BelowMinRate": false
                },
                {
                    "Title": "Electrician",
                    "Rate": 10,
                    "Hours": 1920,
                    "Employees": 1,
                    "Total": 19200,
                    "BelowMinRate": true,
                    "MinRate": 78
                }
            ],
            "Subcontractor": [
                {
                    "Title": "Business Systems Analyst",
                    "Rate": 100,
                    "Hours": 1500,
                    "Employees": 1,
                    "Total": 150000,
                    "BelowMinRate": false
                },
                {
                    "Title": "Share Point Developer",
                    "Rate": 80,
                    "Hours": 1000,
                    "Employees": 1,
                    "Total": 80000,
                    "BelowMinRate": false
                }
            ],
            "Equipment": [
                {
                    "Title": "Laptops ",
                    "Rate": 600,
                    "Quantity": 7,
                    "Total": 4200
                }
            ],
            "Travel": 2000,
            "Total": 1032040
        },
        "Option": {
            "LaborCategory": [
                {
                    "Title": "Project Manager",
                    "Rate": 122.99999999999999,
                    "Hours": 500,
                    "Employees": 1,
                    "Total": 61499.99999999999,
                    "BelowMinRate": false
                },
                {
                    "Title": "Database Administrator",
                    "Rate": 125.04999999999998,
                    "Hours": 960,
                    "Employees": 2,
                    "Total": 240095.99999999997,
                    "BelowMinRate": false
                },
                {
                    "Title": "Data Architect",
                    "Rate": 100.44999999999999,
                    "Hours": 960,
                    "Employees": 1,
                    "Total": 96431.99999999999,
                    "BelowMinRate": false
                },
                {
                    "Title": "Systems Engineer",
                    "Rate": 10.25,
                    "Hours": 960,
                    "Employees": 1,
                    "Total": 9840,
                    "BelowMinRate": false
                }
            ],
            "Subcontractor": [
                {
                    "Title": "Business Systems Analyst",
                    "Rate": 102.49999999999999,
                    "Hours": 750,
                    "Employees": 1,
                    "Total": 76874.99999999999,
                    "BelowMinRate": false
                },
                {
                    "Title": "Share Point Developer",
                    "Rate": 82,
                    "Hours": 500,
                    "Employees": 1,
                    "Total": 41000,
                    "BelowMinRate": false
                }
            ],
            "Travel": 1000,
            "Total": 526743
        },
        "InflationRate": 2.5
    },
    {
        "Vendor": "MONTANA ANALYTICS",
        "Period": "12 month Base + 6 month Option",
        "ContractType": "Firm Fixed Price",
        "Location": "Illinois",
        "Base": {
            "LaborCategory": [
                {
                    "Title": "Senior Project Manager",
                    "Rate": 115,
                    "Hours": 1920,
                    "Employees": 1,
                    "Total": 220800,
                    "BelowMinRate": false
                },
                {
                    "Title": "Data Scientist",
                    "Rate": 125,
                    "Hours": 1500,
                    "Employees": 1,
                    "Total": 187500,
                    "BelowMinRate": false
                },
                {
                    "Title": "Data Analyst",
                    "Rate": 95,
                    "Hours": 1920,
                    "Employees": 2,
                    "Total": 364800,
                    "BelowMinRate": false
                },
                {
                    "Title": "IT Specialist",
                    "Rate": 110,
                    "Hours": 1000,
                    "Employees": 1,
                    "Total": 110000,
                    "BelowMinRate": false
                },
                {
                    "Title": "Data Engineer",
                    "Rate": 105,
                    "Hours": 1920,
                    "Employees": 1,
                    "Total": 201600,
                    "BelowMinRate": false
                },
                {
                    "Title": "Systems Engineer",
                    "Rate": 90,
                    "Hours": 1500,
                    "Employees": 1,
                    "Total": 135000,
                    "BelowMinRate": false
                },
                {
                    "Title": "Electrician",
                    "Rate": 35,
                    "Hours": 1000,
                    "Employees": 1,
                    "Total": 35000,
                    "BelowMinRate": true,
                    "MinRate": 51.15
                }
            ],
            "Equipment": [
                {
                    "Title": "Laptops",
                    "Rate": 700,
                    "Quantity": 9,
                    "Total": 6300
                }
            ],
            "Travel": 3200,
            "Total": 1264200
        },
        "Option": {
            "LaborCategory": [
                {
                    "Title": "Senior Project Manager",
                    "Rate": 118.45,
                    "Hours": 960,
                    "Employees": 1,
                    "Total": 113712,
                    "BelowMinRate": false
                },
                {
                    "Title": "Data Scientist",
                    "Rate": 128.75,
                    "Hours": 750,
                    "Employees": 1,
                    "Total": 96562.5,
                    "BelowMinRate": false
                },
                {
                    "Title": "Data Analyst",
                    "Rate": 97.85000000000001,
                    "Hours": 960,
                    "Employees": 2,
                    "Total": 187872.00000000003,
                    "BelowMinRate": false
                },
                {
                    "Title": "IT Specialist",
                    "Rate": 113.3,
                    "Hours": 500,
                    "Employees": 1,
                    "Total": 56650,
                    "BelowMinRate": false
                },
                {
                    "Title": "Data Engineer",
                    "Rate": 108.15,
                    "Hours": 960,
                    "Employees": 1,
                    "Total": 103824,
                    "BelowMinRate": false
                },
                {
                    "Title": "Systems Engineer",
                    "Rate": 92.7,
                    "Hours": 750,
                    "Employees": 1,
                    "Total": 69525,
                    "BelowMinRate": false
                },
                {
                    "Title": "Share Point Developer",
                    "Rate": 36.050000000000004,
                    "Hours": 500,
                    "Employees": 1,
                    "Total": 18025.000000000004,
                    "BelowMinRate": false
                }
            ],
            "Travel": 2000,
            "Total": 648170.5
        },
        "InflationRate": 3
    },
    {
        "Vendor": "CORLEONE DATA DOMINANCE SERVICES",
        "Period": "12 month Base + 6 month Option",
        "ContractType": "Firm Fixed Price",
        "Location": "Government site",
        "Base": {
            "LaborCategory": [
                {
                    "Title": "Project Manager Sr.",
                    "Rate": 150,
                    "Hours": 1920,
                    "Employees": 1,
                    "Total": 288000,
                    "BelowMinRate": false
                },
                {
                    "Title": "Database Developer",
                    "Rate": 135,
                    "Hours": 1920,
                    "Employees": 2,
                    "Total": 518400,
                    "BelowMinRate": false
                },
                {
                    "Title": "Business Intelligence Analyst",
                    "Rate": 105,
                    "Hours": 1920,
                    "Employees": 1,
                    "Total": 201600,
                    "BelowMinRate": false
                },
                {
                    "Title": "Database Architect",
                    "Rate": 125,
                    "Hours": 1920,
                    "Employees": 2,
                    "Total": 480000,
                    "BelowMinRate": false
                },
                {
                    "Title": "Management Analyst II",
                    "Rate": 95,
                    "Hours": 1920,
                    "Employees": 1,
                    "Total": 182400,
                    "BelowMinRate": false
                },
                {
                    "Title": "Database Administrator",
                    "Rate": 90,
                    "Hours": 1920,
                    "Employees": 1,
                    "Total": 172800,
                    "BelowMinRate": false
                },
                {
                    "Title": "SharePoint Developer",
                    "Rate": 80,
                    "Hours": 1000,
                    "Employees": 1,
                    "Total": 80000,
                    "BelowMinRate": false
                },
                {
                    "Title": "IT Specialist",
                    "Rate": 85,
                    "Hours": 1000,
                    "Employees": 1,
                    "Total": 85000,
                    "BelowMinRate": false
                }
            ],
            "Equipment": [
                {
                    "Title": "Laptops ",
                    "Rate": 650,
                    "Quantity": 10,
                    "Total": 6500
                }
            ],
            "Travel": 1500,
            "Total": 2016200
        },
        "Option": {
            "LaborCategory": [
                {
                    "Title": "Project Manager Sr.",
                    "Rate": 154.125,
                    "Hours": 960,
                    "Employees": 1,
                    "Total": 147960,
                    "BelowMinRate": false
                },
                {
                    "Title": "Database Developer",
                    "Rate": 138.7125,
                    "Hours": 960,
                    "Employees": 2,
                    "Total": 266328,
                    "BelowMinRate": false
                },
                {
                    "Title": "Business Intelligence Analyst",
                    "Rate": 107.8875,
                    "Hours": 960,
                    "Employees": 1,
                    "Total": 103572,
                    "BelowMinRate": false
                },
                {
                    "Title": "Database Architect",
                    "Rate": 128.4375,
                    "Hours": 960,
                    "Employees": 2,
                    "Total": 246600,
                    "BelowMinRate": false
                },
                {
                    "Title": "Management Analyst II",
                    "Rate": 97.61250000000001,
                    "Hours": 960,
                    "Employees": 1,
                    "Total": 93708.00000000001,
                    "BelowMinRate": false
                },
                {
                    "Title": "Database Administrator",
                    "Rate": 92.47500000000001,
                    "Hours": 960,
                    "Employees": 1,
                    "Total": 88776.00000000001,
                    "BelowMinRate": false
                },
                {
                    "Title": "SharePoint Developer",
                    "Rate": 82.2,
                    "Hours": 500,
                    "Employees": 1,
                    "Total": 41100,
                    "BelowMinRate": false
                },
                {
                    "Title": "IT Specialist",
                    "Rate": 87.3375,
                    "Hours": 500,
                    "Employees": 1,
                    "Total": 43668.75,
                    "BelowMinRate": false
                }
            ],
            "Travel": 750,
            "Total": 1032462.75
        },
        "InflationRate": 2.75
    }
]
```

### Response model
Field name | Data Type | Description
-----------|---------- | -----------
Vendor | string | vendor name
Period | string | for example "12 month Base + 6 month Option"
ContractType | string | for example "Firm Fixed Price"
Location | string | usually state name
Base | Labor proposal model | base rate
Option | Labor proposal model | option rate
InflationRate float64 | for example "2.76"

### Labor proposal model
Field name | Data Type | Description
-----------|---------- | -----------
LaborCategory | array of Labor model | omit if it's empty
Subcontractor | array of Labor model | omit if it's empty
Equipment  | array of Equipment model | omit if it's empty
Travel | float64 | amount for tavel expense
Total  | float64 | total amount

### labor model
Field name | Data Type | Description
-----------|---------- | -----------
Title  | string |
Rate | float64 |
Hours | float64 |
Employees | float64 |
Total | float64 |
BelowMinRate | bool  | set to true if the rate is below minimum rate
MinimRate | float64 | minimum rate (if available)


### Equipment model
Field name | Data Type
-----------|----------
Title | string
Rate | float64
Quantity | float64
Total | float64
