# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
TO IMPLEMENT THE SLIDING WINDOW PROTOCOL

## DEVOLOPED BY: NAVEEN.S
## REGISTER NUMBER:212223240106

## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
SERVER:
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is waiting for connection...")
c, addr = s.accept()
print("Connected with: ", addr)
size = int(input("Enter number of frames to send: "))
frames = list(range(size))
window_size = int(input("Enter Window Size: "))
start = 0
i = 0

while True:
    while i < len(frames):
        end = start + window_size
        data = str(frames[start:end])
        c.send(data.encode())
        print("Sent:", data)
        ack = c.recv(1024).decode()
        if ack:
            print("Client:", ack)
        start += window_size
        i += window_size
```
CLIENT:
```
import socket
s = socket.socket()
s.connect(('localhost', 8000))
print("Connected to Server")

while True:
    data = s.recv(1024).decode()
    if not data:
        break
    print("Received:", data)
    s.send("Acknowledgement received from Client".encode())
```
## OUPUT
SERVER:
<img width="1041" height="526" alt="image" src="https://github.com/user-attachments/assets/ddb51b48-be23-4b23-a3fb-eb88c6be4491" />
CLIENT:
<img width="1050" height="385" alt="image" src="https://github.com/user-attachments/assets/2d65e37d-e5fb-4f28-8813-cddde26bbe88" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
