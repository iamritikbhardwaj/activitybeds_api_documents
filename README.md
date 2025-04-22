# activitybeds_api_documents
This repo is to explain the working of activitybeds_api's working

# 🌍 GET /gapi/getCountries

Fetches the list of all countries available in the system, including their metadata, cities, and currency info.

---

## ✅ Response Structure

### Success Response

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
