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

## 📝 Notes

- All timestamps are returned in ISO 8601 format.
- Country codes are case-insensitive (`sg`, `SG`, `sG` all work).
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
```
