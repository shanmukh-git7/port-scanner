import socket
from datetime import datetime

# Input target
target = input("Enter target IP or domain: ")

# Resolve domain to IP (optional)
try:
    target_ip = socket.gethostbyname(target)
except socket.gaierror:
    print("Invalid hostname. Exiting.")
    exit()

print(f"\nScanning target: {target_ip}")
print("Scanning ports 1 to 1024...\n")

# Start timer
start_time = datetime.now()

# Scan ports 1-1024
for port in range(1, 1025):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.settimeout(0.5)
    result = s.connect_ex((target_ip, port))
    if result == 0:
        print(f"Port {port} is OPEN")
    s.close()

# End timer
end_time = datetime.now()
total_time = end_time - start_time
print(f"\nScan completed in: {total_time}")

