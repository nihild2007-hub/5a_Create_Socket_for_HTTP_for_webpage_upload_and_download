# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm
1.Start the program.

2.Create a socket using Python socket library.

3.Bind the socket to localhost and port 8080.

4.Listen and accept connection from the client.

5.Receive HTTP request from the client.

6.If the request is GET, read the webpage file and send it to the client.

7.f the request is POST, receive the uploaded data and store it in a file.

8.Send HTTP response to the client.

9.Close the connection.

10.Stop the program.
## Program 
Server.py
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
        f = open("html.txt","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("upload.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
```
```
Client.py

import socket

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
## OUTPUT
https://private-user-images.githubusercontent.com/227093164/561367098-90cce965-a019-4e64-81f6-8fb3590dbaf2.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NzM1Njk5OTYsIm5iZiI6MTc3MzU2OTY5NiwicGF0aCI6Ii8yMjcwOTMxNjQvNTYxMzY3MDk4LTkwY2NlOTY1LWEwMTktNGU2NC04MWY2LThmYjM1OTBkYmFmMi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMzE1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDMxNVQxMDE0NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lZTVkM2I3ZWMyYmIzMTk4ZjEwZTZmYzhkOGIwODkxNWVmNjQxYjMwMWM0ZjBhMWZhMjQ3MjAwNDJiY2EwNzJjJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9._DUw3gF5Q975FZBVgP5zimGEeQdeubwh2fYGkdn6f_E
## Result
Thus the socket for HTTP for web page upload and download created and Executed
