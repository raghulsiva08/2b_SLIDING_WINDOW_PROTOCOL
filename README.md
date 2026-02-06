# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## REF NO: 25015705
### DATE:06-02-2026
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
server.py
~~~
import socket

s = socket.socket()
s.bind(('localhost', 1234))
s.listen(1)

print("Server Waiting...")
conn, addr = s.accept()
print("Connected from", addr)

while True:
    data = conn.recv(1024).decode()
    if not data:
        break

    print("Received Frames:", data)
    conn.send("ACK".encode())

conn.close()
s.close()
~~~
client.py
~~~
import socket

s = socket.socket()
s.connect(('localhost', 1234))

n = int(input("Enter number of frames: "))
window_size = 4

frames = []
for i in range(n):
    frames.append(i+1)

print("All Frames:", frames)

for i in range(0, n, window_size):
    window = frames[i:i+window_size]
    
    print("Sending Window:", window)
    s.send(str(window).encode())
    
    ack = s.recv(1024).decode()
    print("Received:", ack)

print("All frames sent successfully")
s.close()
~~~
## OUTPUT
server
<img width="1295" height="1079" alt="Screenshot 2026-02-06 112609" src="https://github.com/user-attachments/assets/59020bb1-2c36-4835-bab5-5569f15d3be5" />


client
<img width="1549" height="1053" alt="Screenshot 2026-02-06 112645" src="https://github.com/user-attachments/assets/9fa116b5-7e1a-4d1d-9848-ec0a220e383f" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
