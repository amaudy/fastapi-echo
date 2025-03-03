# FastAPI Echo Service

A simple echo service built with FastAPI that returns information about incoming requests. This service is designed for testing, debugging, and demonstrating HTTP requests and responses.

## Features

- **Echo Endpoint**: Returns details about any request made to any path
- **Error Demonstration**: Endpoints to simulate various HTTP error responses (400, 401, 403, 404, 500, 503)
- **Request Tracing**: Generates correlation IDs for request tracing
- **Performance Metrics**: Measures and returns processing time for each request
- **Structured Logging**: JSON-formatted logs with request details

## Getting Started

### Prerequisites

- Python 3.13+
- Docker (optional)

### Installation

1. Clone the repository:
   ```
   git clone https://github.com/yourusername/fastapi-echo.git
   cd fastapi-echo/echo-service
   ```

2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

3. Run the service:
   ```
   python main.py
   ```

   Or with uvicorn directly:
   ```
   uvicorn main:app --host 0.0.0.0 --port 8000
   ```

### Using Docker

1. Build the Docker image:
   ```
   docker build -t fastapi-echo .
   ```

2. Run the container:
   ```
   docker run -p 8000:8000 fastapi-echo
   ```

## API Usage

### Echo Endpoint

Make any HTTP request to any path, and the service will echo back details about your request:

```bash
# Example GET request
curl http://localhost:8000/any/path/you/want

# Example POST request with JSON body
curl -X POST \
  http://localhost:8000/api/data \
  -H "Content-Type: application/json" \
  -d '{"key": "value"}'
```

Response format:
```json
{
  "path": "/the/requested/path",
  "method": "HTTP_METHOD",
  "headers": {
    "header1": "value1",
    "header2": "value2"
  },
  "body": "request body or null"
}
```

### Error Demonstration Endpoints

Test different HTTP error responses:

- `GET /error/400` - Bad Request
- `GET /error/401` - Unauthorized
- `GET /error/403` - Forbidden
- `GET /error/404` - Not Found
- `GET /error/500` - Internal Server Error
- `GET /error/503` - Service Unavailable

## Response Headers

Each response includes:

- `X-Process-Time`: Time taken to process the request (in seconds)
- `X-Correlation-ID`: Unique ID for request tracing

## Logging

The service logs all requests in JSON format with the following information:
- Request path
- HTTP method
- Status code
- Response time
- Correlation ID
- Error details (if applicable)

## Docker Hub

The Docker image for this service is automatically built and published to Docker Hub using GitHub Actions.

### Image Tags

- `latest` - Built from the main branch
- `vx.x.x` - Built from version tags (e.g., v1.0.0)

### GitHub Actions Workflow

The repository includes a GitHub Actions workflow that:
1. Builds the Docker image
2. Pushes it to Docker Hub when changes are pushed to any branch or when a version tag is created
3. Uses semantic versioning for tag-based releases

### Required Secrets

To enable the GitHub Actions workflow to push to Docker Hub, you need to set up:

1. Environment variable:
   - `DOCKER_HUB_USERNAME`: Your Docker Hub username

2. GitHub secret:
   - `DOCKER_HUB_TOKEN`: Your Docker Hub access token (not your password)

#### Creating a Docker Hub Access Token

1. Log in to [Docker Hub](https://hub.docker.com/)
2. Go to Account Settings → Security
3. Click "New Access Token"
4. Give it a name (e.g., "GitHub Actions")
5. Copy the token and add it as a secret in your GitHub repository

## License

[MIT License](LICENSE)
