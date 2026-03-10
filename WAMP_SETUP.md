# ThinkFast WAMP Setup Guide

## 1. Copy Project Files

Copy the entire **ThinkFast3** folder into:

```
C:\wamp64\www\ThinkFast3\
```

---

## 2. Enable VirtualHost Configuration

Open the following file using a text editor **as Administrator**:

```
C:\wamp64\bin\apache\apache2.4.XX\conf\httpd.conf
```

Find this line (it may be commented out):

```
# Include conf/extra/httpd-vhosts.conf
```

Remove the `#` so it becomes:

```
Include conf/extra/httpd-vhosts.conf
```

---

## 3. Add the VirtualHost Block

Open:

```
C:\wamp64\bin\apache\apache2.4.XX\conf\extra\httpd-vhosts.conf
```

Paste the contents of **`thinkfast-vhost.conf`** (included in this project).

Make sure the **localhost VirtualHost block is still present**.
Without it, `http://localhost/` will stop working once named VirtualHosts are enabled.

---

## 4. Add Hosts Entry

Open **Notepad as Administrator**, then open this file:

```
C:\Windows\System32\drivers\etc\hosts
```

Add the following line at the bottom:

```
127.0.0.1   thinkfast
```

Save and close the file.

---

## 5. Make `data/` Writable

Right-click this folder:

```
C:\wamp64\www\ThinkFast3\data\
```

Go to:

```
Properties → Security
```

Give the Apache service account (**IUSR** or **Everyone** for local development) **Modify** permission so PHP can:

* Read and write `users.csv`
* Create files inside the `rooms/` directory

---

## 6. Restart WAMP

Click the **WAMP tray icon** → select:

```
Restart All Services
```

All WAMP tray icons should turn **green**.

---

## 7. Test PHP

Open the following URL:

```
http://thinkfast/backend/auth.php
```

You should see a JSON response like:

```
{"ok":false,"error":"Missing action"}
```

If you see an **HTML page instead**, PHP is not running.
Check that PHP is enabled in WAMP:

```
WAMP tray icon → PHP → Version
```

---

## 8. Open the Game

Open in your browser:

```
http://thinkfast/src/gui/
```

or simply:

```
http://thinkfast/
```

(The root URL automatically redirects to `/src/gui/`.)

---

# Multiplayer Setup (LAN)

To allow other devices on your network to connect:

### 1. Find Your Local IP

Open **Command Prompt** and run:

```
ipconfig
```

Look for your **IPv4 Address**, for example:

```
192.168.1.42
```

---

### 2. Edit Hosts File on Other Devices

On each device that will connect, add this entry to their **hosts file**:

```
192.168.1.42   thinkfast
```

---

### 3. Open the Game

On those devices, open:

```
http://thinkfast/src/gui/
```

---

### 4. Join a Room

1. Host creates a room
2. A **6-character room code** is generated
3. Other players enter the code to join
