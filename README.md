# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 

## client
```import socket

s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("abi.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("abi.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
```

## server
```import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1.Download 2.Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```
## html
```<!DOCTYPE html>
<html>
<head>
<title>My Page</title>
<style>
body{font-family:Arial;text-align:center;background:#f2f2f2}
h1{color:blue}
button{padding:15px;background:green;color:white}
</style>
</head>

<body>
<h1>Welcome</h1>
<p>Simple webpage</p>

<button onclick="alert('Hello Welcome to webpage.')">Click Me</button>

</body>
</html>
```

## OUTPUT
<img width="626" height="141" alt="image" src="https://github.com/user-attachments/assets/0641d2b1-c19c-4c41-b1aa-b4095c2ac752" />
<img width="1047" height="754" alt="image" src="https://github.com/user-attachments/assets/0c4f54f9-4992-462c-926f-f496d00e1d05" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
