# 🌍 ActivityBeds API Documentation

Welcome to the **ActivityBeds API Docs**.  
This API allows clients to retrieve country and city data, including metadata like currencies, timezone offsets, and configuration flags.

the API supports access to:

- 🏞️ **Activities**
- 🚗 **Transfers**
- 🏨 **Hotels**

These services are designed to help build powerful travel platforms, booking engines, or integrated tourism systems.

---

## 📍 Base URL


http://activitybeds/gapi

---

## 📚 Endpoints Overview

| Endpoint                 | Method | Description                              |
|--------------------------|--------|------------------------------------------|
| `/getCountries`          | GET    | Returns a list of all countries          |
| `/getCities?code=XX`     | GET    | Returns cities for a specific country    |

---

## 🗺️ GET `/gapi/getCountries`

### Description

Fetches the full list of countries, including each country's metadata, cities, and currency details.

---

### ✅ Example Response

```json
{
  "STATUS": "SUCCESS",
  "MESSAGE": "Countries fetched successfully",
  "OUTPUT": [
    {
      "id": 1,
      "code": "SG",
      "name": "Singapore",
      "mobilePrefix": "+65",
      "isCurrencyExchange": true,
      "isDistributionTable": true,
      "isListing": true,
      "isBilling": true,
      "lastUpdated": "2025-04-08T06:13:14Z",
      "lastUpdatedBy": "13712",
      "currency": {
        "code": "SGD",
        "description": "Singapore Dollar",
        "markup": 1.5,
        "roundingUp": 0.01,
        "creditCardFee": 3
      },
      "cities": [
        {
          "id": 1,
          "name": "Singapore",
          "countryId": 1,
          "timezoneOffset": 480,
          "isCapital": true
        },
        {
          "id": 94,
          "name": "Others",
          "countryId": 1,
          "timezoneOffset": 480,
          "isCapital": false
        }
      ]
    }
  ]
}
```

---

### ❌ Error Response

```json
{
  "STATUS": "FAIL",
  "MESSAGE": "Internal server error",
  "OUTPUT": "Detailed error message"
}
```

---

## 🏙️ GET `/gapi/getCities`

### Description

Fetches cities for a specific country by its ISO country `code`.

---

### 🔍 Query Parameters

| Parameter | Type   | Required | Description                      |
|-----------|--------|----------|----------------------------------|
| `code`    | string | ✅ Yes    | ISO country code (e.g., `"SG"`)  |

---

### 📥 Example Request

```
GET /gapi/getCities?code=SG
```

---

### ✅ Example Success Response

```json
{
  "STATUS": "SUCCESS",
  "MESSAGE": "Cities fetched successfully",
  "OUTPUT": [
    {
      "id": 1,
      "name": "Singapore",
      "countryId": 1,
      "timezoneOffset": 480,
      "isCapital": true
    },
    {
      "id": 94,
      "name": "Others",
      "countryId": 1,
      "timezoneOffset": 480,
      "isCapital": false
    }
  ]
}
```

---

### ❌ Error Responses

#### Missing Code

```json
{
  "STATUS": "FAIL",
  "MESSAGE": "Country code is required",
  "OUTPUT": null
}
```

#### Country Not Found

```json
{
  "STATUS": "FAIL",
  "MESSAGE": "Country not found",
  "OUTPUT": null
}
```

#### Server Error

```json
{
  "STATUS": "FAIL",
  "MESSAGE": "Internal server error",
  "OUTPUT": "Detailed error message"
}
```
---

## 🧾 GET `/gapi/setProducts`

### Description

Fetches products (activities, tours, and transfers) for a specific city based on its name and country ID.

---

### 🔍 Query Parameters

| Parameter   | Type   | Required | Description                  |
|-------------|--------|----------|------------------------------|
| `city`      | string | ✅ Yes    | Name of the city (e.g., "Bali") |
| `countryId` | number | ✅ Yes    | Numeric ID of the country    |

---

### 📥 Example Request

GET http://localhost:3001/gapi/setProducts?city=Bali&countryId=2

### ✅ Example Success Response

```json
{
  "STATUS": "SUCCESS",
  "MESSAGE": "Products fetched successfully",
  "OUTPUT": [
    {
      "city": "Bali",
      "tours": [],
      "activities": [
        {
          "country": "Indonesia",
          "originalPrice": 6000,
          "keywords": null,
          "fromPrice": 130000,
          "city": "Bali",
          "currency": "IDR",
          "id": 33147,
          "isGTRecommend": false,
          "image": "a6247942-639b-4276-aa0a-c52486a04afa",
          "isOpenDated": true,
          "isOwnContracted": false,
          "merchant": {
            "id": 2608,
            "name": "Secret Garden Village"
          },
          "isFavorited": false,
          "isBestSeller": false,
          "fromReseller": null,
          "isCancellable": true,
          "name": "Activities at Secret Garden Village",
          "isInstantConfirmation": true,
          "category": "Attraction"
        },
        {
          "country": "Indonesia",
          "originalPrice": 1200000,
          "keywords": null,
          "fromPrice": 1200000,
          "city": "Bali",
          "currency": "IDR",
          "id": 34068,
          "isGTRecommend": false,
          "image": "f76fd59f-8855-4872-a0d4-056413a5b477",
          "isOpenDated": true,
          "isOwnContracted": false,
          "merchant": {
            "id": 2935,
            "name": "Gosek Adventure"
          },
          "isFavorited": false,
          "isBestSeller": false,
          "fromReseller": null,
          "isCancellable": true,
          "name": "ATV by Gosek Adventure",
          "isInstantConfirmation": true,
          "category": "Attraction"
        }
      ],
      "transfers": [
        {
          "country": "Indonesia",
          "originalPrice": 650000,
          "keywords": "Transfer,Cruise,Family Friendly",
          "fromPrice": 650000,
          "city": "Bali",
          "currency": "IDR",
          "id": 33131,
          "isGTRecommend": false,
          "image": "d1edfa67-473c-4d90-abc5-ffec1768a0c5",
          "isOpenDated": true,
          "isOwnContracted": false,
          "merchant": {
            "id": 2607,
            "name": "Dcamel Fast Cruise"
          },
          "isFavorited": false,
          "isBestSeller": false,
          "fromReseller": null,
          "isCancellable": true,
          "name": "2D1N Trip Nusa Lembongan by Dcamel",
          "isInstantConfirmation": true,
          "category": "Transportation"
        }
      ],
      "_id": "680775a3714274ec6cdb6c03",
      "__v": 0
    }
  ]
}
```

---

### ❌ Error Response

```json
{
  "STATUS": "FAIL",
  "MESSAGE": "City or country not found",
  "OUTPUT": null
}
```

---

### 📝 Notes

- This endpoint retrieves all available **activities**, **tours**, and **transfers** grouped under a city.
- Fields such as `isCancellable`, `isGTRecommend`, `merchant`, and `image` help power UI features on frontend platforms.
- Currency and pricing fields are returned for easy display and conversion.

---

## 🔍 GET `/gapi/getOneActivity`, `/getOneTransfer`, `/getOneTour`

### Description

These endpoints return a **single product** — either an activity, transfer, or tour — based on a unique ID passed as a query parameter.

---

### 🔍 Query Parameters

| Parameter | Type   | Required | Description                |
|-----------|--------|----------|----------------------------|
| `id`      | number | ✅ Yes    | The unique ID of the item  |

---

### 📥 Example Requests


- GET http://localhost:3001/gapi/getOneActivity?id=33147
- GET http://localhost:3001/gapi/getOneTransfer?id=33131
- GET http://localhost:3001/gapi/getOneTour?id=12345

---

### ✅ Example Success Response

```json
{
  "STATUS": "SUCCESS",
  "MESSAGE": "Products fetched successfully",
  "OUTPUT": [
    {
      "country": "Indonesia",
      "originalPrice": 6000,
      "keywords": null,
      "fromPrice": 130000,
      "city": "Bali",
      "currency": "IDR",
      "id": 33147,
      "isGTRecommend": false,
      "image": "a6247942-639b-4276-aa0a-c52486a04afa",
      "isOpenDated": true,
      "isOwnContracted": false,
      "merchant": {
        "id": 2608,
        "name": "Secret Garden Village"
      },
      "isFavorited": false,
      "isBestSeller": false,
      "fromReseller": null,
      "isCancellable": true,
      "name": "Activities at Secret Garden Village",
      "isInstantConfirmation": true,
      "category": "Attraction"
    }
  ]
}
```

---

### ❌ Error Response

```json
{
  "STATUS": "FAIL",
  "MESSAGE": "Product not found",
  "OUTPUT": null
}
```

---

### 📝 Notes

- These endpoints are useful for fetching details for a single card or detail page.
- Make sure the `id` is valid and exists in the database.
- Response will always return an array with a single object.

---

## 🔍 GET `/gapi/getProduct/details?id=45223`, `/getProduct/options?id=42432`



### 📥 Example Request

GET http://localhost:3001/gapi/getProduct/details?id=12342

### ✅ Example Success Response

```json
{
    "data": {
        "country": "Indonesia",
        "originalPrice": 8025000.0,
        "keywords": null,
        "blockedDate": [],
        "fromPrice": null,
        "city": "Bali",
        "postalCode": "805661",
        "latitude": -8.4060451,
        "description": "Also known as the Land of the Gods, Bali appeals through its sheer natural beauty of looming volcanoes and lush terraced rice fields that exude peace and serenity. It is also famous for surfers’ paradise! Bali enchants with its dramatic dances and colorful ceremonies, its arts, and crafts, to its luxurious beach resorts and exciting nightlife. And everywhere, you will find intricately carved temples.",
        "exclusions": [],
        "media": [
            {
                "id": 56933,
                "name": "6.png",
                "path": "97c4b953-f112-4953-9076-ef1c3a7cd3ca",
                "size": 786741.0,
                "type": "image/png",
                "extension": "png"
            },
            {
                "id": 56934,
                "name": "5.png",
                "path": "a02e1e2c-df81-40f6-bb90-28328cd31ee8",
                "size": 929030.0,
                "type": "image/png",
                "extension": "png"
            },
            {
                "id": 56935,
                "name": "2.png",
                "path": "487e1e00-944b-4162-a9d6-aa25d940d6d3",
                "size": 1094243.0,
                "type": "image/png",
                "extension": "png"
            },
            {
                "id": 56936,
                "name": "8.png",
                "path": "06bf0ef5-337d-4ef5-8252-1e254005aff8",
                "size": 873189.0,
                "type": "image/png",
                "extension": "png"
            },
            {
                "id": 56937,
                "name": "4.png",
                "path": "0464916d-4eb3-48b8-993a-56de860a6810",
                "size": 872750.0,
                "type": "image/png",
                "extension": "png"
            },
            {
                "id": 56938,
                "name": "7.png",
                "path": "f7380482-29f3-4494-be17-2ce6794aef42",
                "size": 1045177.0,
                "type": "image/png",
                "extension": "png"
            },
            {
                "id": 56939,
                "name": "3.png",
                "path": "73c6df3a-5412-46d4-931f-9341f118ed1b",
                "size": 1045011.0,
                "type": "image/png",
                "extension": "png"
            },
            {
                "id": 56940,
                "name": "9.png",
                "path": "d19e0389-29a6-4953-ba6e-b736aaba03a1",
                "size": 1138533.0,
                "type": "image/png",
                "extension": "png"
            }
        ],
        "countryId": 2,
        "whatToExpect": "D1: FULL DAY KINTAMANI TOUR (B/L/-) \nEmbark on an extraordinary journey as the tour commences with a delightful hotel pick up after a scrumptious breakfast. Prepare to be captivated by the mesmerizing Tegallalang rice terrace, where you'll be enveloped by the breathtaking beauty of terraced rice fields. Next, venture to Kintamani, where a delectable buffet lunch awaits you amidst the awe-inspiring backdrop of Mount and Lake Batur. Indulge your senses as you feast your eyes on this majestic view from a distance.\n\nAfter replenishing your energy, immerse yourself in the enchanting ambiance of Tirta Empul Temple in Tampak Siring. Discover the allure of its meticulously maintained gardens and be awestruck by the sacred spring water pool, revered by Hindus for its spiritual cleansing properties. \n\nBut the adventure doesn't end there! Prepare to be amazed as you visit Pejeng Klod, where the magnificent Tegal Sepih waterfall awaits. Feel the mist on your skin and be mesmerized by its cascading beauty. And to top it all off, explore some fascinating archaeological sites, unraveling the mysteries of the past.\n\nD2: WATERSPORT TANJUNG BENOA & ULUWATU TEMPLE TOUR (B/L/D) \nBreakfast at the hotel. After breakfast, the tour will begin with watersport activities in Tanjung Benoa. In this tour package you will get the opportunity to enjoy 1 x Banana Boat Ride and 1 x Parasailing. For other watersport games you can buy directly at the watersport vendor at your own expense. Once you are satisfied playing the watersport, you will enjoy lunch at the local restaurant. After lunch, the trip continued to visit GWK which is famous for the splendor of the statue of Lord Vishnu which is the second tallest statue in the world. After being satisfied with the GWK, the trip continued by visiting ULUWATU TEMPLE, enjoying the beauty of the sunset from the temple located at the end of a cliff that rises as high as 70 meters from the sea. After being satisfied with enjoying the sunset, the journey continued to Kedonganan Beach to enjoy seafood dinner. After dinner, go back to the hotel. \n\n\nD3: FULL DAY EAST OF BALI TOUR (B/L/-) \nBreakfast at the hotel. After breakfast, go directly to PURA LEMPUYANG which is located in Karangasem Regency. Upon arrival at Pura Lempuyang, you can enjoy the beauty of the temple located on top of Lempuyang Hill. It has an iconic view in the form of a temple gate which is set against the backdrop of the view of Mount Agung in the far reaches. After being satisfied with enjoying the beauty of the temple, the journey continued to TIRTA GANGGA. A heritage park of Keraajan Karangasem History in the 17th century. Enjoy the beauty of the park which has many beautiful ponds by hunting for photos for your Instagram collection. Lunch at a local restaurant. After lunch, the journey continues to TAMAN UJUNG SUKASADA which is also a relic of the Karangasem Kingdom in the 17th century. This vast garden was built as a resting place for the king in the dry season and also a place where the king receives guests. Afterwards, we returning to the hotel.",
        "termsAndConditions": "<div>\n<ul>\n<li>Package offered: Twin Sharing/Pax</li>\n<li>The Triple with EB price is the price for the 3rd person using an Extra Bed.&nbsp;</li>\n<li>The 3rd person price on tripple sharing room is same as child price</li>\n<li>Every hotel have different policy for High Season Surcharge and Peak Season Surcharge , please check HSS and PSS on every hotel</li>\n<li>The price is not included HSS nor PSS</li>\n<li>If you are is on HSS and PSS periode, then the price of the tour package will be added to the PSS and HSS of the hotel</li>\n<li>HSS and PSS calculations for TWIN SHARE are as follows: HSS or PSS x Total Night / 2 Pax</li>\n<li>HSS and PSS calculations for SINGLE OCCUPANCY are as follows: HSS or PSS x Total Night</li>\n</ul>\n</div>\n<div>\n<div>TOUR PACKAGE INCLUDE</div>\n<div>* 4 night accommodation on selected hotel&nbsp;</div>\n<div>* Tour according to the description on the tour program</div>\n<div>* Lunch and Dinner according to the itinerary on the tour program</div>\n<div>* Entrance tickets to tourist objects and activities according to the description on the tour program</div>\n<div>* Air Conditioned Transport according to the number of tour participants</div>\n<div>* Licensed Guide</div>\n<div>* Parking and Toll Fee</div>\n<div>* Mineral water during the tour</div>\n<div>* CHSE goodie bag upon pick up at the airport</div>\n<div>* Hand Sanitizers in the vehicle</div>\n<div>&nbsp;</div>\n<div>&nbsp;</div>\n<div>EXCLUDING:</div>\n<div>* Flight ticket</div>\n<div>* Personal Expenses</div>\n<div>* Guide and Driver Tipping&nbsp;</div>\n</div>",
        "timezoneOffset": 480,
        "currency": "IDR",
        "id": 37872,
        "isGTRecommend": false,
        "longitude": 115.1804969,
        "image": "1604998b-c7bc-4eec-8641-53d358b33854",
        "isOpenDated": true,
        "isOwnContracted": false,
        "merchant": {
            "name": "Artha Bayu Wisata",
            "id": 3658
        },
        "isFavorited": false,
        "isBestSeller": false,
        "howToUseList": [
            {
                "class": "com.globaltix.api.v1.HowToUse",
                "id": 473235,
                "attraction": {
                    "class": "com.globaltix.api.v1.Attraction",
                    "id": 37872
                },
                "isActive": true,
                "placementOrder": 2,
                "ticketTypeGroup": null,
                "value": "Ticketing counter"
            },
            {
                "class": "com.globaltix.api.v1.HowToUse",
                "id": 473236,
                "attraction": {
                    "class": "com.globaltix.api.v1.Attraction",
                    "id": 37872
                },
                "isActive": true,
                "placementOrder": 1,
                "ticketTypeGroup": null,
                "value": "Show Mobile Ticket for redemption"
            }
        ],
        "addressLine": "Dukuh Village Villas & Art",
        "fromReseller": null,
        "highlights": [
            "Ubud",
            "Uluwatu",
            "Tegallalang",
            "Tanjung Benoa"
        ],
        "operatingHours": {
            "fixedDays": [
                {
                    "day": "SUNDAY",
                    "startHour": "09:00",
                    "endHour": "17:00"
                },
                {
                    "day": "MONDAY",
                    "startHour": "09:00",
                    "endHour": "17:00"
                },
                {
                    "day": "TUESDAY",
                    "startHour": "09:00",
                    "endHour": "17:00"
                },
                {
                    "day": "WEDNESDAY",
                    "startHour": "09:00",
                    "endHour": "17:00"
                },
                {
                    "day": "THURSDAY",
                    "startHour": "09:00",
                    "endHour": "17:00"
                },
                {
                    "day": "FRIDAY",
                    "startHour": "09:00",
                    "endHour": "17:00"
                },
                {
                    "day": "SATURDAY",
                    "startHour": "09:00",
                    "endHour": "17:00"
                }
            ],
            "isToursActivities": null,
            "custom": null
        },
        "name": "3 Days Tour - Bali East",
        "isInstantConfirmation": true,
        "location": "Dukuh Village Villas & Art",
        "category": "Tours",
        "thingsToNote": [],
        "inclusions": []
    },
    "error": null,
    "size": 1,
    "success": true
}
```

---

## 📝 Notes

- All timestamps are returned in ISO 8601 format.
- Country codes are case-sensitive (`sg`, `sG` does not work).
- Response is always wrapped in `STATUS`, `MESSAGE`, and `OUTPUT`.

---

## 🧠 Developer Tips

- Use tools like **Postman** or **curl** to manually test endpoints.
- Ensure your MongoDB contains the base countries data before using `/getCities`.
- If you're using Mongoose, prefer `.lean()` to avoid circular JSON issues.
- Responses are designed to be frontend-consumable out of the box.

---

## 📌 Example Test With `curl`

You can use `curl` to test the API directly from your terminal or Postman.

```bash
# ✅ Get all countries
curl "http://localhost:3001/gapi/getCountries"

# ✅ Get cities for a specific country code (e.g., Singapore)
curl "http://localhost:3001/gapi/getCities?code=SG"

# ✅ Get products for a city (activities, transfers, tours)
curl "http://localhost:3001/gapi/setProducts?city=Bali&countryId=2"

# ✅ Get one activity by ID
curl "http://localhost:3001/gapi/getOneActivity?id=33147"

# ✅ Get one transfer by ID
curl "http://localhost:3001/gapi/getOneTransfer?id=33131"

# ✅ Get one tour by ID (replace with actual ID)
curl "http://localhost:3001/gapi/getOneTour?id=12345"
```

---

> For support, raise an issue in this repo or reach out to the backend team.
