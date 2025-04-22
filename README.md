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


GET http://localhost:3001/gapi/getOneActivity?id=33147
GET http://localhost:3001/gapi/getOneTransfer?id=33131
GET http://localhost:3001/gapi/getOneTour?id=12345
```

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

## 📌 Example Test With curl

```bash
curl http://localhost:3000/gapi/getCountries

curl "http://localhost:3000/gapi/getCities?code=SG"
```

---

> For support, raise an issue in this repo or reach out to the backend team.
