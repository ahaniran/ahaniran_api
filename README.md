# AHANIRAN API Documentation

Welcome to **AHANIRAN**, your essential resource for detailed information about Iran's steel products. Our platform provides comprehensive data on various steel products, manufacturers, and the price history of each product. Whether you're in manufacturing, distribution, or research, AhanIran delivers the insights you need.

## API Key
All requests to the AhanIran API must include an `api_key` query parameter. To obtain an API key, please email your request to `info [at] ahaniran [dot] com`.

## Base URL
https://ahaniran.com/api/


## Error Handling
- **Unauthorized Requests**: Returns `401` status code with `"data": "NOT AUTHORIZED"`.
- **Invalid API Key**: Returns `401` status code with `"data": "INVALID API KEY"`.

## Endpoints

### 1. Get Product by ID
- **Endpoint**: `/product/[id]/`
- **Method**: `GET`
- **Description**: Returns information about a single product based on its ID. Supports the `populate` query to include simple values for the `factory` and `prices` properties.
- **Query Parameters**:
  - `populate` (optional): Specifies which properties to populate (`factory`, `prices`).
  - `fields` (optional): Specifies which fields to return.
- **Response**:
  ```json
  {
    "status": true,
    "data": {
      "id": int,
      "name": string,
      "status": bool,
      "size": float,
      "unit": string,
      "mode": string,
      "standards": [string],
      "factory": {
        "id": int,
        "name": string
      },
      "prices": [{
        "date": string,
        "price": float
      }]
    }
  }

### 2. Get Multiple Products
- **Endpoint**: `/product/`
- **Method**: `GET`
- **Description**: Returns information about multiple products. Supports the `populate` query to include simple values for the `factory` and `prices` properties. Includes pagination.
- **Query Parameters**:
  - `populate` (optional): Specifies which properties to populate (`factory`, `prices`).
  - `fields` (optional): Specifies which fields to return.
  - `page` (optional): Page number for pagination. Default is `1`.
- **Response**:
  ```json
  {
    "status": true,
    "data": {
      "page": int,
      "total_pages": int,
      "total_items": int,
      "items": [
        {
          "id": int,
          "name": string,
          "status": bool,
          "size": float,
          "unit": string,
          "mode": string,
          "standards": [string],
          "factory": {
            "id": int,
            "name": string
          },
          "prices": [{
            "date": string,
            "price": float
          }]
        }
      ]
    }
  }

### 3. Get Factory Information
- **Endpoint**: `/factory/`
- **Method**: `GET`
- **Description**: Returns an array of factories. Includes pagination.
- **Query Parameters**:
  - `page` (optional): Page number for pagination. Default is `1`.
- **Response**:
  ```json
  {
    "status": true,
    "data": {
      "page": int,
      "total_pages": int,
      "total_items": int,
      "items": [
        {
          "id": int,
          "name": string,
          "website": string,
          "capacity": string,
          "location": {
            "latitude": float,
            "longitude": float
          },
          "export": [string],
          "products": [{
            "id": int,
            "name": string,
            "status": bool,
            "size": float,
            "unit": string,
            "mode": string,
            "standards": [string],
            "prices": [{
              "date": string,
              "price": float
            }]
          }],
          "symbol": string
        }
      ]
    }
  }

### 4. Get Factory by ID
- **Endpoint**: `/factory/[id]/`
- **Method**: `GET`
- **Description**: Returns information about a single factory based on its ID.
- **Response**:
  ```json
  {
    "status": true,
    "data": {
      "id": int,
      "name": string,
      "website": string,
      "capacity": string,
      "location": {
        "latitude": float,
        "longitude": float
      },
      "export": [string],
      "products": [{
        "id": int,
        "name": string,
        "status": bool,
        "size": float,
        "unit": string,
        "mode": string,
        "standards": [string],
        "prices": [{
          "date": string,
          "price": float
        }]
      }],
      "symbol": string
    }
  }

### 5. Get Price Information
- **Endpoint**: `/price/`
- **Method**: `GET`
- **Description**: Returns an array of prices for a product based on its ID. Supports date filtering and pagination.
- **Query Parameters**:
  - `product_id` (required): Specifies the ID of the product.
  - `start_date` (optional): Specifies the start date for filtering prices. Format `YYYY-MM-DD`.
  - `end_date` (optional): Specifies the end date for filtering prices. Format `YYYY-MM-DD`.
  - `page` (optional): Page number for pagination. Default is `1`.
- **Response**:
  ```json
  {
    "status": true,
    "data": {
      "page": int,
      "total_pages": int,
      "total_items": int,
      "items": [
        {
          "date": string,
          "price": float
        }
      ]
    }
  }


## Acceptable Product Types
| **Product Type** | **توضیحات** |
|------------------|-------------|
| Rebar            | میلگرد            |
| Beam             | تیرآهن            |
| Profile          | پروفیل             |
| Sheet            | ورق               |
| Coil             | کلاف              |
| Pipe             | لوله              |


