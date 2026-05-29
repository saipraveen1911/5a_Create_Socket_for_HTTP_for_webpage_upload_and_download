# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download

## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download

## Algorithm:

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

## Program :

MAIN CODE:

```
import socket
import webbrowser
import os

def send_request(host, port, request):

    with socket.create_connection((host, port)) as s:

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

    html = response.split("\r\n\r\n", 1)[1]

    filename = "page.html"

    with open(filename, "w", encoding="utf-8") as f:
        f.write(html)

    print("HTML page saved.")

    path = os.path.abspath(filename)

    webbrowser.open("file://" + path)

    print("Opened in browser.")

if __name__ == "__main__":

    host = "example.com"
    port = 80

    download_and_open(host, port)
```

PAGE HTML CODE:

```
210

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Example Domain</title>
    <style>
      body {
        background: #eee;
        width: 60vw;
        margin: 15vh auto;
        font-family: system-ui, sans-serif;
      }

      h1 {
        font-size: 1.5em;
      }

      main {
        opacity: 0.8;
      }

      a:link,
      a:visited {
        color: #348;
      }
    </style>
  </head>
  <body>
    <main>
      <h1>Example Domain</h1>
      <p>This domain is for use in documentation examples without needing permission. Avoid use in operations.</p>
      <p><a href="https://iana.org/domains/example">Learn more</a></p>
    </main>
  </body>
</html>

0
```

## OUTPUT:

<img width="1898" height="927" alt="5th exp - vscode" src="https://github.com/user-attachments/assets/e83cbbfc-a5a9-491e-a7f8-5bafac6975a4" />

<img width="1912" height="967" alt="domain 5th" src="https://github.com/user-attachments/assets/17e7fcb2-08f0-4b1f-ba85-c0bf9786c3d4" />

## Result:

Thus the socket for HTTP for web page upload and download created and Executed
