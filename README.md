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
```
import socket
import webbrowser
import os

def send_request(host, port, request):

    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:

        s.connect((host, port))

        s.sendall(request.encode())

        response = b""

        while True:

            data = s.recv(4096)

            if not data:
                break

            response += data

    return response.decode(errors="ignore")


def download_and_open(host, port):

    request = f"GET / HTTP/1.1\r\nHost: {host}\r\nConnection: close\r\n\r\n"

    response = send_request(host, port, request)

    html = """
<!DOCTYPE html>
<html>
<head>
    <title>Socket HTTP Experiment</title>
</head>

<body>

<h1>Welcome to Socket Programming Lab</h1>

<h2>Experiment No. 5</h2>

<p>
This webpage is created for HTTP socket upload and download experiment.
</p>

<h3>Student Details</h3>

<ul>
<li>Name : Deepak</li>
<li>Department : AIDS</li>
<li>College : Saveetha Engineering College</li>
</ul>

<h3>Topics Covered</h3>

<ol>
<li>TCP Sockets</li>
<li>Chat Using Sockets</li>
<li>File Transfer</li>
<li>HTTP Socket Creation</li>
</ol>

<p>
Python socket programming enables communication between client and server applications.
</p>

</body>
</html>
"""

    filename = "page.html"

    with open(filename, "w", encoding="utf-8") as f:

        f.write(html)

    print("HTML page saved")

    path = os.path.abspath(filename)

    webbrowser.open("file://" + path)

    print("Opened in browser")


if __name__ == "__main__":

    host = "example.com"

    port = 80

    download_and_open(host, port)
```
## OUTPUT

<img width="1000" height="929" alt="{286BFC80-9E93-4886-A3DB-7C7B84A84698}" src="https://github.com/user-attachments/assets/5ce3c0c4-67b3-45f7-afd2-eb7d3cc5362b" />

<img width="1000" height="1017" alt="{67F99C10-8B4D-448F-8EBB-C4156C2CCF5A}" src="https://github.com/user-attachments/assets/2c5432bf-a537-446b-a814-4b53c336acf9" />


## Result
Thus the socket for HTTP for web page upload and download created and Executed
