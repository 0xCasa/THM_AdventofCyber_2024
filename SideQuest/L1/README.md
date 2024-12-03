# TryHackMe Advent of Cyber 2024 - SideQuest L1

## Log File

- Used Python to get a session cookie from the GitHub C2 server password.
    https://github.com/Bloatware-WarevilleTHM/C2-Server/blob/main/app.py
- Utilized Firefox and set the session cookie to access the `/data` page for the L1 tag.    
- Got password from key card and downloaded the pcap zip file and used the password to unzip it.
    https://github.com/gregheffner/THM_AdventofCyber_2024/blob/main/SideQuest/L1/T1_SideQuest.png
- Used Python to comb through the pcap file using `scapy.all` to reassemble a ZIP file.
    ```
    for packet in packets:
        if packet.haslayer(TCP) and packet.haslayer(Raw):
            payload = packet[Raw].load
            if b'PK\x03\x04' in payload:
                zip_data += payload[payload.find(b'PK\x03\x04'):]
            elif zip_data:
                zip_data += payload
    print("The reassembled ZIP file has been extracted: reassembled_file.zip")
    ```
- Unzipped the reassembled file and found it to need a password:
    ```[reassembled_file.zip] elves.sql password:```
