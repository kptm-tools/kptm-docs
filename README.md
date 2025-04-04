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


**Connection Establishment:**

Clients should establish a WebSocket connection 🔗 to the specified endpoint. The server will periodically broadcast scan data 📢 to all clients. 

#### 📤 Server -> Client Messages

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
