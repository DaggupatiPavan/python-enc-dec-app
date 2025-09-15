# Encryption/Decryption API

A simple low-code/no-code Python FastAPI application for encryption and decryption operations with Docker support and Swagger UI.

## Features

- **Multiple Encryption Methods**: Base64, Fernet, and AES-like encryption
- **RESTful API**: Clean and intuitive API endpoints
- **Swagger UI**: Interactive API documentation at `/docs`
- **Docker Support**: Easy containerization and deployment
- **No-Code Friendly**: Simple JSON requests and responses

## Quick Start

### Using Docker Compose (Recommended)

1. Clone or download the project
2. Navigate to the project directory
3. Run with Docker Compose:

```bash
docker-compose up --build
```

4. Access the API at `http://localhost:8000`
5. View Swagger UI at `http://localhost:8000/docs`

### Using Docker

1. Build the Docker image:
```bash
docker build -t enc-dec-api .
```

2. Run the container:
```bash
docker run -p 8000:8000 enc-dec-api
```

### Running Locally

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Run the application:
```bash
python main.py
```

## API Endpoints

### Base URL: `http://localhost:8000`

#### GET `/`
Root endpoint with API information.

#### GET `/methods`
Get list of available encryption/decryption methods.

#### POST `/encrypt`
Encrypt text using specified method.

**Request Body:**
```json
{
  "text": "Hello World",
  "method": "base64",
  "secret_key": "optional-key-for-aes"
}
```

**Response:**
```json
{
  "original_text": "Hello World",
  "encrypted_text": "SGVsbG8gV29ybGQ=",
  "method": "base64",
  "success": true,
  "message": "Text encrypted successfully"
}
```

#### POST `/decrypt`
Decrypt text using specified method.

**Request Body:**
```json
{
  "encrypted_text": "SGVsbG8gV29ybGQ=",
  "method": "base64",
  "secret_key": "optional-key-for-aes"
}
```

**Response:**
```json
{
  "encrypted_text": "SGVsbG8gV29ybGQ=",
  "decrypted_text": "Hello World",
  "method": "base64",
  "success": true,
  "message": "Text decrypted successfully"
}
```

## Encryption Methods

### Base64
- **Description**: Simple base64 encoding/decoding
- **Requires Key**: No
- **Use Case**: Basic encoding, not secure encryption

### Fernet
- **Description**: Symmetric encryption using Fernet
- **Requires Key**: No (auto-generated)
- **Use Case**: Secure encryption for sensitive data

### AES
- **Description**: Simple AES-like encryption with custom key
- **Requires Key**: Yes
- **Use Case**: Custom key-based encryption

## Example Usage with curl

### Encrypt with Base64
```bash
curl -X POST "http://localhost:8000/encrypt" \
     -H "Content-Type: application/json" \
     -d '{"text": "Hello World", "method": "base64"}'
```

### Decrypt with Base64
```bash
curl -X POST "http://localhost:8000/decrypt" \
     -H "Content-Type: application/json" \
     -d '{"encrypted_text": "SGVsbG8gV29ybGQ=", "method": "base64"}'
```

### Encrypt with AES
```bash
curl -X POST "http://localhost:8000/encrypt" \
     -H "Content-Type: application/json" \
     -d '{"text": "Secret Message", "method": "aes", "secret_key": "my-secret-key"}'
```

## Swagger UI

Access the interactive API documentation at:
- **Local**: `http://localhost:8000/docs`
- **Docker**: `http://localhost:8000/docs`

The Swagger UI provides:
- Interactive API testing
- Request/response schemas
- Try-it-out functionality
- Detailed endpoint documentation

## Development

### Project Structure
```
python-enc-dec-app/
├── main.py              # FastAPI application
├── requirements.txt     # Python dependencies
├── Dockerfile          # Docker configuration
├── docker-compose.yml  # Docker Compose configuration
└── README.md          # This file
```

### Adding New Encryption Methods

1. Add the method to the `/methods` endpoint
2. Implement encryption logic in `/encrypt` endpoint
3. Implement decryption logic in `/decrypt` endpoint
4. Update the documentation

## Security Notes

- This is a demo application for educational purposes
- For production use, consider:
  - Using proper key management
  - Implementing rate limiting
  - Adding authentication/authorization
  - Using HTTPS
  - Proper error handling and logging

## License

MIT License - feel free to use and modify for your projects.