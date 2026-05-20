# 5_Create_Socket_for_HTTP_for_webpage_upload_and_download
## NAME : Yuuvasri R
## REGISTER NUMBER : 212225230313
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
## Server:
```
import socket
server = socket.socket()
server.bind(('localhost', 8080))
server.listen(1)
print("Server waiting for connection...")
conn, addr = server.accept()
print("Connected by:", addr)
while True:
    data = conn.recv(4096)
    if not data:
        break
    print("\nReceived from client:\n")
    print(data.decode(errors='ignore'))
    response = "HTTP/1.1 200 OK\r\n\r\nFile received successfully"
    conn.send(response.encode())
conn.close()
server.close()
```
## Client:
```
import socket
def send_request(host, port, request):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((host, port))
        s.sendall(request)
        response = s.recv(4096).decode()
    return response
def upload_file(host, port, filename):
    with open(filename, 'rb') as file:
        file_data = file.read()
    content_length = len(file_data)
    headers = (
        f"POST /upload HTTP/1.1\r\n"
        f"Host: {host}\r\n"
        f"Content-Length: {content_length}\r\n\r\n")
    request = headers.encode() + file_data
    response = send_request(host, port, request)
    return response
if __name__ == "__main__":
    host = 'localhost'
    port = 8080
    filename = 'example.txt'
    response = upload_file(host, port, filename)
    print("\nServer Response:\n")
    print(response)
```
## OUTPUT
<img width="1094" height="961" alt="Screenshot 2026-05-20 195449" src="https://github.com/user-attachments/assets/37289993-afdf-4f29-8c7f-8af5c1342f4f" />
<img width="1108" height="970" alt="Screenshot 2026-05-20 195459" src="https://github.com/user-attachments/assets/2c13df2c-0e1a-43d8-9cde-3bb5e1eb7b46" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed






























.




















































.
