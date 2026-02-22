# MoogzTrade Web Demo

A high-end, professional web demonstration of the MoogzTrade Security-First Trading Platform SDK. Built with FastAPI backend and modern frontend technologies, this demo showcases the full capabilities of the SDK in a production-ready environment.

## 🚀 Features

### Core Functionality
- **Security Lab**: Real-time AES-256 encryption with HMAC verification
- **AI Tooling**: Interactive agent console with simulated LLM responses
- **Market Data**: Live market quotes with interactive charts
- **Portfolio Dashboard**: Comprehensive portfolio analytics and allocation visualization
- **Module Explorer**: Interactive showcase of individual SDK modules
- **System Health**: Real-time monitoring of all system components

### Technical Features
- **Demo Mode**: Safe for public hosting with mock data
- **Responsive Design**: Mobile-first approach with Tailwind CSS
- **Fintech Dark Theme**: Professional appearance with neon accents
- **Real-time Updates**: Live data visualization and status monitoring
- **Production Ready**: Docker deployment with security best practices

## 📋 Prerequisites

- Python 3.11+
- Node.js 16+ (for development tools)
- Git

## 🛠️ Installation & Setup

### 1. Clone the Repository
```bash
git clone <repository-url>
cd moogweb
```

### 2. Set Up Python Environment
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Verify SDK Integration
Ensure the MoogzTrade SDK is available in the `moogz_trade_sdk` directory:
```bash
ls moogz_trade_sdk/
# Should show: __init__.py, modules/, core/, etc.
```

### 4. Run the Application
```bash
# Development mode
python main.py

# Or using uvicorn directly
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### 5. Access the Demo
Open your browser and navigate to:
- **Main Application**: http://localhost:8000
- **API Documentation**: http://localhost:8000/api/docs
- **Health Check**: http://localhost:8000/api/health

## 🌐 Deployment Options

### Option 1: Docker (Recommended)
```bash
# Build the Docker image
docker build -t moogztrade-demo .

# Run the container
docker run -p 8000:8000 moogztrade-demo

# Or with Docker Compose
docker-compose up -d
```

### Option 2: Heroku
```bash
# Install Heroku CLI and login
heroku login

# Create Heroku app
heroku create your-app-name

# Set environment variables
heroku config:set DEMO_MODE=true

# Deploy
git push heroku main
```

### Option 3: IONOS Cloud
```bash
# Using the provided Procfile
# Deploy via IONOS Cloud Panel or CLI
# Ensure PORT environment variable is set
```

### Option 4: Traditional VPS
```bash
# Install dependencies
sudo apt update
sudo apt install python3 python3-pip nginx

# Set up application
pip3 install -r requirements.txt
gunicorn main:app -w 4 -k uvicorn.workers.UvicornWorker --bind 0.0.0.0:8000

# Configure Nginx reverse proxy
# (See nginx configuration below)
```

## ⚙️ Configuration

### Environment Variables
```bash
# Demo Mode (recommended for public hosting)
DEMO_MODE=true

# Production Mode (requires real API keys)
DEMO_MODE=false

# Server Configuration
PORT=8000
HOST=0.0.0.0

# Logging
LOG_LEVEL=INFO
```

### Nginx Configuration (Optional)
```nginx
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## 📊 API Endpoints

### Core Endpoints
- `GET /` - Main application interface
- `GET /api/health` - System health check
- `POST /api/encrypt` - AES-256 encryption
- `POST /api/market-data` - Market data retrieval
- `POST /api/portfolio` - Portfolio information
- `POST /api/agent` - AI agent interaction
- `POST /api/module-demo` - Module demonstrations
- `GET /api/modules` - Available modules list
- `GET /api/system-health` - System health status

### Example API Usage
```bash
# Health Check
curl http://localhost:8000/api/health

# Encrypt Data
curl -X POST http://localhost:8000/api/encrypt \
  -H "Content-Type: application/json" \
  -d '{"plaintext": "Hello World", "demo_mode": true}'

# Get Market Data
curl -X POST http://localhost:8000/api/market-data \
  -H "Content-Type: application/json" \
  -d '{"symbol": "AAPL", "demo_mode": true}'
```

## 🎨 Customization

### Branding
Update the following files to customize branding:
- `templates/index.html` - Logo, colors, and text
- `static/app.js` - Application behavior
- `main.py` - API responses and configuration

### Theme Customization
The application uses a Fintech Dark theme with neon accents. Modify the CSS in `templates/index.html`:
```css
/* Primary accent colors */
.neon-accent {
    background: linear-gradient(45deg, #00ff88, #00ccff);
}

/* Glass effect for panels */
.glass-effect {
    background: rgba(15, 23, 42, 0.8);
    backdrop-filter: blur(10px);
}
```

### Adding New Modules
1. Update the modules list in `main.py` (`/api/modules` endpoint)
2. Add module demo logic in `/api/module-demo` endpoint
3. Update the frontend in `static/app.js` (`displayModules` function)

## 🔒 Security Considerations

### Demo Mode
- **Enabled by default** for public safety
- Uses mock data instead of real market information
- No external API calls required
- Safe for public hosting

### Production Mode
- Requires valid API keys and credentials
- Implements real encryption and market data
- Ensure proper security measures
- Use HTTPS in production

### Security Features
- Input validation and sanitization
- Rate limiting capabilities
- Secure headers configuration
- Non-root Docker user
- Environment variable configuration

## 🐛 Troubleshooting

### Common Issues

#### SDK Import Errors
```bash
# Ensure SDK is in the correct path
ls moogz_trade_sdk/__init__.py

# Check Python path
export PYTHONPATH=$PYTHONPATH:/path/to/moogweb
```

#### Port Already in Use
```bash
# Find and kill process using port 8000
lsof -i :8000
kill -9 <PID>

# Or use different port
uvicorn main:app --port 8080
```

#### Permission Issues
```bash
# Fix file permissions
chmod +x main.py
sudo chown -R $USER:$USER /path/to/moogweb
```

### Debug Mode
Enable debug logging:
```bash
export LOG_LEVEL=DEBUG
python main.py
```

## 📈 Performance Optimization

### Production Tuning
```bash
# Use Gunicorn with multiple workers
gunicorn main:app -w 4 -k uvicorn.workers.UvicornWorker --bind 0.0.0.0:8000

# Enable caching headers
# Add to main.py or reverse proxy
```

### Monitoring
- Health checks at `/api/health`
- System monitoring at `/api/system-health`
- Application logs for debugging

## 🤝 Support

### Documentation
- **API Docs**: http://localhost:8000/api/docs
- **ReDoc**: http://localhost:8000/api/redoc

### Getting Help
1. Check the troubleshooting section above
2. Review the API documentation
3. Check application logs for errors
4. Verify environment configuration

## 📄 License

This demo is part of the MoogzTrade SDK package. Please refer to the main SDK license for usage terms and conditions.

## 🚀 Next Steps

1. **Explore the Demo**: Navigate through all sections to understand capabilities
2. **Test the APIs**: Use the provided endpoints to integrate with your applications
3. **Purchase the SDK**: Click the "Buy Now / View on Acquire" button for full access
4. **Customize**: Modify the demo to match your branding and requirements
5. **Deploy**: Use the provided deployment options for production hosting

---

**Built with ❤️ by the MoogzTrade Team**

*For technical support or inquiries, please visit our website or contact us through the Acquire platform.*
