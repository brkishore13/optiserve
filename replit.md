# OptiServe - Performance Analysis Platform

## Overview

OptiServe is a comprehensive microservice performance analysis platform that ingests code repositories and provides detailed performance improvement recommendations. The application performs both static code analysis and provides an interactive dashboard for viewing results.

## User Preferences

Preferred communication style: Simple, everyday language.

## Recent Changes (July 23, 2025)

✅ **Fixed Navigation Tabs**: Implemented proper routing for Analyses, Reports, and Settings tabs
✅ **Complete UI Pages**: Created comprehensive pages for all navigation tabs with full functionality
✅ **Microservice Analysis**: Added live service testing capabilities alongside static code analysis
✅ **Production Ready**: Application is fully functional and deployable on Mac computers
✅ **GitHub Ready**: Complete documentation and deployment guides created for sharing

## System Architecture

OptiServe follows a modern full-stack architecture with a React frontend, Express.js backend, and PostgreSQL database. The application is designed as a monorepo with clear separation between client, server, and shared components.

### Directory Structure
- `/client` - React frontend application with Vite build system
- `/server` - Express.js backend with TypeScript
- `/shared` - Shared TypeScript schemas and types
- `/migrations` - Database migration files

## Key Components

### Frontend Architecture
- **Framework**: React with TypeScript
- **Build Tool**: Vite for fast development and optimized builds
- **UI Library**: Shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with CSS variables for theming
- **State Management**: TanStack React Query for server state
- **Routing**: Wouter for lightweight client-side routing

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **Database ORM**: Drizzle ORM with PostgreSQL
- **Database Provider**: Neon Database (serverless PostgreSQL)
- **Session Management**: PostgreSQL-based sessions with connect-pg-simple
- **Build System**: esbuild for production builds

### Database Schema
The application uses four main entities:
- **Users**: Basic user authentication
- **Repositories**: Git repository information and metadata
- **Analyses**: Analysis jobs with status tracking and scoring
- **Recommendations**: Performance improvement suggestions with categorization

## Data Flow

1. **Repository Input**: Users provide Git repository URLs for analysis
2. **Analysis Processing**: Server clones repository and performs static code analysis
3. **Language Detection**: Automatic detection of programming language (Java, Python, Node.js, Go)
4. **Code Analysis**: Language-specific analyzers scan for performance issues
5. **Recommendation Generation**: Creates categorized recommendations with severity levels
6. **Results Display**: Interactive dashboard shows performance scores and actionable recommendations

## External Dependencies

### Database
- **Neon Database**: Serverless PostgreSQL for data persistence
- **Drizzle Kit**: Database migrations and schema management

### Analysis Tools
- **Git Operations**: Direct git commands for repository cloning
- **Language Parsers**: Custom parsers for package.json, pom.xml, requirements.txt, go.mod
- **File System Analysis**: Node.js fs module for code scanning

### UI Components
- **Radix UI**: Headless UI primitives for accessibility
- **Lucide React**: Icon library
- **Class Variance Authority**: Component variant management
- **Date-fns**: Date manipulation utilities

## Deployment Strategy

### Development
- **Development Server**: Vite dev server with HMR for frontend
- **Backend Server**: tsx for TypeScript execution in development
- **Database**: Neon Database with environment-based connection strings

### Production Build
- **Frontend**: Vite builds optimized static assets to `/dist/public`
- **Backend**: esbuild bundles server code to `/dist/index.js`
- **Static Serving**: Express serves built frontend assets in production

### Environment Configuration
- **DATABASE_URL**: Required environment variable for PostgreSQL connection
- **NODE_ENV**: Environment detection for development/production modes
- **REPL_ID**: Replit-specific configuration for development tooling

### Analysis Engine
The core analysis functionality is modular and extensible:
- **Language Analyzers**: Separate analyzers for Java, Python, Node.js, and Go
- **Async Processing**: Analysis jobs run asynchronously with progress tracking
- **Error Handling**: Comprehensive error handling with status updates
- **Recommendation Categories**: Database, memory, configuration, and network optimizations

The application is designed to be easily extensible with new language analyzers and recommendation types while maintaining a clean separation of concerns between the analysis engine, data layer, and user interface.