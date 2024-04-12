# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
```py
import socket

def send_file(client_socket, filename):
    try:
        with open(filename, 'rb') as file:
            data = file.read()
            client_socket.sendall(data)
            print("File sent successfully")
    except Exception as e:
        print("Error sending file:", e)

def receive_file(server_socket, filename):
    try:
        with open(filename, 'wb') as file:
            while True:
                data = server_socket.recv(1024)
                if not data:
                    break
                file.write(data)
            print("File received successfully")
    except Exception as e:
        print("Error receiving file:", e)

def server():
    host = '127.0.0.1'
    port = 12345

    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_socket.bind((host, port))
    server_socket.listen(5)
    print("Server listening on {}:{}".format(host, port))

    while True:
        client_socket, client_address = server_socket.accept()
        print("Connected to", client_address)

        filename = input("Enter filename to send: ")
        send_file(client_socket, filename)
        client_socket.close()

def client():
    host = '127.0.0.1'
    port = 12345

    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client_socket.connect((host, port))
    print("Connected to server")

    filename = input("Enter filename to save: ")
    receive_file(client_socket, filename)
    client_socket.close()

if __name__ == "__main__":
    import sys
    if len(sys.argv) < 2:
        print("Usage: python file_transfer.py [server | client]")
        sys.exit(1)
    if sys.argv[1] == "server":
        server()
    elif sys.argv[1] == "client":
        client()
    else:
        print("Invalid option. Please use 'server' or 'client'.")
```
## OUPUT
![311749291-b8c549bc-dea7-43c1-9744-9b2ca18c0baf](https://github.com/codedbykishore/3c.FILE_TRANSFER_USING_TCP_SOCKETS/assets/147139122/8662f9fd-2be9-4151-ab7b-a3bf0ab7d031)

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
