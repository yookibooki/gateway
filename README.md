**System Overview:**
The **ПК «Газсеть Шлюз» (Software Complex "Gazset Gateway")** is a comprehensive technical solution designed for building modern gas telemetry and dispatching networks on a regional scale. Its primary goal is to automate the monitoring and data collection from gas metering units (УУГ - Uzly Uchota Gaza). The system supports a specific range of hardware, including correctors and communication modules from "ЭЛЬСТЕР Газэлектроника" (LIS200 family: EK 260-290, TC 210-220), SMT-Smart gas meters with integrated communication, and TMP telemetry modules connected to BK series gas meters. It also supports other devices like СПГ, ИРВИС, Флоугаз correctors, FLOWSIC500, ВКГ-2, and controllers like КПРГ-6/БПЭК-04Ex. A key aspect is its design for easy integration with higher-level external information systems.

**Core Component: GatewayWS Web Service**

The central piece described in detail is the **GatewayWS** web service. This component acts as the primary interface for external systems.

1.  **Function:** It provides an open, standardized interface (SOAP/WSDL) to the backend **"Газсеть Экстра" server** and its associated database.
2.  **Capabilities:** The web service exposes numerous operations (`get...`, `set...` methods) allowing external client applications to:
    *   **Discover System Structure:** Retrieve lists of consumer groups (`getRootNodes`) and the devices (correctors, meters, modules) within them (`getChildNodes`, `getDeviceRV`).
    *   **Access Device Information:** Get details about specific devices, including their type, configuration, and supported parameters/tags (`getDeviceRV`, `getChildTags`).
    *   **Retrieve Data:** Fetch various types of data:
        *   **Current Data:** Real-time or near-real-time parameter values (`getLastCurrentParamsRV`, `getLastDeviceParamsRV`).
        *   **Historical Archives:** Interval, daily, monthly, event, audit/change logs (`getHistory`, `getDayHistory`, `getLastDayArcRV`, `getLastIntArcRV`, `getLastMonArcRV`, `getLastAuditRV`, `getLastSysStatRV`).
        *   **Consumption Archives:** Specific archives focused on gas volume/energy consumption (`getLastIntVolRV`, `getArchiveVolRV`).
    *   **Access Dictionaries:** Get lists and descriptions of system parameters, events, status codes, and measurement units (`getParamDictRV`, `getSysDictRV`, `getEventDict`, `getStateDict`, `getDBUnits`).
    *   **Incremental Updates:** Utilize a `rowVersion` mechanism to efficiently fetch only data that has been added or changed since the last request, reducing data transfer volume.
    *   **Limited Control:** Initiate on-demand polling for specific devices (`setExtraPoll`).
3.  **Technology:** Built on standard web service technologies (SOAP, WSDL, XML over HTTP). The manual provides instructions for generating client-side proxies (specifically for Java using JAX-WS and `wsimport`).

**System Architecture & Other Components (as inferred from the manual):**

While the manual focuses on the `GatewayWS` interface, it describes or depicts other necessary components:

1.  **Газсеть Database (Сервер БД Газсеть):** Stores all configuration data (groups, devices, parameters), historical archives, event logs, and system operational data. It's the central repository accessed by `GatewayWS`.
2.  **Communication Servers (TCP, CSD, FTP, ТМР):** Dedicated services responsible for the actual communication with field devices over different channels (GPRS-TCP, GSM/CSD, GPRS-FTP). `GatewayWS` likely interacts with these servers to manage real-time data flow or trigger polling.
3.  **Scheduler (Планировщик Газсеть):** Manages scheduled polling of devices (especially those on CSD or wired connections). It monitors data completeness and can request missing data fragments, potentially using `GatewayWS` for triggering.
4.  **Auto-Processor (Автообработчик):** Processes raw data files received from devices (via FTP, etc.) and imports the structured information into the main Газсеть database.
5.  **Field Devices:** The network of supported gas correctors, smart meters, and telemetry modules installed at metering points.
6.  **External Client Systems:** Higher-level applications (Billing, SCADA, Analytics, Dispatching Systems) that consume the `GatewayWS` web service to retrieve and utilize the gas metering data.

**Data Handling:**

*   **Address Space:** Organizes devices hierarchically into logical groups (e.g., by region, consumer).
*   **Parameter Access:** Uses a "mnemonic tag" system (Теги) for accessing parameters, providing a level of abstraction over device-specific addresses, particularly for the LIS200 family.
*   **Data Types:** Defines specific XML structures (classes) for returning data (e.g., `Archives`, `DayArc`, `IntArc`, `Device`, `Cust`, `Value`, `SysStat`). Status information is often encoded in bitmasks within specific fields (e.g., `StSy`, `St_4`, `crashState`, `alarmState`).
*   **Error Handling:** The system returns specific `#ERROR_XXX` codes via the web service to indicate various operational or data access issues.

**In essence, the "Газсеть Шлюз" system, with `GatewayWS` as its public face, acts as a middleware layer that collects, stores, and provides structured access to data from a diverse network of gas metering equipment, enabling integration with enterprise-level energy management and monitoring systems.**
