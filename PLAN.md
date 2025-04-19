**The Goal:**

*   Get the gas usage data from the meter equipment automatically.
*   Send this data over the cell phone network (like sending a text message, but with data).
*   Have the data land on a central computer (your server) where you can see it and store it.

**The Main Players (What You Need):**

1.  **The Gas Meter Equipment (Корректор):** This is the device actually measuring the gas out in the field. It might be in a place where sparks are dangerous (Hazardous Zone).
2.  **The Magic Box (БПЭК-03/ЦК):** This is the star of the show.
    *   It lives in a safe area (Safe Zone), *not* where the gas meter is.
    *   It connects to the Gas Meter with a **special safe wire** that prevents sparks.
    *   Inside, it has a **built-in cell phone modem**, like a basic phone that can only send data.
    *   It needs a **SIM card** (like your phone) to connect to the cell network.
3.  **Your Server:** A computer, probably in your office or a data center, that is always turned on and connected to the internet. This is where the data will be sent.
4.  **Cell Phone Network:** The invisible network (like Vodaphone, T-Mobile, etc.) that the Magic Box uses to send the data.
5.  **Special Software ("Газсеть: Сервис"):** You need this program on a laptop *temporarily* to teach the Magic Box what to do.

**How it Works (The Simple Story):**

1.  **Measuring:** The Gas Meter Equipment constantly measures how much gas is flowing.
2.  **Asking Safely:** The Magic Box (БПЭК) periodically asks the Gas Meter Equipment for its latest readings using the special safe wire.
3.  **Storing:** The Magic Box remembers these readings.
4.  **Scheduled Call:** You'll tell the Magic Box *when* to send the data (e.g., "Every night at 1:00 AM").
5.  **Connecting:** At that scheduled time, the Magic Box uses its SIM card and antenna to connect to the cell phone data network (GPRS).
6.  **Sending:** It sends the stored gas readings as a data file over the network to the specific internet address of *your server*. It uses a standard method like FTP (think of it like uploading a file to a website).
7.  **Receiving:** Your server, which is listening for incoming data, receives the file and saves it.
8.  **Waiting:** The Magic Box disconnects from the cell network and goes back to collecting readings, waiting for the next scheduled time to send again.

**What You Need to Do (Simplified Steps):**

1.  **Install the Hardware:**
    *   Mount the Gas Meter Equipment in its location (Hazardous Zone - **Get qualified help for this!**).
    *   Mount the Magic Box (БПЭК) in a safe nearby location.
    *   Connect them using the correct, special safe cable.
    *   Connect the power cord and the **essential ground wire** to the Magic Box.
    *   Screw the antenna onto the Magic Box.
2.  **Prepare the SIM Card:**
    *   Get a SIM card from a cell provider.
    *   Make sure it has a **data plan** (GPRS).
    *   Make sure it's **activated** and has money/credit if needed.
    *   **Crucially:** Disable the PIN code lock on the SIM card (you can usually do this using a regular cell phone).
    *   Put this SIM card into the slot inside the Magic Box.
3.  **Teach the Magic Box (Configuration):**
    *   Connect your laptop (with "Газсеть: Сервис" software) to the Magic Box using a standard USB cable.
    *   In the software, tell the Magic Box:
        *   The **internet address** of your server (e.g., `ftp.mycompany.com` or an IP address like `192.168.1.100`).
        *   The **username** and **password** needed to log in to your server (you'll set this up on the server).
        *   The **APN** setting for your SIM card (the cell provider gives you this - it's needed to connect to their data network).
        *   **How often** to send the data (e.g., once a day at 01:00).
    *   Save these settings to the Magic Box. Disconnect the laptop.
4.  **Set Up Your Server:**
    *   Make sure your server computer is running.
    *   Install software that can act as an **FTP server** (like FileZilla Server, or use built-in Windows/Linux features). The official "Газсеть: Экстра" software does this, but standard FTP works too if you know how to handle the data files.
    *   Create the **username** and **password** that you told the Magic Box.
    *   Ensure the server is **reachable** from the internet/cell network (this might involve network/firewall configuration - ask your IT person if unsure).

**And That's It!**

If everything is set up correctly, the Magic Box (БПЭК) will now automatically connect and send its data to your server at the time you scheduled. You just need to check your server for the new data files each day (or however often you set it).

**Key Things to Remember:**

*   **Safety:** Wiring in hazardous areas is serious. Use qualified people. Grounding is essential.
*   **SIM Card:** No PIN lock, needs data plan.
*   **Server Address:** The Magic Box needs the *correct* address and login for your server.
*   **Firewalls:** Make sure firewalls aren't blocking the Magic Box from reaching your server.
