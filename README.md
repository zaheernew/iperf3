# 🚀 iPerf3 - Network Bandwidth & Throughput Testing



iPerf3 is a **powerful open-source tool** used for measuring **bandwidth** and **throughput** between two network nodes. It’s widely used for **performance testing, benchmarking, and troubleshooting** in LAN/WAN environments.

With iPerf3, you can measure:

* 📶 **Bandwidth** (maximum data transfer capacity)
* 📊 **Throughput** (actual achieved transfer rate)
* 🌐 **Latency (Ping & Traceroute)**
* 📡 **TCP & UDP performance**

---

## 📘 Key Concepts

### 📶 Bandwidth

* Bandwidth is the **maximum capacity** of a network link.
* Think of it as the **width of a highway** — the larger it is, the more cars (data packets) can travel at once.

### 📊 Throughput

* Throughput is the **actual amount of data successfully transferred** over the link.
* It depends on **network conditions, congestion, and protocol efficiency**.
* Think of it as the **number of cars that actually make it to the destination**.

### ❓ Why Measure Bandwidth?

* To verify **ISP or internal network capacity**
* To plan **upgrades** and allocate resources
* To troubleshoot **slow links**

### ❓ Why Measure Throughput?

* To see **real-world performance** instead of just theoretical capacity
* To identify **bottlenecks, packet loss, or jitter**
* To ensure **applications (VoIP, video, etc.) work smoothly**

---

## 🎯 Purpose of iPerf3

✔️ Measures **maximum TCP and UDP bandwidth**
✔️ Supports **client/server mode**
✔️ Tests **one-way or bidirectional traffic**
✔️ Logs results for **performance analysis**
✔️ Cross-platform (Linux, Windows, macOS)

---

## ⚙️ Testing Setup with iPerf3

### 🖥️ Server Side

```powershell
# Open the iperf folder
# Log on to PowerShell (inside the folder)

PS C:\iperf3.18_64> .\iperf3.exe -s
```

This starts iPerf3 in **server mode**, waiting for client connections.

---

### 💻 Client Side

```powershell
# Open the iperf folder
# Log on to PowerShell (inside the folder)

# Allow script execution
PS C:\iperf> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
PS C:\iperf> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
# Press 'A' to confirm
```

Now run the automated PowerShell test script:

```powershell
PS C:\iperf> .\network_test.ps1
```

---

## 📜 `network_test.ps1` Script

This script automates **ping, TCP/UDP iPerf3 tests, and traceroute**, saving results into a timestamped log file.

```powershell
# Create the log directory if it doesn't exist
$logDir = "C:\iperf_logs"
if (!(Test-Path $logDir)) {
    New-Item -Path $logDir -ItemType Directory | Out-Null
}

# Ask user for a base filename
$fileName = Read-Host "Enter a name (Location) for the log file (without extension)"
$timestamp = Get-Date -Format "yyyy-MM-dd_HH-mm-ss"
$fullPath = "$logDir\$fileName`_$timestamp.txt"

# Start logging
"==== Network Test Log - $timestamp ====" | Out-File -FilePath $fullPath

"`n--- [Ping to 10.72.32.21] ---" | Out-File -Append $fullPath
ping 10.72.32.21 | Out-File -Append $fullPath

"`n--- [iPerf3 TCP Test to 10.72.32.20] ---" | Out-File -Append $fullPath
C:\iperf\iperf3.exe -c 10.72.32.20 | Out-File -Append $fullPath

"`n--- [iPerf3 UDP Test to 10.72.32.20] ---" | Out-File -Append $fullPath
C:\iperf\iperf3.exe -c 10.72.32.20 -u | Out-File -Append $fullPath

"`n--- [Traceroute to 10.72.32.21] ---" | Out-File -Append $fullPath
tracert 10.72.32.21 | Out-File -Append $fullPath

"`n==== End of Log ====" | Out-File -Append $fullPath

Write-Host "✅ Log saved to: $fullPath"
```

---

## ▶️ How to Run

1. Open PowerShell
2. Navigate to the iPerf3 folder:

   ```powershell
   PS C:\Windows\system32> cd C:\
   PS C:\> cd .\iperf3.18_64\
   ```
3. Run the script:

   ```powershell
   PS C:\iperf3.18_64> .\network_test.ps1
   ```

🔧 If script execution fails:

```powershell
PS C:\iperf3.18_64> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
PS C:\iperf3.18_64> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
PS C:\iperf3.18_64> Get-ExecutionPolicy -List
```

---

## 📊 Example Output

* ✅ Ping results (latency & packet loss)
* ✅ iPerf3 TCP test results (bandwidth in Mbps)
* ✅ iPerf3 UDP test results (jitter, packet loss, throughput)
* ✅ Traceroute (network path analysis)
* ✅ Saved in `C:\iperf_logs\` with timestamped filenames

---

## 🧑‍💻 Project Links

🔗 [Official iPerf3 Documentation](https://iperf.fr/iperf-doc.php)
🔗 [Download iPerf3](https://iperf.fr/iperf-download.php)

⚖️ License: iPerf3 is released under a **BSD license**.

🙏 Credits: iPerf3 is maintained by **ESnet** and the open-source community.

---

# 🧡 Happy Testing! 🚀
