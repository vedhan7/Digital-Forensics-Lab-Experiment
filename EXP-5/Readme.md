# Experiment 5: Digital Forensics - Autopsy.

## Execution Steps

### 1. Autopsy splash screen, "Done loading modules 
Opening the initial `.cap` file reveals the raw network traffic, including standard TCP handshakes and HTTP connections.
![Initial Capture](01_autopsy_installation.png)

### 2. Welcome / Open Recent Case dialog with "EXP5_DellLatitude
Applying the display filter `http.request.method == "GET"` allows us to isolate specific web page requests and analyze the destination IPs.
![HTTP GET Filter](02_new_case_creation.png)

### 3. 	Web History — 18 results, "Mr. Evil" browsing ethereal.com, wardriving.com, netstumbler.com
By inspecting the packet stream, we can identify TCP anomalies such as Spurious Retransmissions and Duplicate ACKs, which are useful for diagnosing network health.
![TCP Retransmissions](06a_web_history_artifacts.png)

### 4. 	Web Cookies — 24 results tied to "mr.evil@..."
Further analysis of the captured packets to understand the overall network flow.
![Traffic Analysis](06b_web_cookies_artifacts.png)

### 5. Web Bookmarks — 6 Microsoft-related bookmarks
Using `sudo tcpdump -w exact_capture.pcap port 80` in the terminal to actively listen and write incoming HTTP traffic to a new capture file.
![tcpdump Execution](06c_web_bookmarks_artifacts.png)

### 6. 	Run Programs — 59 prefetch (.pf) entries
Generating simulated login traffic by sending a `curl -X POST` request containing credentials to `httpbin.org` and a vulnerable test server.
![cURL POST Traffic](06d_run_programs_artifacts.png)

### 7. 	Recent Documents — GhostWare, Anonymizer, keys.lnk, Receipt.lnk
Opening the new capture file and applying the `http.request.method == "POST"` filter successfully isolates the payload we just generated.
![HTTP POST Filter](06e_recent_documents_artifacts.png)

### 8. Timeline Editor — event histogram 1989–2004
Inspecting the details of the filtered POST packet reveals the `application/x-www-form-urlencoded` data structure transmitted over the network.
![POST Packet Details](09_timeline_analysis.png)


