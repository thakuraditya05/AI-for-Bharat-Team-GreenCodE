# GenAI Content Creator

A full-stack AI-powered content creation platform for multi-platform social media management, built on the MERN stack (MongoDB, Express, React, Node.js).

## Overview

GenAI Content Creator empowers content creators with intelligent tools for social media management across Instagram, YouTube, Twitter/X, Threads, Reddit, Telegram, and Discord. The platform combines real-time trend analysis, AI-powered content generation, and strategic scheduling to optimize content performance.

## Key Features

### 🎯 Multi-Platform Dashboard
- Unified view of all connected social media accounts
- Real-time metrics and engagement tracking
- Secure credential storage with AES-256 encryption
- Auto-refresh every 5 minutes

### 📈 Real-Time Trend Intelligence
- Trending hashtags and keywords across all platforms
- Viral content detection (songs, memes, formats)
- Engagement score ranking
- 15-minute data refresh cycle
- Intelligent caching to minimize API costs

### ✍️ AI Content Script Generation
- Complete scripts for YouTube videos, Shorts, and blogs
- Structured content with hooks, body, and conclusions
- Automatic source citation
- Natural keyword incorporation
- Generation time under 30 seconds

### 🎨 Thumbnail & Title Optimization
- Platform-specific title generation (5+ variations)
- CTR-optimized suggestions
- Visual style recommendations with references
- Adaptive captions for each platform
- Niche-specific performance insights

### 📅 Intelligent Scheduling
- Calendar interface for content planning
- Platform-specific optimal posting times
- Automated posting or notifications
- Schedule up to 90 days in advance
- Dynamic recommendations based on audience patterns

### 💡 AI-Powered Idea Generation
- 10+ unique content ideas per request
- Trend-based suggestions
- Personalized to your content history
- Niche filtering
- Complete with descriptions and hooks

### 📧 Automated Email Management
- AI-generated email drafts
- Template library for reuse
- Workflow automation (collaborations, sponsorships, fan responses)
- Email logging and tracking
- Context-aware generation

### 📁 Project-Based Organization
- Isolated project threads for campaigns
- Platform-specific content streams
- Chronological content display
- Rich text support (Markdown, code blocks)
- Advanced search and filtering

## Technology Stack

### Frontend
- React 18+ with hooks
- Redux Toolkit / React Context API
- Material-UI / Tailwind CSS
- Socket.io-client for real-time updates
- Axios with interceptors

### Backend
- Node.js 18+ with Express.js
- JWT authentication with refresh tokens
- Socket.io for WebSocket connections
- Joi / express-validator
- express-rate-limit (100 req/min per user)

### Database
- MongoDB 6+ with Mongoose ODM
- Indexed queries for performance
- TTL indexes for cache and sessions
- 365-day content history retention

### AI/ML
- OpenAI GPT-4 for content generation
- LangChain for complex workflows
- Python FastAPI microservice
- TensorFlow/Keras for trend prediction
- scikit-learn for clustering
- pandas/NumPy for data processing

### Data Acquisition
- Official APIs: YouTube Data API, Reddit API, Twitter API
- Web scraping: BeautifulSoup4, Selenium
- Redis caching (10-15 min TTL)
- Proxy rotation for resilience

### DevOps
- Docker containerization
- GitHub Actions CI/CD
- AWS / Google Cloud Platform
- PM2 / CloudWatch monitoring

## Architecture

The application follows a modular microservices-inspired design with clear separation of concerns:

```
Frontend Layer → Backend API → Business Logic Layer → AI/ML Layer
                                                    ↓
                              Data Acquisition ← External APIs
                                     ↓
                              MongoDB Database
```

### Core Services

- **Authentication Service**: JWT-based secure session management
- **Dashboard Service**: Platform connection and data aggregation
- **Trend Intelligence Engine**: Real-time trend analysis and ML predictions
- **AI Scripting Suite**: Content generation with OpenAI integration
- **Thumbnail Generator**: Title optimization and visual recommendations
- **Scheduler Service**: Optimal posting time calculation and automation
- **Idea Generator**: Trend-based content suggestions
- **Email Manager**: Automated email generation and sending
- **Project Manager**: Content organization and search

## Getting Started

### Prerequisites

- Node.js 18+
- MongoDB 6+
- Python 3.9+ (for ML service)
- Redis (for caching)
- OpenAI API key

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd genai-content-creator

# Install backend dependencies
npm install

# Install frontend dependencies
cd client
npm install
cd ..

# Install Python ML service dependencies
cd ml-service
pip install -r requirements.txt
cd ..

# Set up environment variables
cp .env.example .env
# Edit .env with your API keys and configuration
```

### Environment Variables

Create a `.env` file in the root directory:

```env
# Server
PORT=5000
NODE_ENV=development

# Database
MONGODB_URI=mongodb://localhost:27017/genai-content-creator

# Redis
REDIS_URL=redis://localhost:6379

# Authentication
JWT_SECRET=your-jwt-secret
JWT_REFRESH_SECRET=your-refresh-secret
JWT_EXPIRE=15m
JWT_REFRESH_EXPIRE=7d

# OpenAI
OPENAI_API_KEY=your-openai-api-key

# Platform APIs
YOUTUBE_API_KEY=your-youtube-api-key
TWITTER_API_KEY=your-twitter-api-key
REDDIT_CLIENT_ID=your-reddit-client-id
REDDIT_CLIENT_SECRET=your-reddit-client-secret

# Email Service
EMAIL_SERVICE=sendgrid
EMAIL_API_KEY=your-email-api-key
EMAIL_FROM=noreply@yourapp.com

# Python ML Service
ML_SERVICE_URL=http://localhost:8000
```

### Running the Application

```bash
# Start MongoDB
mongod

# Start Redis
redis-server

# Start Python ML service
cd ml-service
uvicorn main:app --reload --port 8000
cd ..

# Start backend server
npm run dev

# Start frontend (in a new terminal)
cd client
npm start
```

The application will be available at:
- Frontend: http://localhost:3000
- Backend API: http://localhost:5000
- ML Service: http://localhost:8000

## API Documentation

### Authentication

```
POST   /api/auth/register    - Register new user
POST   /api/auth/login       - Login user
POST   /api/auth/logout      - Logout user
POST   /api/auth/refresh-token - Refresh access token
GET    /api/auth/me          - Get current user
```

### Dashboard

```
GET    /api/dashboard/overview           - Get dashboard overview
GET    /api/dashboard/platforms          - Get all platform connections
GET    /api/dashboard/metrics/:platform  - Get platform-specific metrics
POST   /api/dashboard/sync/:platform     - Sync platform data
```

### Trends

```
GET    /api/trends/hashtags              - Get trending hashtags
GET    /api/trends/keywords              - Get trending keywords
GET    /api/trends/viral-content         - Get viral content
GET    /api/trends/recommendations       - Get personalized recommendations
POST   /api/trends/refresh               - Force refresh trend data
```

### AI Content Generation

```
POST   /api/ai/generate-script           - Generate content script
POST   /api/ai/generate-title            - Generate optimized titles
POST   /api/ai/generate-description      - Generate descriptions
POST   /api/ai/generate-ideas            - Generate content ideas
GET    /api/ai/generation-history        - Get generation history
```

### Scheduling

```
GET    /api/schedule/calendar            - Get calendar view
POST   /api/schedule/create              - Create scheduled post
PUT    /api/schedule/:id                 - Update scheduled post
DELETE /api/schedule/:id                 - Delete scheduled post
GET    /api/schedule/optimal-times       - Get optimal posting times
```

### Projects

```
GET    /api/projects                     - List all projects
POST   /api/projects/create              - Create new project
GET    /api/projects/:id                 - Get project details
PUT    /api/projects/:id                 - Update project
DELETE /api/projects/:id                 - Delete project
GET    /api/projects/:id/content         - Get project content
POST   /api/projects/:id/content         - Add content to project
GET    /api/content/search               - Search content
```

### Email

```
POST   /api/email/generate               - Generate email draft
POST   /api/email/send                   - Send email
GET    /api/email/templates              - Get email templates
POST   /api/email/templates/create       - Create email template
GET    /api/email/history                - Get email history
```

## Testing

The project uses a dual testing approach:

### Unit Tests
```bash
# Run all unit tests
npm test

# Run with coverage
npm run test:coverage

# Run frontend tests
cd client && npm test

# Run backend tests
npm run test:backend
```

### Property-Based Tests
```bash
# Run property-based tests
npm run test:properties

# Run with specific seed for reproducibility
npm run test:properties -- --seed=12345
```

Testing frameworks:
- **JavaScript/TypeScript**: Jest + fast-check
- **Python ML Service**: pytest + Hypothesis

Coverage targets:
- Minimum 80% overall coverage
- 100% coverage for critical paths (auth, payments, persistence)

## Security

- AES-256 encryption for stored credentials
- JWT with refresh token rotation
- Rate limiting (100 requests/min per user)
- Input validation on all endpoints
- CORS configuration
- Helmet.js security headers
- MongoDB injection prevention
- XSS and CSRF protection

## Performance

- Dashboard load: < 500ms
- Trend data (cached): < 1s
- Trend data (fresh): < 5s
- AI generation: < 30s
- Search: < 300ms
- Target: 1000 concurrent users

## Error Handling

All errors follow a consistent format:

```json
{
  "error": {
    "code": "RESOURCE_NOT_FOUND",
    "message": "The requested project does not exist",
    "suggestions": ["Check the project ID", "View all projects at /api/projects"],
    "timestamp": "2024-01-15T10:30:00Z"
  }
}
```

Retry strategies:
- Exponential backoff for external APIs (3 attempts max)
- Circuit breaker for repeatedly failing services
- Graceful degradation when services are unavailable

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For issues and questions:
- GitHub Issues: [repository-url]/issues
- Documentation: [documentation-url]
- Email: support@yourapp.com

## Roadmap

- [ ] Mobile app (React Native)
- [ ] Additional platform integrations (TikTok, LinkedIn)
- [ ] Advanced analytics dashboard
- [ ] Team collaboration features
- [ ] White-label solutions
- [ ] API access for third-party integrations
- [ ] Video editing integration
- [ ] A/B testing for titles and thumbnails

---

Built with ❤️ for content creators worldwide
