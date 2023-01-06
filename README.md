# _airline-data-modeling_

#### By _**Alejandro Socarras**_

#### _Unit 2, Week 3 Code Review_

## Description

```json
{
  "eticket_num": "498-938211-0795",
  "confirmation": "ZVFDC4",
  "ticket_date": "2022-03-23",
  "price": 723.42,
  "seat": "31I",
  "status": "active",

  "airline": {
    "name": "China Eastern Airlines",
    "iata": "MU",
    "icao": "CES",
    "callsign": "CHINA EASTERN",
    "country": "China"
  },

  "origin": {
    "name": "Montreal / Pierre Elliott Trudeau International Airport",
    "city": "Montreal",
    "country": "Canada",
    "iata": "YUL",
    "icao": "CYUL",
    "latitude": 45.47,
    "longitude": -73.74,
    "altitude": 118,
    "tz_timezone": "America/Toronto"
  },

  "destination": {
    "name": "Chicago Midway International Airport",
    "city": "Chicago",
    "country": "United States",
    "iata": "MDW",
    "icao": "KMDW",
    "latitude": 41.79,
    "longitude": -87.75,
    "altitude": 620,
    "tz_timezone": "America/Chicago"
  },

  "passenger": {
    "first_name": "Robert",
    "last_name": "Brown",
    "gender": "M",
    "birth_date": "1969-02-17",
    "email": "robert.brown.69@hotmail.com",
    "street": "5007 Thomas Way",
    "city": "Lake Hollystad",
    "state": "DC",
    "zip": "20027"
  }
}
```

Using `tickets.json`, complete the following exercises: 

### Exercise 1: Data Modeling

Using draw.io create a data model. Your data model MUST meet the following requirements:

1. Contain a _tickets_ fact table
1. Contain the following dimensions: _airlines_, _airports_, and _passengers_
1. Develop _passengers_ as an SCD Type2 dimension:
    - Passenger email can be used as the natural key
    - Be sure to add a surrogate key and effective start/end dates
    - You can optionally add an active column
1. IATA codes can be used as the primary key for both _airlines_ and _airports_
1. Use the t-ticket number as the primary key for the _tickets_ fact

<br><br>

### Exercise 2: Data Loading and Normalization

Develop an ETL pipeline that loads our dimensions and facts from the source file. You pipeline MUST meet the following requirements:

**General**:
- Load all dimensions in order: _airlines_, _airports_, and _passengers_
- Load the _tickets_ fact table after loading dimensions
- Your pipeline can drop/replace tables
- You can assume only inserts at this state. No updates, deletes, or merges

**Airlines Dim:**
- Identify unique airlines
- Use IATA code as the dimension key

**Airports Dim:**
- Identify unique airports from both origin and destination fields
- Use IATA code as the dimension key

**Passengers Dim:**
- Identify unique passengers
- Use the passenger email as the dimension natural key
- Generate UUIDs for the dimension surrogate keys
- Set the effective start date to any date. You can either use the ticket date, current date, or a fixed set date in the past
- Set the effective end date to None
- Optionally set your active flag to 'Y'
- Passenger address columns are considered SCD Type 2 columns
- All other columns are SCD Type 1

**Tickets Fact:**
- Link to _airlines_ and _airports_ dimensions by their IATA codes. 
- You don't need a lookup for _airlines_ and _airports_ since we use their IATA as dimension keys
- Link to the _passengers_ dimension by its surrogate key
- You need to perform a lookup to the _passengers_ dimension
- Load all teh tickets

## Setup/Installation Requirements

_To run the project from your local system:_

1. Make a directory on your disk where you would like to clone the repo.

2. Copy the repo link: https://github.com/apsocarras/spotify-pandas.git (available if you click the green "Code" dropdown button on this page).

3. Open your terminal and change into the directory you made (`cd /path/to/new/directory`).

4. Type `git clone ` and paste the URL.

## Known Bugs

_No known bugs._

## License

_[MIT License](https://opensource.org/licenses/MIT)_

Copyright (c) _1.6.23_ Alejandro Socarras

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


