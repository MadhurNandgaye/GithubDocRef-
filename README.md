Here’s a complete Go backend REST API project tailored for your Logic App Monitor—file by file. It’s built using Gin framework and follows a clean folder structure with separation of responsibilities.

⸻

🗂 Project Structure

logic-monitor-api/
├── cmd/
│   └── server/
│       └── main.go
├── internal/
│   ├── config/
│   │   └── config.go
│   ├── api/
│   │   ├── handlers.go
│   │   └── routes.go
│   ├── logic/
│   │   └── monitor.go
│   ├── model/
│   │   └── status.go
│   └── svc/
│       └── servicecontext.go
├── go.mod
└── go.sum

This approach is based on layered project structures recommended in Go best practices  ￼.

⸻

📄 File-by-File Code

1. cmd/server/main.go

package main

import "logic-monitor-api/internal/api"

func main() {
    r := api.SetupRouter()
    r.Run(":8080") // starts server
}


⸻

2. internal/config/config.go

package config

import "os"

type Config struct {
    InternalURL string
    ExternalURL string
}

func Load() *Config {
    return &Config{
        InternalURL: os.Getenv("INTERNAL_URL"),
        ExternalURL: os.Getenv("EXTERNAL_URL"),
    }
}


⸻

3. internal/model/status.go

package model

type EndpointStatus string

const (
    Green  EndpointStatus = "Green"
    Yellow EndpointStatus = "Yellow"
    Red    EndpointStatus = "Red"
)

type StatusResponse struct {
    Endpoint string         `json:"endpoint"`
    Status   EndpointStatus `json:"status"`
}


⸻

4. internal/svc/servicecontext.go

package svc

import "logic-monitor-api/internal/config"

type ServiceContext struct {
    Config *config.Config
}

func NewServiceContext(cfg *config.Config) *ServiceContext {
    return &ServiceContext{Config: cfg}
}


⸻

5. internal/logic/monitor.go

package logic

import (
    "logic-monitor-api/internal/model"
    "net/http"
    "time"
)

func CheckEndpoint(name, url string) model.StatusResponse {
    client := http.Client{Timeout: 3 * time.Second}
    resp, err := client.Get(url)
    status := model.Green
    if err != nil || resp.StatusCode >= 500 {
        status = model.Red
    } else if resp.StatusCode >= 400 {
        status = model.Yellow
    }
    return model.StatusResponse{Endpoint: name, Status: status}
}


⸻

6. internal/api/routes.go

package api

import (
    "logic-monitor-api/internal/api/handlers"

    "github.com/gin-gonic/gin"
)

func SetupRouter() *gin.Engine {
    r := gin.Default()
    v1 := r.Group("/api/v1")
    {
        v1.GET("/statuses", handlers.GetStatuses)
    }
    return r
}


⸻

7. internal/api/handlers.go

package api

import (
    "logic-monitor-api/internal/config"
    "logic-monitor-api/internal/logic"
    "logic-monitor-api/internal/model"
    "logic-monitor-api/internal/svc"

    "github.com/gin-gonic/gin"
)

func GetStatuses(c *gin.Context) {
    cfg := config.Load()
    sctx := svc.NewServiceContext(cfg)

    statuses := []model.StatusResponse{
        logic.CheckEndpoint("internal", sctx.Config.InternalURL),
        logic.CheckEndpoint("external", sctx.Config.ExternalURL),
    }
    c.JSON(200, statuses)
}


⸻

8. go.mod

module logic-monitor-api

go 1.20

require github.com/gin-gonic/gin v1.9.0


⸻

🚀 Usage
	1.	Setup environment variables:

set INTERNAL_URL=http://internal-service/health
set EXTERNAL_URL=https://public-api/health


	2.	Run:

go mod tidy
go run cmd/server/main.go


	3.	Test:

GET http://localhost:8080/api/v1/statuses

Response:

[
  {"endpoint":"internal","status":"Green"},
  {"endpoint":"external","status":"Yellow"}
]



⸻

📚 Notes:
	•	You can extend it with databases, email integration, or self-healing actions.
	•	The modular structure (cfg, svc, logic, api) follows best practices for maintainability  ￼ ￼.
	•	For more advanced features, integrate with a scheduler or job queue, and extend monitor.go to trigger self-heal APIs.

⸻

Let me know if you’d like me to add file upload endpoints, alerting integration, or database persistence next!
