# 🚀 Core API Documentation 🚀

Welcome to the documentation repository for the Core API! 📖

This repository tracks changes and provides the Swagger documentation for the `core-service` API.

➡️ **View the Documentation Online:** [Core API Documentation](https://kptm-tools.github.io/kptm-docs/) ⬅️

---

This documentation is automatically generated and updated to reflect the latest changes in the `core-service` API.

Feel free to explore the API documentation to understand the available endpoints and data models.

---

## ⚡ WebSocket API 

This section describes the asynchronous API used in `core-service`, featuring WebSockets for real-time communication.

### 🔍 Get Current Scans

**Endpoint:** `ws://localhost:8002/ws/scan` 🌐

**Header:** `Authorization`: Bearer your-authtoken-goes-here 🔑


#### Connection Establishment:

Clients should establish a WebSocket connection 🔗 to the specified endpoint. The server will periodically broadcast scan data 📢 to all clients. 

##### 📤 Server -> Client Messages

1. Sends scan data.

```json
[
    {
        "scan_id": "75e5b3d7-9932-47f5-a19a-4e59031ef99d",
        "scan_date": "2025-11-08T09:00:00Z",
        "host": "Printer Device 192.168.1.1",
        "vulnerabilities": 1,
        "severities": {
            "critical": 0,
            "high": 0,
            "medium": 1,
            "low": 0,
            "none": 0,
            "unknown": 0
        },
        "duration": 300,
        "status": "Completed"
    },
    {
        "scan_id": "0c560ebb-37e2-4375-ba11-9ea07191913b",
        "scan_date": "2025-01-01T10:00:00Z",
        "host": "Web Server example.com",
        "vulnerabilities": 1,
        "severities": {
            "critical": 1,
            "high": 0,
            "medium": 0,
            "low": 0,
            "none": 0,
            "unknown": 0
        },
        "duration": 300,
        "status": "Completed"
    }
]
```

### 📊 Dynamic Security Report

**Endpoint:** ws://localhost:8002/ws/report/{scanId} 🌐

    {scanId}: Path parameter representing the unique identifier of the cybersecurity scan. Each scanId can be considered a separate "room" for real-time interaction.

**Header:** Authorization: Bearer your-authtoken-goes-here 🔑

#### Connection Establishment:

Clients should establish a WebSocket connection 🔗 to the specified endpoint. The server will attempt to find or create a "room" for the given scanId.

#### Message Format:

All messages exchanged over the WebSocket connection are JSON objects with the following structure:

```json
{
  "type": "string",
  "payload": {}
}
```

#### 💬 Message Types

##### ➡️ Client -> Server Messages:

1. `initial_data_request`: Requests the initial data for the report.

```json
{
  "type": "initial_data_request",
  "payload": {
    "scan_id": "string"
  }
}
```

2. `vector_update`: Sends an update to a specific vector's value.

```json
{
  "type": "vector_update",
  "payload": {
    "vulnerability_type_name": "string",
    "new_value": 0.0
  }
}
```

3. `select_vector`: Informs the server which vector has been selected for detailed information.

```json
{
  "type": "select_vector",
  "payload": {
    "vulnerability_type_name": "string"
  }
}
```

4. `apply_vectors_request`: Signals that the user has finished adjusting the vectors and wants the final report data based on the applied values.

```json
{
  "type": "apply_vectors_request",
  "payload": {}
}
```

##### ⬅️ Server -> Client Messages:

1. `initial_data_response`: Sends the initial data required to render the report.

```json
{
  "type": "initial_data_response",
  "payload": {
    "vulnerability_types": [
      {
        "name": "string",
        "highest_cvss": 0.0,
        "count": 0,
        "percentage": 0.0,
        "available_cvss_values": []
      },
      // ... more vulnerability types
    ],
    "global_cvss_score": 0.0,
    "global_total_vulnerabilities": 0
  }
}
```

2. `vector_update_response`: Sends the updated global expected CVSS score and total vulnerabilities after a vector's value is applied (or moved).

```json
{
  "type": "vector_update_response",
  "payload": {
    "expected_global_cvss_score": 0.0,
    "expected_global_total_vulnerabilities": 0
  }
}
```

3. `vector_details_response`: Sends the details of the vulnerability with the highest CVSS for the selected vulnerability type.

```json
{
  "type": "vector_details_response",
  "payload": {
    "vulnerability_details": {
      "id": "string",
      "type": "string",
      "cvss": 0.0,
      "description": "string"
      // ... other relevant details
    }
  }
}
```

4. `report_data_response`: Sends the final response data, including vulnerabilities to be solved, unattended vulnerabilities, and the overall security posture. This is sent after the user clicks "Apply" and potentially "Next".

```json
{
  "type": "report_data_response",
  "payload": {
    "solved_vulnerabilities": [],
    "unattended_vulnerabilities": [],
    "expected_security_posture": "string"
  }
}
```

5. `error`: Indicated an error occurred on the server.

```json
{
  "type": "error",
  "payload": {
    "message": "string"
  }
}
```
