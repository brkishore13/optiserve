# OptiServe Deployment Guide

## Complete Setup Instructions for Mac

### Prerequisites Installation

1. **Install Node.js 18+**
   ```bash
   # Using Homebrew (recommended)
   brew install node
   
   # Verify installation
   node --version  # Should be 18.0.0 or higher
   npm --version
   ```

2. **Install PostgreSQL** (Option 1: Local Database)
   ```bash
   # Using Homebrew
   brew install postgresql
   brew services start postgresql
   
   # Create database user and database
   createuser -s optiserve
   createdb optiserve -O optiserve
   ```

3. **Alternative: Use Neon Database** (Option 2: Cloud Database)
   - Visit [neon.tech](https://neon.tech) and create a free account
   - Create a new database project
   - Copy the connection string for use in step 6

### Application Setup

4. **Clone/Download the Application**
   ```bash
   # If using GitHub (after repository is created)
   git clone https://github.com/[username]/optiserve.git
   cd optiserve
   
   # Or download and extract the project files
   ```

5. **Install Dependencies**
   ```bash
   npm install
   ```

6. **Configure Environment Variables**
   ```bash
   # Copy the example environment file
   cp .env.example .env
   
   # Edit .env file with your database connection
   nano .env
   ```
   
   **For Local PostgreSQL:**
   ```
   DATABASE_URL=postgresql://optiserve@localhost:5432/optiserve
   NODE_ENV=development
   PORT=5000
   ```
   
   **For Neon Database:**
   ```
   DATABASE_URL=postgresql://[username]:[password]@[endpoint]/[database]?sslmode=require
   NODE_ENV=development  
   PORT=5000
   ```

7. **Initialize Database Schema**
   ```bash
   npm run db:push
   ```

8. **Start the Application**
   ```bash
   # Development mode (with hot reloading)
   npm run dev
   
   # Production mode
   npm run build
   npm start
   ```

9. **Access the Application**
   - Open your browser to `http://localhost:5000`
   - You should see the OptiServe dashboard

### GitHub Repository Setup

To create and push to GitHub:

1. **Create GitHub Repository**
   - Go to [github.com](https://github.com) and create a new repository
   - Name it "optiserve" or your preferred name
   - Don't initialize with README (we have one)

2. **Push Code to GitHub**
   ```bash
   # Initialize git repository (if not already done)
   git init
   
   # Add all files
   git add .
   
   # Make initial commit
   git commit -m "Initial commit: OptiServe performance analysis platform"
   
   # Add GitHub remote (replace with your repository URL)
   git remote add origin https://github.com/[your-username]/optiserve.git
   
   # Push to GitHub
   git branch -M main
   git push -u origin main
   ```

### Testing the Application

1. **Test Static Code Analysis**
   - Navigate to Dashboard
   - Select "Static Code Analysis"  
   - Enter: `https://github.com/spring-projects/spring-petclinic`
   - Branch: `main`
   - Language: `Java`
   - Click "Analyze Repository"

2. **Test Live Service Analysis**
   - Select "Live Service Analysis"
   - Enter: `https://httpbin.org/json`
   - Click "Test Service"

3. **Test Navigation**
   - Click "Analyses" tab to view analysis history
   - Click "Reports" tab to see performance reports
   - Click "Settings" tab to configure preferences

### Production Deployment

For production deployment on a Mac server:

1. **Build for Production**
   ```bash
   npm run build
   ```

2. **Set Production Environment**
   ```bash
   # Edit .env file
   NODE_ENV=production
   PORT=5000
   ```

3. **Start Production Server**
   ```bash
   npm start
   ```

4. **Process Management** (Optional)
   ```bash
   # Install PM2 for process management
   npm install -g pm2
   
   # Start with PM2
   pm2 start dist/index.js --name "optiserve"
   pm2 startup
   pm2 save
   ```

### Troubleshooting

**Database Connection Issues:**
```bash
# Check if PostgreSQL is running
brew services list | grep postgresql

# Restart PostgreSQL if needed
brew services restart postgresql

# Test database connection
psql -d optiserve -c "SELECT 1;"
```

**Port Already in Use:**
```bash
# Find process using port 5000
lsof -i :5000

# Kill the process (replace PID)
kill -9 [PID]
```

**Permission Issues:**
```bash
# Fix npm permissions
sudo chown -R $(whoami) ~/.npm
```

### Application Structure

```
optiserve/
├── README.md              # Main documentation
├── DEPLOYMENT.md          # This deployment guide
├── package.json           # Dependencies and scripts
├── .env.example          # Environment variables template
├── client/               # React frontend
│   ├── src/
│   │   ├── components/   # UI components
│   │   ├── pages/       # Application pages (Dashboard, Analyses, Reports, Settings)
│   │   └── lib/         # Utilities
├── server/               # Express.js backend
│   ├── services/        # Analysis engines
│   ├── routes.ts        # API endpoints
│   └── index.ts         # Server entry point
├── shared/              # Shared TypeScript schemas
└── dist/                # Built files (created after npm run build)
```

### Available Features

✅ **Dashboard**: Create new analyses (static code or live service)
✅ **Analyses**: View complete analysis history with filtering
✅ **Reports**: Performance insights and trends
✅ **Settings**: Configure analysis parameters
✅ **Static Analysis**: Java, Python, Node.js, Go repository analysis
✅ **Live Service Testing**: Performance, security, and connectivity testing
✅ **Real-time Progress**: Step-by-step analysis progress tracking
✅ **Comprehensive Reporting**: Detailed recommendations with code examples

The application is now fully functional with working navigation and ready for production use!