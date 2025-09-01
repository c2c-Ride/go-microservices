# Go Microservices Project

A microservices-based e-commerce application built with Go, featuring gRPC services, GraphQL API, and containerized deployment.

## 🏗️ Architecture

This project implements a microservices architecture with the following components:

### Services
- **Account Service** (`/account`) - User account management with gRPC API
- **Catalog Service** (`/catalog`) - Product catalog management (in development)
- **Order Service** (`/order`) - Order processing (in development)
- **GraphQL Gateway** (`/graphql`) - Unified API gateway using GraphQL

### Technology Stack
- **Language**: Go 1.25.0
- **gRPC**: Inter-service communication
- **GraphQL**: API gateway with gqlgen
- **Database**: PostgreSQL (planned for each service)
- **Containerization**: Docker & Docker Compose
- **Protocol Buffers**: Service contracts

## 📁 Project Structure

```
go-microservices/
├── account/           # Account microservice
│   ├── account.proto  # gRPC service definition
│   ├── server.go      # gRPC server implementation
│   ├── service.go     # Business logic
│   ├── repository.go  # Data access layer
│   └── pb/           # Generated protobuf files
├── catalog/          # Catalog microservice (in development)
├── order/            # Order microservice (in development)
├── graphql/          # GraphQL API gateway
│   ├── schema.graphql # GraphQL schema
│   ├── main.go       # GraphQL server
│   └── generated.go  # Auto-generated resolvers
├── docker-compose.yml # Container orchestration
└── go.mod            # Go module definition
```

## 🚀 Getting Started

### Prerequisites
- Go 1.25.0 or later
- Protocol Buffers compiler (`protoc`)
- Docker and Docker Compose
- PostgreSQL (for database services)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd go-microservices
   ```

2. **Install Go dependencies**
   ```bash
   go mod tidy
   ```

3. **Install Protocol Buffers tools**
   ```bash
   go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
   go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
   ```

4. **Generate protobuf files**
   ```bash
   cd account
   go generate
   ```

### Running the Services

#### Development Mode
```bash
# Start all services with Docker Compose
docker-compose up

# Or run individual services
cd account && go run cmd/main.go
cd graphql && go run main.go
```

#### Production Mode
```bash
# Build and run with Docker
docker-compose up --build
```

## 🔧 Development

### Adding New Services
1. Create a new service directory
2. Define your `.proto` file for gRPC contracts
3. Generate Go code: `go generate`
4. Implement service, repository, and server layers
5. Add to `docker-compose.yml`

### GraphQL Schema Updates
1. Modify `graphql/schema.graphql`
2. Regenerate resolvers: `go run github.com/99designs/gqlgen generate`

### Protocol Buffer Updates
1. Modify `.proto` files
2. Regenerate Go code: `go generate`

## 📊 API Endpoints

### GraphQL Gateway
- **URL**: `http://localhost:8080/graphql`
- **Playground**: `http://localhost:8080/`

### gRPC Services
- **Account Service**: `localhost:50051`
- **Catalog Service**: `localhost:50052` (planned)
- **Order Service**: `localhost:50053` (planned)

## 🗄️ Database Schema

Each microservice will have its own database:
- `account_db` - User accounts
- `catalog_db` - Product catalog
- `order_db` - Orders and transactions

## 🔄 Service Communication

- **Internal**: gRPC for inter-service communication
- **External**: GraphQL API gateway for client applications
- **Data Consistency**: Event-driven architecture (planned)

## 🧪 Testing

```bash
# Run all tests
go test ./...

# Run specific service tests
go test ./account/...
go test ./graphql/...
```

## 📦 Deployment

### Docker
```bash
# Build images
docker-compose build

# Run services
docker-compose up -d
```

### Kubernetes (planned)
- Helm charts for each service
- Service mesh integration
- Horizontal pod autoscaling

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests
5. Submit a pull request

## 📝 License

This project is under development and subject to change.

## 🔮 Roadmap

- [ ] Complete Catalog Service implementation
- [ ] Complete Order Service implementation
- [ ] Add authentication and authorization
- [ ] Implement event sourcing
- [ ] Add monitoring and logging
- [ ] Kubernetes deployment
- [ ] CI/CD pipeline
- [ ] Performance testing

---

**Note**: This project is currently under active development. Some services and features may be incomplete or subject to change.
