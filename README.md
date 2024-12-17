# RequestForge

<p align="center">
  <img src="https://img.shields.io/badge/python-3.11+-blue.svg" alt="Python Version">
  <img src="https://img.shields.io/badge/flask-2.3+-green.svg" alt="Flask Version">
  <img src="https://img.shields.io/badge/bootstrap-5.3+-purple.svg" alt="Bootstrap Version">
  <img src="https://img.shields.io/badge/license-MIT-yellow.svg" alt="License">
</p>

## ✨ Features

- 🔑 API Key Management: Securely store and manage API keys
- 🛠 Request Builder: Create and customize API requests with a user-friendly interface
- 🔄 Workflow Automation: Chain multiple API calls into automated workflows
- 📊 Response Visualization: View and analyze API responses
- 🤝 Team Collaboration: Share API calls and workflows with team members
- 📝 Request History: Track and review past API calls
- 🔔 Webhook Integration: Trigger workflows via webhooks
- 📦 Backup Management: Export and import your configurations

## 🔧 Prerequisites

- Python 3.11 or higher
- pip (Python package installer)
- SQLite3
- Modern web browser with JavaScript enabled

## 📥 Installation

Clone the repository:
```bash
docker pull martian1337/requestforge
```
## 🚀 Usage

Start the container on port 5000:
```bash
docker run martian1337/requestforge
```
OR 

Run the Container with Port Mapping (example with port 8080)
```bash
docker run -p 8080:5000 martian1337/requestforge
```
>[!IMPORTANT]
>The container's server logs will still inform the user to visit the app on port 5000. With this is fact, it's the Docker user's responsibility to keep up with their configured/desired port

2. Access the web interface:
   - Open your browser and navigate to `http://localhost:5000` or `http://localhost:desiredport`
   - Default login credentials:
     - Username: `admin`
     - Password: `password`

3. Basic operations:
   - Create API calls from the dashboard
   - Build workflows by chaining API calls
   - Manage API keys in the settings
   - Set up webhooks for automation

# 📖 API Documentation

## Authentication

RequestForge uses token-based authentication for API access. To obtain an API token:

1. Log in to your account
2. Navigate to API Keys section
3. Generate a new API key

Include the API key in the request header:
```
Authorization: Bearer YOUR_API_KEY
```

## API Endpoints

#### API Calls

##### List API Calls
```
GET /api/v1/calls
```
Returns a list of API calls associated with your account.

Response:
```json
{
  "api_calls": [
    {
      "id": 1,
      "name": "Example Call",
      "url": "https://api.example.com/data",
      "method": "GET",
      "headers": {},
      "created_at": "2024-10-29T10:00:00Z"
    }
  ]
}
```

##### Create API Call
```
POST /api/v1/calls
```
Create a new API call configuration.

Request body:
```json
{
  "name": "New API Call",
  "url": "https://api.example.com/data",
  "method": "POST",
  "headers": {
    "Content-Type": "application/json"
  },
  "body": {
    "key": "value"
  }
}
```

#### Workflows

##### List Workflows
```
GET /api/v1/workflows
```
Returns a list of workflows.

Response:
```json
{
  "workflows": [
    {
      "id": 1,
      "name": "Data Collection",
      "description": "Collect data from multiple sources",
      "steps": ["api_call_1", "api_call_2"],
      "created_at": "2024-10-29T10:00:00Z"
    }
  ]
}
```

##### Execute Workflow
```
POST /api/v1/workflows/{workflow_id}/execute
```
Trigger execution of a specific workflow.

#### Webhooks

##### Register Webhook
```
POST /api/v1/webhooks
```
Register a new webhook for workflow automation.

Request body:
```json
{
  "name": "Data Update Hook",
  "url": "https://your-server.com/webhook",
  "workflow_id": 1
}
```


### Error Responses

The API uses standard HTTP status codes and returns errors in the following format:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Detailed error message"
  }
}
```

Common error codes:
- `401`: Unauthorized - Invalid or missing API key
- `403`: Forbidden - Insufficient permissions
- `404`: Not Found - Resource doesn't exist
- `429`: Too Many Requests - Rate limit exceeded


## 👨‍💻 Continuous Integration

1. Automated Checks:
   - Code style (flake8)
   - Unit tests (pytest)
   - Security scanning
   - Dependencies audit

2. Integration Testing:
   - API endpoint testing
   - Database migrations
   - Authentication flows

3. Deployment:
   - Automated staging deployment
   - Manual production deployment
   - Rollback procedures

## 🔨 Troubleshooting


#### Authentication Issues

1. **Login Failures**
   - **Issue**: Cannot log in with default credentials
   - **Solutions**:
     - Verify database creation
     - Check case sensitivity in username
     - Clear browser cookies and cache

2. **API Key Problems**
   - **Issue**: API requests return 401 errors
   - **Solutions**:
     - Regenerate API key
     - Check header format
     - Verify key hasn't expired
     - Ensure proper permission settings

#### Runtime Errors

1. **Application Won't Start**
   - **Issue**: Server fails to start
   - **Solutions**:
     - Check port availability
     - Verify Python version
     - Look for syntax errors
     - Check environment variables

2. **Workflow Execution Fails**
   - **Issue**: Workflows fail to complete
   - **Solutions**:
     - Check API endpoint availability
     - Verify workflow configuration
     - Check network connectivity
     - Review execution logs


## 🔐 Default Credentials

- Username: `admin`
- Password: `password`

**Important**: Change these credentials immediately after first login!

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⚠️ Security Notice

This application is provided as-is for development and testing purposes. Before deploying in a production environment:

1. Change the default admin credentials to a strong, complex password
2. Enable HTTPS and/or use a reverse proxy
3. Follow security best practices for API key storage
