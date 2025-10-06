# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
-Aadhithan B 212224040001
## AIM
To implement a program to illustrate the mechanism of sliding window protocol

## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
   
## PROGRAM

SERVER 
```
import socket
server = socket.socket()
server.bind(('localhost', 8000))
server.listen(5)

print("Waiting for connection...")
client, addr = server.accept()
print("Connected with", addr)

size = int(input("Enter number of frames to send: "))
frames = list(range(size))
window_size = int(input("Enter Window Size: "))
start = 0
i = 0
while i < len(frames):
    end = start + window_size
    data = frames[start:end]
    client.send(str(data).encode())
    print(f"Sent frames: {data}")

    ack = client.recv(1024).decode()
    if ack:
        print("Acknowledgment received:", ack)
        start += window_size
        i += window_size

print("All frames sent successfully.")
client.close()
server.close()

```

CLIENT:
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    data = s.recv(1024).decode()
    if not data:
        break  
    print("Received frames:", data)
    s.send("Acknowledgment received from the client".encode())

s.close()
```

## OUPUT

SERVER:

<img width="1295" height="367" alt="image" src="https://github.com/user-attachments/assets/b4eabe93-a180-4eb7-bfdb-0d57951930f6" />

CLIENT:

<img width="1280" height="288" alt="image" src="https://github.com/user-attachments/assets/3219723c-0bde-467d-858b-108572a49f0d" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
