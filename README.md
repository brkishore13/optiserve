# OptiServe - Performance Analysis Platform

A comprehensive microservice performance analysis platform that analyzes code repositories and tests running microservices to provide detailed performance improvement recommendations.

## Features

### 🔍 Static Code Analysis
- **Multi-language support**: Java, Python, Node.js, Go
- **Repository analysis**: Clone and analyze GitHub repositories
- **Smart recommendations**: Database, memory, configuration, and network optimizations
- **Performance scoring**: 0-100 performance rating with detailed breakdowns

### 🌐 Live Service Analysis
- **Microservice testing**: Test any running service endpoint
- **Performance metrics**: Response time consistency and load testing
- **Security analysis**: HTTPS validation, security headers, certificate verification
- **Real-time monitoring**: Live performance and availability testing

### 📊 Comprehensive Reporting
- **Analysis history**: View and filter all past analyses
- **Performance reports**: Detailed insights and trends
- **Settings management**: Configurable analysis parameters
- **Progress tracking**: Real-time analysis progress with step-by-step updates

## Quick Start

### Prerequisites

- **Node.js** 18 or higher
- **PostgreSQL** (or use included Neon database configuration)
- **Git** for repository cloning

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd optiserve
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   # Copy the example environment file
   cp .env.example .env
   
   # Edit .env with your database URL
   # DATABASE_URL=postgresql://username:password@localhost:5432/optiserve
   ```

4. **Initialize the database**
   ```bash
   npm run db:push
   ```

5. **Start the development server**
   ```bash
   npm run dev
   ```

6. **Open your browser**
   Navigate to `http://localhost:5000`

## Database Setup

### Option 1: PostgreSQL (Local Development)

1. **Install PostgreSQL**
   ```bash
   # macOS (using Homebrew)
   brew install postgresql
   brew services start postgresql
   
   # Create database
   createdb optiserve
   ```

2. **Configure DATABASE_URL**
   ```bash
   DATABASE_URL=postgresql://localhost:5432/optiserve
   ```

### Option 2: Neon Database (Cloud)

1. Create a free account at [Neon](https://neon.tech)
2. Create a new database
3. Copy the connection string to your `.env` file
4. Run `npm run db:push` to set up tables

## Usage

### Static Code Analysis

1. **Navigate to Dashboard**
2. **Select "Static Code Analysis"**
3. **Enter repository details**:
   - Repository URL (e.g., `https://github.com/username/project`)
   - Branch (default: main)
   - Primary language (auto-detected)
4. **Click "Analyze"**
5. **View results** with performance score and recommendations

### Live Service Analysis

1. **Navigate to Dashboard**
2. **Select "Live Service Analysis"** 
3. **Enter service URL** (e.g., `https://api.example.com/health`)
4. **Click "Test Service"**
5. **Review performance and security analysis**

### Analysis Management

- **View History**: Navigate to "Analyses" tab for complete history
- **Generate Reports**: Use "Reports" tab for performance insights
- **Configure Settings**: Customize analysis parameters in "Settings"

## Architecture

```
optiserve/
├── client/                 # React frontend
│   ├── src/
│   │   ├── components/     # UI components
│   │   ├── pages/         # Application pages
│   │   ├── hooks/         # Custom React hooks
│   │   └── lib/           # Utilities and configuration
├── server/                # Express.js backend
│   ├── services/          # Analysis engines
│   │   ├── analysis.ts    # Static code analysis
│   │   ├── microservice-analyzer.ts  # Live service testing
│   │   ├── analyzers.ts   # Language-specific analyzers
│   │   └── git.ts         # Repository management
│   ├── routes.ts          # API routes
│   ├── storage.ts         # Database interface
│   └── index.ts           # Server entry point
├── shared/                # Shared TypeScript schemas
└── database/              # Database configuration
```

### Technology Stack

**Frontend**:
- React 18 with TypeScript
- Vite for build tooling
- Tailwind CSS for styling
- Shadcn/ui components
- TanStack Query for state management
- Wouter for routing

**Backend**:
- Express.js with TypeScript
- Drizzle ORM with PostgreSQL
- Node.js fs for file operations
- Git CLI for repository cloning

**Database**:
- PostgreSQL with Drizzle schema
- Neon database support
- Automated migrations

## API Reference

### Analysis Endpoints

```bash
# Create new analysis
POST /api/analyses
{
  "type": "static" | "live_service",
  "repositoryUrl": "https://github.com/...",  # for static
  "serviceUrl": "https://api.example.com",    # for live_service
  "branch": "main",
  "language": "java"
}

# Get analysis details
GET /api/analyses/:id

# Get analysis recommendations
GET /api/analyses/:id/recommendations

# List all analyses
GET /api/analyses
```

### Repository Endpoints

```bash
# List repositories
GET /api/repositories

# Get repository details
GET /api/repositories/:id

# Get repository analyses
GET /api/repositories/:id/analyses
```

## Development

### Project Structure

- **Monorepo setup** with client and server in same repository
- **Shared TypeScript schemas** for type safety
- **Automated database migrations** with Drizzle
- **Hot module reloading** for development
- **Production builds** with optimized assets

### Available Scripts

```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run db:push      # Update database schema
npm run db:studio    # Open database admin interface
npm start           # Start production server
```

### Development Workflow

1. **Start development environment**
   ```bash
   npm run dev
   ```

2. **Make changes** to client or server code
3. **Database changes**: Update `shared/schema.ts` then run `npm run db:push`
4. **Test changes** at `http://localhost:5000`

## Deployment

### Production Build

```bash
# Build the application
npm run build

# Start production server
npm start
```

### Environment Variables

Required environment variables for production:

```bash
DATABASE_URL=postgresql://...
NODE_ENV=production
```

### Docker Deployment (Optional)

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build
EXPOSE 5000
CMD ["npm", "start"]
```

## Troubleshooting

### Common Issues

1. **Database connection errors**
   - Verify DATABASE_URL is correct
   - Ensure PostgreSQL is running
   - Check firewall settings

2. **Git cloning failures**
   - Verify repository URL is accessible
   - Check network connectivity
   - Ensure sufficient disk space

3. **Analysis timeouts**
   - Large repositories may take time to analyze
   - Check server logs for specific errors
   - Increase timeout in settings if needed

### Debug Mode

Enable detailed logging by setting:
```bash
NODE_ENV=development
```

### Support

For issues and questions:
1. Check the troubleshooting section above
2. Review server logs for error details
3. Ensure all dependencies are properly installed
4. Verify database connectivity

## License

MIT License - see LICENSE file for details.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

---

Built with ❤️ for performance optimization and microservice analysis.