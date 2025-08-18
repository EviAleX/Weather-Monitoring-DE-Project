# Real-Time Weather Data Streaming and Analytics Platform

This project demonstrates an end-to-end, real-time data engineering solution built on Microsoft Azure and Fabric. The pipeline ingests live weather data from an external API, processes it in real-time, and visualizes the insights through interactive Power BI dashboards.

![Archicture diagram](images/architecture.png)
---
## 🏛️**Architecture Overview**

The architecture is designed for low-latency, high-throughput data processing, leveraging a modern, event-driven approach.

**Core technologies**:
- **Data Ingestion**: Azure Functions & Azure Event Hub & Databricks
- **Real-Time Processing**: Microsoft Fabric (EventStream, KQL Database)
- **Alerting**: Microsoft Fabric (Data Activator)
- **Business Intelligence**: PowerBI
- **Security**: Azure Key Vault

---
## 🚀**Pipeline Workflow**

The data flows through the system in four key stages:

### 1. **Data Ingestion (The Producer)**

- An **Azure Function**, triggered by a timer every 30 seconds, acts as the data producer.

<img width="1918" height="1065" alt="image" src="https://github.com/user-attachments/assets/5527feb9-d209-4a31-b7d8-bf343d9652af" />

- The function securely retrieves an API key from **Azure Key Vault**.
- It calls a live weather API to fetch current conditions, forecasts, and alerts for a specified location.

<img width="1919" height="1066" alt="image" src="https://github.com/user-attachments/assets/c01a4834-d902-449d-b199-d0408550f22f" />

- The raw JSON response is flattened and cleaned within the Python script to create a structured, single-level event.
- This processed event is then sent to an **Azure Event Hub**, which serves as the entry point for our streaming data.

<img width="1919" height="1062" alt="image" src="https://github.com/user-attachments/assets/a28446d4-c2de-492f-a762-8acef2d1796f" />
  
---

### 2. **Real-Time Processing (The stream)**

- A **Microsoft Fabric EventStream** is configured to listen to the Azure Event Hub.
- As data arrives, the EventStream ingests it and routes it directly to a **KQL Database (EventHouse)**. This database is optimised for high-speed ingestion and querying of time-series data.

<img width="1919" height="1062" alt="image" src="https://github.com/user-attachments/assets/27c0abf1-5bff-4cbb-9a46-cfcbae1ac2d3" />

---

### 3. **Monitoring & Alerting**

- **Microft Fabric's Data Activator** continuously monitors the data in the KQL Database. 
- It is configured with specific triggers (if there is any weather alert) to send out real-time alerts, enabling proactive responses to changing weather conditions.

<img width="1918" height="1064" alt="image" src="https://github.com/user-attachments/assets/42994ab1-4f82-4467-ba77-966bd260d459" />

---

### 4. **Visualisation & Reporting**

- **PowerBI** connects directly to the KQL Database in DirectQuery mode.
- This allows for the creation of powerful, interactive dashboards that visualise the weather data in near real-time providing stakeholders with up-to-the-second insights.

<img width="1919" height="1114" alt="image" src="https://github.com/user-attachments/assets/1ada78dd-85b7-4efb-ae8b-5b18bb682351" />

---

## ✅**Key Features** 
- **Severless Ingestion**: Utilizes Azure Functions for cost-effective, scalable data producer. 
- **Real-Time**: An event-driven architecture ensures data is processed and visualised with minimal latency. 
- **Secure**: Leverages Azure Key Vault for secrets management and Managed Identity for secure, passwordless connections between services.
- **Unified Analytics**: Demonstrates the power of Microsoft Fabric to unify data streaming, processing, and business intelligence in a single platform
