```cpp
#include <iostream>
#include <WinSock2.h>
#include <ws2tcpip.h>

#pragma comment(lib, "Ws2_32.lib")

int main() {
	WSADATA wsaData;
	int result = WSAStartup(MAKEWORD(2, 2), &wsaData);

	if(result != 0) {
		std::cerr << "WSAStartup failed: " << result << std::endl;
		return 1;
	}

	SOCKET serverSocket = socket(AF_INET, SOCK_DGRAM, IPPROTO_UDP);

	if(serverSocket == INVALID_SOCKET) {
		std::cerr << "Error creating socket: " << WSAGetLastError() << std::endl;
		WSACleanup();
		return 1;
	}

	sockaddr_in serverAddress = { 0, };

	serverAddress.sin_family = AF_INET;
	serverAddress.sin_port = htons(1234);
	inet_pton(serverAddress.sin_family, "127.0.0.1", &serverAddress.sin_addr);

	int resultBind = bind(serverSocket, reinterpret_cast<sockaddr*>(&serverAddress), sizeof(serverAddress));

	if(resultBind == SOCKET_ERROR) {
		std::cerr << "Error binding socket: " << WSAGetLastError() << std::endl;
		WSACleanup();
		return 1;
	}

	while(true) {
		sockaddr_in clientAddress = { 0, };
		int clientAddressLen = sizeof(clientAddress);

		char buffer[1024] = { 0, };

		int resultReceive = recvfrom(serverSocket, buffer, 1024, 0, reinterpret_cast<sockaddr*>(&clientAddress), &clientAddressLen);

		if(resultReceive == SOCKET_ERROR) {
			std::cerr << "Error receiving socket: " << WSAGetLastError() << std::endl;
			closesocket(serverSocket);
			WSACleanup();
			return 1;
		}

		std::cout << "Receive: " << buffer << std::endl;

		sendto(serverSocket, buffer, resultReceive, 0, reinterpret_cast<sockaddr*>(&clientAddress), clientAddressLen);
	}

	return 0;
}
```
