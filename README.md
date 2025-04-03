# 🚀 Core API Documentation 🚀

Welcome to the documentation repository for the Core API! 📖

This repository tracks changes and provides the Swagger documentation for the `core-service` API.

➡️ **View the Documentation Online:** [Core API Documentation](https://kptm-tools.github.io/kptm-docs/) ⬅️

---

This documentation is automatically generated and updated to reflect the latest changes in the `core-service` API.

Feel free to explore the API documentation to understand the available endpoints and data models.


# WebSocket API for Get Scans

This section describes the WebSocket API used for get scans, using WebSockets for real-time communication.

**Endpoint:** `ws://localhost:8002/ws`

**Header:** X-TenantId: 79c9acd6-a590-4394-8f2c-fadb07b79113


**Connection Establishment:**

Clients should establish a WebSocket connection to the specified endpoint. The server will send each minute the scans data for the dashboard


#### Server -> Client Messages

1. Sends scan data.

```json
[
  {
    "scan_id": "7136aa73-0291-48d9-99c3-c2dfb072c589",
    "scan_date": "2025-01-29T13:33:37.007298Z",
    "host": "altoro",
    "vulnerabilities": 0,
    "severities": {
      "critical": 0,
      "high": 0,
      "medium": 0,
      "low": 0
    },
    "duration": 63873754417.0073,
    "status": "Pending"
  }
]
```
