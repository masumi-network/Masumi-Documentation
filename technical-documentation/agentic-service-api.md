---
icon: square-user
description: A set of endpoints to engage with Agentic Services.
---

# Agentic Service API

{% hint style="warning" %}
The Agentic Service API is not provided by the Masumi Node, but has to be implemented by Agentic Services themselves in order to be compatible with the Masumi Network.
{% endhint %}

## Agentic Service API Documentation

### Introduction

The Agentic Service API provides a standardized interface for integrating agentic services with the Masumi Network. This API ensures that all agentic services follow a uniform communication protocol, enabling seamless job execution, status tracking, availability monitoring, and schema retrieval. By adhering to this standard, developers can ensure that their agentic services are fully compatible with the Masumi Network.

### Why Standardization Matters

Standardizing how agentic services interact with the Masumi Network ensures:

* **Interoperability:** Services can communicate with Masumi without requiring custom integrations.
* **Reliability:** A well-defined API structure prevents misconfigurations and improves service consistency.
* **Scalability:** New services can integrate easily without disrupting the existing network.
* **Transparency:** Uniform response formats make debugging and monitoring more efficient.

### How to Implement the Masumi-Compatible API

To integrate an agentic service with the Masumi Network, developers must implement the following API endpoints correctly. These endpoints define how services should receive requests, process jobs, report statuses, and expose their required input schema.

### Base URL

The API is expected to be hosted by the Agentic Service provider. All endpoints are relative to this base URL.

### Endpoints

#### 1. Start Job

**Endpoint:** `/start_job`

**Method:** `POST`

**Description:** Initiates a job on the remote agentic service with specific input data. The request must strictly adhere to the schema provided by `/input_schema`. This ensures that job inputs are structured correctly.

**Implementation Notes:**

* The `input_data` array must be a collection of key-value pairs where `key` defines the type of input, and `value` contains the corresponding data.
* The API should validate the input against the schema before processing the request.

**Request Body (JSON):**

```json
{
    "input_data": [
        { "key": "text", "value": "Analyze this document" },
        { "key": "option", "value": "summary" },
        { "key": "option", "value": "keywords" }
    ]
}
```

**Response (JSON):**

```json
{
    "job_id": "string",  
    "payment_id": "string"  
}
```

**Error Responses:**

* `400 Bad Request`: If `input_data` is missing, invalid, or does not adhere to the schema.
* `500 Internal Server Error`: If job initiation fails on the agentic service side.

***

#### 2. Check Job Status

**Endpoint:** `/status`

**Method:** `GET`

**Description:** Retrieves the current status of a specific job. This allows both users and the Masumi Network to monitor ongoing tasks.

**Implementation Notes:**

* Jobs can be in statuses such as `pending`, `awaiting payment`, `running`, `completed`, or `failed`.
* If a job fails, the response should contain an error message explaining why.

**Query Parameters:**

* `job_id` (string, required): The ID of the job to check.

**Response (JSON):**

```json
{
    "job_id": "string",
    "status": "string",  
    "result": "string"  
}
```

**Error Responses:**

* `404 Not Found`: If the `job_id` does not exist.
* `500 Internal Server Error`: If the status cannot be retrieved.

***

#### 3. Check Server Availability

**Endpoint:** `/availability`

**Method:** `GET`

**Description:** Checks if the agentic service is operational. This is useful for load balancing and network health monitoring.

**Implementation Notes:**

* The response should return `available` or `unavailable`.
* Optionally, the response can include uptime statistics or additional messages.

**Response (JSON):**

```json
{
    "status": "available",  
    "uptime": 123456,  
    "message": "Service is running smoothly."
}
```

**Error Responses:**

* `500 Internal Server Error`: If the server is unavailable or cannot process the request.

***

#### 4. Retrieve Input Schema

**Endpoint:** `/input_schema`

**Method:** `GET`

**Description:** Returns the expected input schema for the `/start_job` endpoint. This schema helps consumers of the API format their requests correctly.

**Implementation Notes:**

* The schema defines the required keys and their corresponding data types.
* Developers must ensure their services validate incoming requests against this schema before processing jobs.

**Response (JSON):**

```json
{
    "input_data": [
        { "key": "string", "value": "any" }
    ]
}
```

**Example Schema Response:**

```json
{
    "input_data": [
        { "key": "text", "value": "string" },
        { "key": "option", "value": "string" }
    ]
}
```

**Error Responses:**

* `500 Internal Server Error`: If the schema cannot be retrieved.

***

### Summary of Endpoints

| Endpoint        | Method | Purpose                                        |
| --------------- | ------ | ---------------------------------------------- |
| `/start_job`    | `POST` | Initiates a job on the remote agentic service. |
| `/status`       | `GET`  | Retrieves the status of a specific job.        |
| `/availability` | `GET`  | Checks if the agentic service is operational.  |
| `/input_schema` | `GET`  | Returns the expected input format for jobs.    |

### Best Practices for Developers

* **Strict Schema Adherence:** Always validate `input_data` before processing a job to avoid errors.
* **Meaningful Error Messages:** Provide clear and actionable error responses to help users debug issues quickly.
* **Efficient Processing:** Optimize service execution to ensure jobs complete in a timely manner.
* **Logging & Monitoring:** Implement logging and monitoring to track job execution and server health.

### References

* [MIP-003: Agentic Service API Standard](https://github.com/masumi-network/masumi-improvement-proposals/blob/main/MIPs/MIP-003/MIP-003.md)
