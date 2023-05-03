#include <stdio.h>
#include <stdlib.h>
#include <winsock2.h>
#include <ws2tcpip.h>

int is_port_open(const char *hostname, int port) {
    struct sockaddr_in server;
    SOCKET sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    if (sock == INVALID_SOCKET) {
        printf("Socket creation failed: %d\n", WSAGetLastError());
        return 0;
    }

    memset(&server, 0, sizeof(server));
    server.sin_family = AF_INET;
    server.sin_addr.s_addr = inet_addr(hostname);
    server.sin_port = htons(port);

    int connectionResult = connect(sock, (struct sockaddr *)&server, sizeof(server));
    closesocket(sock);

    return connectionResult == 0;
}

int main(int argc, char *argv[]) {
    if (argc != 3) {
        printf("Usage: %s <hostname> <number_of_ports>\n", argv[0]);
        return 1;
    }

    WSADATA wsaData;
    int initResult = WSAStartup(MAKEWORD(2, 2), &wsaData);
    if (initResult != 0) {
        printf("WSAStartup failed: %d\n", initResult);
        return 1;
    }

    const char *hostname = argv[1];
    int numberOfPorts = atoi(argv[2]);

    for (int port = 1; port <= numberOfPorts; port++) {
        if (is_port_open(hostname, port)) {
            printf("port %d is open\n", port);
        }
    }
        WSACleanup();

        return 0;

    }
