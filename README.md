# 2a_Stop_and_Wait_Protocol
## Name: SUBASH M
## Reg.no: 212224220109
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
server.py
```
# stop_and_wait_server.py
import socket
import time

# Create server socket
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind(('localhost', 9999))
server_socket.listen(1)

print("Server: Waiting for client connection...")
conn, addr = server_socket.accept()
print(f"Server: Connected to {addr}\n")

while True:
    # Receive frame
    frame = conn.recv(1024).decode()
    if not frame or frame == "END":
        print("Server: Transmission completed.")
        break

    print(f"Server: Received Frame {frame}")

    # Simulate processing delay
    time.sleep(1)

    # Send ACK back to client
    ack = f"ACK{frame}"
    conn.send(ack.encode())
    print(f"Server: Sent {ack}\n")

conn.close()
server_socket.close()
```
client.py
```
# stop_and_wait_client.py
import socket
import time

# Create client socket
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect(('localhost', 9999))

frames = int(input("Enter number of frames to send: "))

for i in range(frames):
    frame = str(i)
    print(f"Client: Sending Frame {frame}")
    client_socket.send(frame.encode())

    # Wait for ACK
    ack = client_socket.recv(1024).decode()
    print(f"Client: Received {ack}\n")
    time.sleep(1)  # Simulate delay

# End transmission
client_socket.send("END".encode())
print("Client: Transmission completed.")

client_socket.close()
```
## OUTPUT
<img width="1671" height="772" alt="Screenshot 2025-09-02 155756" src="https://github.com/user-attachments/assets/83c3c4c1-e074-41ad-8e68-a746188e545d" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
