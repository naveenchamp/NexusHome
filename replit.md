# SmartHabitat IoT Kit Builder - Replit Application Guide

## Overview

SmartHabitat is a full-stack web application for building and managing smart home systems using modular IoT kits. Users can browse available smart home kits, design floor plans, place devices in rooms, and control their smart home devices through an integrated dashboard. The application features a modern React frontend with a Node.js/Express backend, PostgreSQL database with Neon serverless hosting, and Replit authentication.

## User Preferences

Preferred communication style: Simple, everyday language.
Database preference: MongoDB over PostgreSQL for data storage.

## System Architecture

The application follows a monorepo structure with clear separation between client, server, and shared code:

- **Frontend**: React with TypeScript, Vite build system, shadcn/ui components
- **Backend**: Node.js with Express, TypeScript
- **Database**: MongoDB with Mongoose ODM (currently using memory storage with comprehensive dummy data)
- **Authentication**: Replit OAuth integration with session management
- **Styling**: Tailwind CSS with custom design system
- **State Management**: TanStack Query for server state, React hooks for local state

## Key Components

### Frontend Architecture
- **React Router**: Using Wouter for client-side routing
- **UI Components**: shadcn/ui component library with Radix UI primitives
- **Styling**: Tailwind CSS with CSS variables for theming
- **State Management**: TanStack Query for API calls and caching
- **Form Handling**: React Hook Form with Zod validation

### Backend Architecture
- **Express Server**: RESTful API with middleware for logging and error handling
- **Authentication**: Replit OAuth with Passport.js and session storage
- **Database Access**: Mongoose ODM with MongoDB connection handling
- **File Structure**: Clean separation of routes, database, and authentication logic

### Database Schema (MongoDB Collections)
- **Users**: Replit OAuth user data (id, email, name, profile image)
- **Sessions**: Session storage for authentication persistence
- **Kit Categories**: Grouping for smart home device types (3 categories: Lighting, Security, Energy)
- **Kits**: Individual smart home modules/devices available for purchase (9 comprehensive kits)
- **Floor Plans**: User-created home layouts with room definitions (2 sample plans per user)
- **User Devices**: Instances of kits placed in specific floor plan locations (8 sample devices)

## Data Flow

1. **Authentication Flow**: 
   - Users authenticate via Replit OAuth
   - Sessions stored in PostgreSQL for persistence
   - Protected routes require authentication middleware

2. **Kit Browsing**:
   - Categories and kits loaded from database
   - Filtering by category supported
   - Kit details include specifications and compatibility

3. **Floor Planning**:
   - Users create floor plans with room layouts
   - Drag-and-drop interface for device placement
   - Position and room assignment stored for each device

4. **Device Control**:
   - Real-time device status and control interface
   - Device state changes trigger database updates
   - Dashboard aggregates all user devices across floor plans

## External Dependencies

### Database & Infrastructure
- **MongoDB**: Document database for flexible smart home data storage
- **Mongoose ODM**: Object Document Mapping with schema validation and type safety

### Authentication
- **Replit OAuth**: Integrated authentication using OpenID Connect
- **Passport.js**: Authentication middleware with session management

### Frontend Libraries
- **React**: UI framework with hooks and functional components  
- **Vite**: Fast build tool with HMR and TypeScript support
- **TanStack Query**: Server state management and caching
- **Wouter**: Lightweight client-side routing
- **shadcn/ui**: Pre-built accessible UI components
- **Tailwind CSS**: Utility-first CSS framework

### Backend Libraries
- **Express**: Web framework with middleware support
- **connect-mongo**: MongoDB session store for Express sessions (fallback to memory store)
- **mongoose**: MongoDB object modeling and connection management

## Deployment Strategy

The application is designed for Replit deployment with the following considerations:

- **Development**: `npm run dev` starts both Vite dev server and Express API
- **Production Build**: `npm run build` creates optimized client bundle and compiles server
- **Environment Variables**: MONGODB_URI (optional), SESSION_SECRET, REPL_ID, ISSUER_URL required
- **Static Assets**: Client build output served by Express in production
- **Database Initialization**: Comprehensive dummy data loaded automatically on first user login

The monorepo structure allows for easy deployment on Replit with automatic environment setup and integrated database provisioning.