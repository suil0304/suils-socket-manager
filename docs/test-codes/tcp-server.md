```cpp
// Code by AI
// sorry, im so lazy
#include <iostream>
#include <string>
#include <cstdint>
#include <cstring>
#include <WinSock2.h>
#include <ws2tcpip.h>

#pragma comment(lib, "Ws2_32.lib")

constexpr uint32_t HEADER_SIZE = 4;
constexpr uint32_t MAX_PAYLOAD_SIZE = 1024;

struct SuilTCPProtocolHeader {
	uint32_t payloadSize;
};

struct SuilTCPProtocol {
	SuilTCPProtocolHeader header;
	char payload[MAX_PAYLOAD_SIZE];
};

bool sendAll(SOCKET socket, const char* buffer, int length) {
	int sent = 0;

	while (sent < length) {
		int result = send(
			socket,
			buffer + sent,
			length - sent,
			0
		);

		if (result == SOCKET_ERROR || result == 0) {
			return false;
		}

		sent += result;
	}

	return true;
}

bool recvAll(SOCKET socket, char* buffer, int length) {
	int received = 0;

	while (received < length) {
		int result = recv(
			socket,
			buffer + received,
			length - received,
			0
		);

		if (result == 0) {
			return false;
		}

		if (result == SOCKET_ERROR) {
			return false;
		}

		received += result;
	}

	return true;
}

bool sendPacket(SOCKET socket, const char* payload, uint32_t payloadSize) {
	if (payloadSize > MAX_PAYLOAD_SIZE) {
		return false;
	}

	uint32_t networkPayloadSize = htonl(payloadSize);

	if (!sendAll(
		socket,
		reinterpret_cast<const char*>(&networkPayloadSize),
		sizeof(networkPayloadSize)
	)) {
		return false;
	}

	if (payloadSize == 0) {
		return true;
	}

	return sendAll(
		socket,
		payload,
		static_cast<int>(payloadSize)
	);
}

bool recvPacket(SOCKET socket, char* payload, uint32_t& payloadSize) {
	uint32_t networkPayloadSize = 0;

	if (!recvAll(
		socket,
		reinterpret_cast<char*>(&networkPayloadSize),
		sizeof(networkPayloadSize)
	)) {
		return false;
	}

	payloadSize = ntohl(networkPayloadSize);

	if (payloadSize > MAX_PAYLOAD_SIZE) {
		return false;
	}

	if (payloadSize == 0) {
		return true;
	}

	return recvAll(
		socket,
		payload,
		static_cast<int>(payloadSize)
	);
}

int main() {
	WSADATA wsaData;
	int result = WSAStartup(MAKEWORD(2, 2), &wsaData);

	if (result != 0) {
		std::cerr << "WSAStartup failed: " << result << std::endl;
		return 1;
	}

	SOCKET serverSocket = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);

	if (serverSocket == INVALID_SOCKET) {
		std::cerr << "Error creating socket: " << WSAGetLastError() << std::endl;
		WSACleanup();
		return 1;
	}

	sockaddr_in serverAddr = {};

	serverAddr.sin_family = AF_INET;
	serverAddr.sin_port = htons(8080);
	inet_pton(AF_INET, "127.0.0.1", &serverAddr.sin_addr);

	result = bind(
		serverSocket,
		reinterpret_cast<sockaddr*>(&serverAddr),
		sizeof(serverAddr)
	);

	if (result == SOCKET_ERROR) {
		std::cerr << "Error binding socket: " << WSAGetLastError() << std::endl;
		closesocket(serverSocket);
		WSACleanup();
		return 1;
	}

	result = listen(serverSocket, SOMAXCONN);

	if (result == SOCKET_ERROR) {
		std::cerr << "Error listening on socket: " << WSAGetLastError() << std::endl;
		closesocket(serverSocket);
		WSACleanup();
		return 1;
	}

	std::cout << "Listening on 127.0.0.1:8080" << std::endl;

	SOCKET clientSocket = accept(serverSocket, nullptr, nullptr);

	if (clientSocket == INVALID_SOCKET) {
		std::cerr << "accept failed: " << WSAGetLastError() << std::endl;
		closesocket(serverSocket);
		WSACleanup();
		return 1;
	}

	std::cout << "Client connected" << std::endl;

	const char* connectedMessage = "client connected, welcome.";

	if (!sendPacket(
		clientSocket,
		connectedMessage,
		static_cast<uint32_t>(strlen(connectedMessage))
	)) {
		std::cerr << "Error sending connected message: " << WSAGetLastError() << std::endl;
		closesocket(clientSocket);
		closesocket(serverSocket);
		WSACleanup();
		return 1;
	}

	char payload[MAX_PAYLOAD_SIZE];

	while (true) {
		uint32_t payloadSize = 0;

		if (!recvPacket(clientSocket, payload, payloadSize)) {
			std::cout << "Client disconnected or protocol error" << std::endl;
			break;
		}

		if (payloadSize == 0) {
			std::cout << "Received empty packet" << std::endl;
			continue;
		}

		std::cout << "Received: "
			<< std::string(payload, payloadSize)
			<< std::endl;

		if (!sendPacket(clientSocket, payload, payloadSize)) {
			std::cerr << "Error sending echo: " << WSAGetLastError() << std::endl;
			break;
		}
	}

	closesocket(clientSocket);
	closesocket(serverSocket);
	WSACleanup();

	return 0;
}
```
