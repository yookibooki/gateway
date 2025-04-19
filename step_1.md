**Goal:** Teach the БПЭК box where your server is and when to send the data.

**What You Need Ready:**

1.  **Your Server Details:**
    *   The **Internet Address** of your server (either a domain name like `ftp.yourcompany.com` or a static IP address like `123.45.67.89`).
    *   The **Username** for logging into your FTP server.
    *   The **Password** for logging into your FTP server.
2.  **SIM Card Details:**
    *   An **activated SIM card** with a **GPRS data plan** and **PIN lock disabled**.
    *   The **APN** (Access Point Name) provided by your SIM card's mobile operator (e.g., "internet", "internet.mts.ru", etc.). You *need* this for the БПЭК to connect to the mobile data network.
3.  **Your Laptop:** With "Газсеть: Сервис" installed.
4.  **Hardware Connected:**
    *   Laptop connected to БПЭК via USB.
    *   БПЭК connected to the Corrector.
    *   БПЭК powered on (and grounded!).
    *   Antenna connected to БПЭК.
    *   SIM card inserted into БПЭК.

**Steps Using "Газсеть: Сервис":**

1.  **Connect to the БПЭК:**
    *   Open "Газсеть: Сервис".
    *   In the connection settings (like Fig Г1):
        *   Select `БПЭК серии ЦК - config` as the device type.
        *   Select `по интерфейсу RS-232 и USB` for connection.
        *   Find the correct `COM` port that your laptop assigned to the USB connection.
        *   Set Speed: `19200`, Format: `8n1`, Quality: `турбо-режим`.
    *   Click the "Подключиться к прибору" (Connect to device) button (or similar). The status should change to "Соединение установлено" (Connection established - like Fig Г2).

2.  **Check Corrector Communication (Optional but Recommended):**
    *   Go to the "Корректор №1" tab.
    *   Go to the "Конфигурация" sub-tab. Make sure the correct `Тип корректора` (Corrector Type) is selected (Fig Г3).
    *   Go to the "Интерфейс" sub-tab. Make sure the `Тип интерфейса`, `Скорость обмена`, `Формат данных` match the settings of the actual corrector device it's connected to (Fig Г4). If these are wrong, the БПЭК can't read data from it.

3.  **Configure SIM Card & Network Access:**
    *   Go to the "Контроллер БПЭК" tab.
    *   Go to the "Сим №1" sub-tab (or "Сим №2" if using the second slot).
    *   Make sure `Состояние` (State) is set to `Включена` (Enabled).
    *   Find the **APN settings** section (likely within the FTP or CSD setup pop-up accessed via buttons on Fig Г8, or directly visible on a screen similar to Fig Г10's "Настройка APN" section).
    *   Enter the correct **APN** name provided by your mobile operator. You might also need APN username/password if your operator requires it (often blank).

4.  **Configure FTP Server Destination & Schedule:**
    *   Go to the "Контроллер БПЭК" tab -> "Сим №1" sub-tab (or Sim №2).
    *   Find the button for **"Режим FTP Настроить..."** (Configure FTP Mode...) (like on Fig Г8). Click it.
    *   A window like Fig Г10 should appear ("Настройка передачи данных").
    *   **Режим передачи (Transmission Mode):** Select how often you want data sent (e.g., `Раз в сутки` - Once a day).
    *   **Время (Time):** Set the specific time (e.g., `01:00:00`) for the daily transmission.
    *   **Настройка APN (APN Setup):** Double-check the APN is correct here too.
    *   **Настройка сервера №1 (Server #1 Setup):**
        *   **Адрес (Address):** Enter **Your Server's Internet Address**.
        *   **Логин (Login):** Enter **Your FTP Username**.
        *   **Пароль (Password):** Enter **Your FTP Password**.
    *   (Optional) You can configure a second server as a backup if needed.
    *   Click **"Применить" (Apply)** in this pop-up window.

5.  **Save Settings to БПЭК:**
    *   After configuring everything, click the main button that looks like a "Play" symbol or says **"Старт передачи данных"** (Start data transfer) in the main software window. This writes the configuration from the software into the БПЭК's memory.
    *   Wait for confirmation that the parameters were successfully updated.

6.  **Disconnect and Test:**
    *   Disconnect the USB cable from the БПЭК.
    *   Make sure your **Server Software (FTP Server)** is running on your server machine and is configured with the same username/password you gave the БПЭК.
    *   Make sure your server is reachable from the internet (firewalls configured correctly).
    *   Wait for the scheduled time (e.g., 1:00 AM).
    *   Check the designated folder on your FTP server. A new data file from the БПЭК should appear!

**Simple Analogy:** You just used the "Газсеть: Сервис" software on your laptop to give the БПЭК box:
*   The **phone number and instructions** (APN) to connect to the mobile data network.
*   The **mailing address** (Server Address) and **secret knock** (Username/Password) for your server.
*   A **schedule** (Time) telling it when to mail the data package (FTP file).
