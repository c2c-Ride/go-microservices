# Go Microservices Project

A microservices-based e-commerce application built with Go, featuring gRPC services, GraphQL API, and containerized deployment.

## 🆕 **Latest Updates (Today's Progress)**

### ✅ **Major Infrastructure Improvements Completed**

#### **Port Conflict Resolution**
- **Fixed critical port conflicts** - All services now use unique ports
- **Account Service**: Main port 8081, Health check port 8082
- **Catalog Service**: Main port 8083, Health check port 8084  
- **Order Service**: Main port 8085, Health check port 8086
- **GraphQL Service**: Main port 8087, Health check port 8088

#### **Docker Security & Best Practices**
- **Non-root user execution** - All services now run as `appuser:appgroup` (UID 1001)
- **Multi-stage builds** - Optimized production images with minimal attack surface
- **Security hardening** - Removed unnecessary build dependencies from runtime images
- **Proper ownership** - Binary files owned by non-root user

#### **Health Check Implementation**
- **Container orchestration ready** - Each service has `/health` endpoint
- **Docker health checks** - Automatic health monitoring with configurable intervals
- **Service dependencies** - Proper startup order based on health status
- **Monitoring endpoints** - Separate ports for health checks to avoid interference

#### **Order Service Development**
- **Complete service structure** - Service, repository, and server layers implemented
- **PostgreSQL integration** - Database schema and repository implementation
- **Transaction support** - ACID compliance for order operations
- **Product relationships** - Order-product mapping with proper normalization

#### **Docker Compose Enhancement**
- **Production-ready configuration** - Proper service dependencies and health checks
- **Volume management** - Persistent data storage for all databases
- **Environment configuration** - Service URLs and database connections
- **Health-based orchestration** - Services wait for dependencies to be healthy

---

## 🏗️ Architecture

This project implements a microservices architecture with the following components:

### Services
- **Account Service** (`/account`) - User account management with gRPC API
- **Catalog Service** (`/catalog`) - Product catalog management with Elasticsearch backend ✅ **COMPLETED**
- **Order Service** (`/order`) - Order processing with PostgreSQL backend ✅ **IN Progress**
- **GraphQL Gateway** (`/graphql`) - Unified API gateway using GraphQL ✅ **ENHANCED**

### Technology Stack
- **Language**: Go 1.25.0
- **gRPC**: Inter-service communication
- **GraphQL**: API gateway with gqlgen
- **Database**: PostgreSQL (account & order services), Elasticsearch (catalog service)
- **Containerization**: Docker & Docker Compose ✅ **PRODUCTION READY**
- **Protocol Buffers**: Service contracts

## 📁 Project Structure

```
go-microservices/
├── account/           # Account microservice ✅ PRODUCTION READY
│   ├── account.proto  # gRPC service definition
│   ├── server.go      # gRPC server implementation
│   ├── service.go     # Business logic
│   ├── repository.go  # Data access layer
│   ├── app.dockerfile # Production Docker image ✅ ENHANCED
│   └── pb/           # Generated protobuf files
├── catalog/          # Catalog microservice ✅ PRODUCTION READY
│   ├── catalog.proto # gRPC service definition
│   ├── server.go     # gRPC server implementation
│   ├── service.go    # Business logic
│   ├── repository.go # Elasticsearch data layer
│   ├── client.go     # gRPC client library
│   ├── app.dockerfile # Production Docker image ✅ ENHANCED
│   └── pb/          # Generated protobuf files
├── order/            # Order microservice ✅ IN PROGRESS
│   ├── order.proto   # gRPC service definition (to be created)
│   ├── server.go     # gRPC server implementation ✅ ENHANCED
│   ├── service.go    # Business logic ✅ IN PROGRESS
│   ├── repository.go # PostgreSQL data layer ✅ COMPLETED
│   ├── app.dockerfile # Production Docker image ✅ ENHANCED
│   └── up.sql       # Database schema
├── graphql/          # GraphQL API gateway ✅ ENHANCED
│   ├── schema.graphql # GraphQL schema
│   ├── main.go       # GraphQL server ✅ ENHANCED
│   ├── app.dockerfile # Production Docker image ✅ NEW
│   └── generated.go  # Auto-generated resolvers
├── docker-compose.yml # Container orchestration ✅ PRODUCTION READY
└── go.mod            # Go module definition
```

## 🚀 Getting Started

### Prerequisites
- Go 1.25.0 or later
- Protocol Buffers compiler (`protoc`)
- Docker and Docker Compose ✅ **ENHANCED**
- PostgreSQL (for account & order services)
- Elasticsearch (for catalog service)

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
   # For account service
   cd account
   go generate
   
   # For catalog service
   cd ../catalog
   go generate
   ```

### Running the Services

#### **Production-Ready Docker Deployment** ✅ **NEW**
```bash
# Start all services with health checks and proper orchestration
docker-compose up --build

# View service status and health
docker-compose ps
docker-compose logs -f [service-name]

# Scale services (when implemented)
docker-compose up --scale order=3
```

#### Development Mode
```bash
# Start all services with Docker Compose
docker-compose up

# Or run individual services
cd account && go run cmd/account/main.go
cd catalog && go run cmd/catalog/main.go
cd order && go run cmd/order/main.go
cd graphql && go run main.go
```

## 🔧 Development

### **New Development Workflow** ✅ **ENHANCED**
1. **Service Development**: Each service has its own Docker image with health checks
2. **Database Integration**: Proper schema management with `up.sql` files
3. **Health Monitoring**: Built-in health endpoints for container orchestration
4. **Security**: Non-root execution and minimal attack surface

### Adding New Services
1. Create a new service directory
2. Define your `.proto` file for gRPC contracts
3. Generate Go code: `go generate`
4. Implement service, repository, and server layers
5. Add to `docker-compose.yml` with health checks
6. Create production-ready Docker image

### GraphQL Schema Updates
1. Modify `graphql/schema.graphql`
2. Regenerate resolvers: `go run github.com/99designs/gqlgen generate`

### Protocol Buffer Updates
1. Modify `.proto` files
2. Regenerate Go code: `go generate`

## 📊 API Endpoints

### **Updated Service Ports** ✅ **NEW**
- **Account Service**: `localhost:8081` (gRPC), `localhost:8082` (Health)
- **Catalog Service**: `localhost:8083` (gRPC), `localhost:8084` (Health)
- **Order Service**: `localhost:8085` (gRPC), `localhost:8086` (Health)
- **GraphQL Gateway**: `localhost:8087` (API), `localhost:8088` (Health)

### GraphQL Gateway
- **URL**: `http://localhost:8087/graphql` ✅ **UPDATED**
- **Playground**: `http://localhost:8087/playground` ✅ **UPDATED**

### gRPC Services
- **Account Service**: `localhost:8081` ✅ **UPDATED**
- **Catalog Service**: `localhost:8083` ✅ **UPDATED**
- **Order Service**: `localhost:8085` ✅ **NEW**

## 🗄️ Database Schema

Each microservice has its own database with proper health monitoring:
- `account_db` - User accounts (PostgreSQL) ✅ **HEALTH MONITORED**
- `catalog_db` - Product catalog (Elasticsearch) ✅ **HEALTH MONITORED**
- `order_db` - Orders and transactions (PostgreSQL) ✅ **NEW & HEALTH MONITORED**

## 🔄 Service Communication

- **Internal**: gRPC for inter-service communication ✅ **ENHANCED**
- **External**: GraphQL API gateway for client applications ✅ **ENHANCED**
- **Health Monitoring**: Built-in health checks for orchestration ✅ **NEW**
- **Data Consistency**: Transaction-based order processing ✅ **NEW**

## 🧪 Testing

```bash
# Run all tests
go test ./...

# Run specific service tests
go test ./account/...
go test ./catalog/...
go test ./order/... ✅ **NEW**
go test ./graphql/...

# Test health endpoints
curl http://localhost:8082/health  # Account
curl http://localhost:8084/health  # Catalog
curl http://localhost:8086/health  # Order
curl http://localhost:8088/health  # GraphQL
```

## 📦 Deployment

### **Production-Ready Docker** ✅ **ENHANCED**
```bash
# Build optimized production images
docker-compose build

# Run with health monitoring
docker-compose up -d

# Monitor service health
docker-compose ps
docker-compose logs -f [service-name]

# Scale services (when implemented)
docker-compose up --scale order=3
```

### **Health Check Monitoring** ✅ **NEW**
- **Automatic health monitoring** every 30 seconds
- **Service dependency management** - services wait for healthy dependencies
- **Container restart policies** based on health status
- **Production-ready orchestration** with proper startup sequences

### Kubernetes (planned)
- Helm charts for each service
- Service mesh integration
- Horizontal pod autoscaling
- **Health check integration** ✅ **READY**

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. **Add health checks** for new services ✅ **REQUIRED**
5. **Use non-root users** in Docker images ✅ **REQUIRED**
6. **Test with Docker Compose** before submitting ✅ **REQUIRED**
7. Submit a pull request

## 📝 License

This project is under development and subject to change.

## 🔮 Roadmap

- [x] Complete Catalog Service implementation ✅
- [ ] **Complete Order Service implementation** ✅ **IN PROGRESS**
- [x] **Fix Docker port conflicts** ✅ **COMPLETED TODAY**
- [x] **Implement health checks** ✅ **COMPLETED TODAY**
- [x] **Security hardening** ✅ **COMPLETED TODAY**
- [x] **Production-ready Docker images** ✅ **COMPLETED TODAY**
- [ ] Add monitoring and logging
- [ ] **Kubernetes deployment** ✅ **READY FOR IMPLEMENTATION**
- [ ] **Service mesh integration** ✅ **HEALTH CHECKS READY**

## 🎯 **Today's Major Achievements**

### **Infrastructure & DevOps**
- ✅ **Eliminated port conflicts** - All services can now run simultaneously
- ✅ **Production-ready Docker images** - Security hardened with non-root users
- ✅ **Health check system** - Container orchestration ready
- ✅ **Service dependency management** - Proper startup sequences

### **Order Service Development**
- ✅ **Complete service architecture** - Service, repository, and server layers
- ✅ **PostgreSQL integration** - Transaction-based order processing
- ✅ **Product relationship management** - Normalized order-product structure
- ✅ **Docker containerization** - Production-ready deployment

### **Security & Best Practices**
- ✅ **Non-root execution** - All services run as unprivileged users
- ✅ **Minimal attack surface** - Multi-stage builds with essential dependencies only
- ✅ **Health monitoring** - Built-in monitoring for production environments
- ✅ **Proper service isolation** - Each service has dedicated ports and health endpoints

---

**Note**: This project is currently under active development. The Account and Catalog services are fully implemented, with Order service partially developed and additional features in development.
