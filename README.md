# 📱 Instant Messaging System (Backend)

Welcome to the **Instant Messaging System** backend, developed for the [TikTok Tech Immersion Server (Backend) Assignment](https://bytedance.sg.feishu.cn/docx/P9kQdDkh5oqG37xVm5slN1Mrgle). This project provides essential features for an instant messaging system, focusing on message handling through microservices architecture.

![Build Status](https://github.com/SharpWoofer/TikTok-IM/actions/workflows/test.yml/badge.svg)
![License](https://img.shields.io/badge/license-MIT-green)
![Language](https://img.shields.io/badge/language-Go-blue)
![Version](https://img.shields.io/badge/version-1.0.0-brightgreen)
![Docker](https://img.shields.io/badge/docker-ready-blueviolet)
![Documentation](https://img.shields.io/badge/docs-updated-yellow)

![244300799-7668d883-03dc-4cd3-b097-17704da9dd4a](https://github.com/user-attachments/assets/fdd96dc5-22ca-4ae2-b5f3-bdd2fface928)

## 📂 Project Overview

This backend system is designed to handle core messaging functionalities including sending and retrieving messages. It consists of two main services and utilizes Redis for data storage.

### Architecture Diagram
![UML diagram](https://github.com/user-attachments/assets/7fe46438-839a-4774-92ed-2d0a363a7368)

1. **Client (User)** initiates an HTTP request.
2. **HTTP Server** processes HTTP requests and forwards them to the **RPC Server**.
3. **RPC Server** handles business logic by performing **SendRequest** or **PullRequest** operations.
4. **SendRequest** writes messages to the **Redis** data store.
5. **PullRequest** retrieves messages from **Redis**.
6. **HTTP Server** returns the result to the client.

## 🚀 Features

- **Two Services:** HTTP server and RPC server for distinct messaging functionalities.
- **APIs:** Implemented using Golang for sending and pulling messages.
- **Data Storage:** Utilizes [Redis](https://hub.docker.com/r/bitnami/redis/) for efficient data management.
- **Message Delivery:** Pull-based approach for message retrieval.
- **Performance:** Supports over 20 concurrent connections.

## ⚙️ Usage

### Prerequisites
- Ensure Docker is installed and running on your machine.
- go 1.18+

### Install Dependencies
```bash
make pre
```
### Run the System
```bash
docker-compose up -d
```
### Check if it's Running
```bash
curl localhost:8080/ping
```

## 🌐 API Specifications

### Send a Message
- Endpoint: POST /api/send
- Request Body:
  ```json
  {
      "chat": "a1:a2",
      "text": "hello",
      "sender": "a2"
  }
  ```
Response: 204 No Content (Empty)

### Pull Messages
- Endpoint: GET /api/pull
- Request Body:
  ```json
  {
      "chat": "a1:a2",
      "cursor": 0,
      "limit": 2,
      "reverse": true
  }
  ```
  Response example:
   ```json
    {
      "messages": [
          {
              "chat": "a1:a2",
              "text": "good morning",
              "sender": "a2",
              "send_time": 1684770951
          },
          {
              "chat": "a1:a2",
              "text": "hello",
              "sender": "a1",
              "send_time": 1684770116
          }
      ],
      "has_more": true,
      "next_cursor": 2
  }
  ```

## 📚 Documentation
- [HTTP API Definitions](https://github.com/TikTokTechImmersion/assignment_demo_2023/blob/main/idl_http.proto)

## 📄 License
This project is licensed under the MIT License. See [LICENSE](LICENSE) for more information.

## 🙏 Acknowledgements
A special thank you to the TikTok Tech Immersion team for providing the opportunity to work on this project.
