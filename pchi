#!/usr/bin/env python3
import socket
import sys


class Connection:
    def send(self, hostname, port, content):
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        s.connect((hostname, int(port)))
        s.sendall(str.encode(content))
        s.close()

    def receive(self, hostname, port):
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        s.bind((hostname, int(port)))
        s.listen(1)
        conn, addr = s.accept()
        print('Connected by', addr, file=sys.stderr)
        while 1:
            data = conn.recv(1024)
            if not data:
                break
            print(bytes.decode(data), end="", flush=True)
        conn.close()


def printHelp():
    print("Usages : ")
    print(sys.argv[0]+" send hostname port")
    print(sys.argv[0]+" receive hostname port")
    print()
    print("Example : ")
    print(sys.argv[0]+" send 127.0.0.1 8333")
    print()
    print("To send files, do the following")
    print(sys.argv[0]+" receive 127.0.0.1 8333 > outFile")
    print(sys.argv[0]+" send 127.0.0.1 8333 < inFile")
    quit()


def main():
    connection = Connection()
    if len(sys.argv) > 1 and sys.argv[1] == 'help':
        printHelp()
    assert len(sys.argv) == 4, "Invalid syntax, Try "+sys.argv[0]+" help"
    if sys.argv[1] == 'send':
        connection.send(sys.argv[2], sys.argv[3], sys.stdin.read())
    else:
        connection.receive(sys.argv[2], sys.argv[3])


if __name__ == "__main__":
    main()
