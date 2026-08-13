# Experiment 3: Digital Forensics - Network Analysis with Wireshark and tcpdump

This experiment focuses on capturing and analyzing network traffic within the Google Cloud Shell environment using command-line tools and Wireshark.

## Execution Steps

### 1. Initial Packet Capture 
Opening the initial `.cap` file reveals the raw network traffic, including standard TCP handshakes and HTTP connections.
![Initial Capture](01_wireshark_initial_capture.png)

### 2. Filtering for HTTP GET Requests
Applying the display filter `http.request.method == "GET"` allows us to isolate specific web page requests and analyze the destination IPs.
![HTTP GET Filter](02_http_get_filter.png)

### 3. Analyzing TCP Errors
By inspecting the packet stream, we can identify TCP anomalies such as Spurious Retransmissions and Duplicate ACKs, which are useful for diagnosing network health.
![TCP Retransmissions](03_tcp_retransmissions.png)

### 4. General Traffic Analysis
Further analysis of the captured packets to understand the overall network flow.
![Traffic Analysis](04_general_traffic_analysis.png)

### 5. Executing tcpdump for Targeted Capture
Using `sudo tcpdump -w exact_capture.pcap port 80` in the terminal to actively listen and write incoming HTTP traffic to a new capture file.
![tcpdump Execution](08_tcpdump_execution.png)

### 6. Generating POST Traffic with cURL
Generating simulated login traffic by sending a `curl -X POST` request containing credentials to `httpbin.org` and a vulnerable test server.
![cURL POST Traffic](07_curl_post_traffic.png)

### 7. Filtering for HTTP POST Requests
Opening the new capture file and applying the `http.request.method == "POST"` filter successfully isolates the payload we just generated.
![HTTP POST Filter](05_http_post_filter.png)

### 8. Packet Payload Details
Inspecting the details of the filtered POST packet reveals the `application/x-www-form-urlencoded` data structure transmitted over the network.
![POST Packet Details](06_post_packet_details.png)



