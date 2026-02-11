# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
server side:
~~~
import socket

arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
    "192.168.1.3": "AA:BB:CC:DD:EE:03"
}

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 5000

server.bind((host, port))
server.listen(1)

print("ARP Server is waiting for connection...")

conn, addr = server.accept()
print("Connected to client:", addr)

ip_address = conn.recv(1024).decode()
print("Received IP:", ip_address)

mac_address = arp_table.get(ip_address, "IP Address not found in ARP Table")

conn.send(mac_address.encode())

conn.close()
server.close()
~~~
client side:
~~~
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 5000

client.connect((host, port))

ip = input("Enter IP Address: ")

client.send(ip.encode())

mac = client.recv(1024).decode()

print("MAC Address:", mac)

client.close()
~~~

## OUPUT - ARP
server side:
<img width="1033" height="651" alt="Screenshot 2026-02-11 110946" src="https://github.com/user-attachments/assets/1d4cadd8-90ed-4ae5-a599-703892068d98" />
client side:
<img width="1062" height="457" alt="Screenshot 2026-02-11 111019" src="https://github.com/user-attachments/assets/11764957-202c-4f64-860b-3e07ec0dbfc6" />


## PROGRAM - RARP
server side:
~~~
import socket

rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 6000

server.bind((host, port))
server.listen(1)

print("RARP Server is waiting for connection...")

conn, addr = server.accept()
print("Connected to client:", addr)

mac_address = conn.recv(1024).decode()
print("Received MAC:", mac_address)

ip_address = rarp_table.get(mac_address, "MAC Address not found in RARP Table")

conn.send(ip_address.encode())

conn.close()
server.close()
~~~
client side:
~~~
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 6000

client.connect((host, port))

mac = input("Enter MAC Address: ")

client.send(mac.encode())

ip = client.recv(1024).decode()

print("IP Address:", ip)

client.close()
~~~
## OUPUT -RARP
server side:

<img width="1032" height="688" alt="Screenshot 2026-02-11 111754" src="https://github.com/user-attachments/assets/ed805e6b-4fc8-4ed1-af6c-b90719fdded7" />
client side:

<img width="1033" height="577" alt="Screenshot 2026-02-11 111828" src="https://github.com/user-attachments/assets/d30abe57-6e02-4937-ad15-0b0c66b71f19" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
