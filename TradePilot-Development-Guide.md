# TradePilot Development Guide
## Flutter (Dart) + NestJS (TypeScript) with AI Coding Assistants

**Last Updated:** November 2025  
**Target:** MVP in 16-20 weeks, 50 customers in 90 days post-launch

---

## Table of Contents

1. [Development Environment Setup](#development-environment-setup)
2. [Project Architecture](#project-architecture)
3. [Week-by-Week Development Roadmap](#week-by-week-development-roadmap)
4. [AI Coding Assistant Workflows](#ai-coding-assistant-workflows)
5. [Critical Implementation Details](#critical-implementation-details)
6. [Testing & Deployment](#testing--deployment)
7. [Troubleshooting & Resources](#troubleshooting--resources)

---

## Development Environment Setup

### Phase 1: Install Core Tools (Day 1)

#### 1.1 Flutter & Dart Setup

**macOS:**
```bash
# Install Flutter via official installer
# Download from: https://docs.flutter.dev/get-started/install/macos

# Add to PATH (add to ~/.zshrc or ~/.bash_profile)
export PATH="$PATH:/Users/YOUR_USERNAME/development/flutter/bin"

# Verify installation
flutter doctor

# Install Xcode (for iOS development)
# Download from Mac App Store

# Install Android Studio (for Android development)
# Download from: https://developer.android.com/studio

# Accept licenses
flutter doctor --android-licenses
```

**Windows:**
```bash
# Download Flutter SDK from: https://docs.flutter.dev/get-started/install/windows
# Extract to C:\src\flutter
# Add C:\src\flutter\bin to PATH

# Install Android Studio
# Install Visual Studio (for Windows desktop development)

# Verify
flutter doctor
```

**Linux:**
```bash
# Install Flutter
sudo snap install flutter --classic

# Install Android Studio
sudo snap install android-studio --classic

# Verify
flutter doctor
```

#### 1.2 Node.js & TypeScript Setup

```bash
# Install Node.js 20.x LTS
# Download from: https://nodejs.org/

# Verify installation
node --version  # Should be v20.x.x
npm --version

# Install global TypeScript
npm install -g typescript

# Install NestJS CLI globally
npm install -g @nestjs/cli

# Verify
nest --version
```

#### 1.3 Database & Tools

```bash
# Install PostgreSQL
# macOS: brew install postgresql@15
# Windows: Download from https://www.postgresql.org/download/
# Linux: sudo apt install postgresql-15

# Install Redis
# macOS: brew install redis
# Windows: Download from https://redis.io/download
# Linux: sudo apt install redis-server

# Install Git
# Download from: https://git-scm.com/downloads

# Install Docker Desktop (optional but recommended)
# Download from: https://www.docker.com/products/docker-desktop
```

#### 1.4 IDE & Extensions

**VS Code (Recommended):**
```bash
# Download from: https://code.visualstudio.com/

# Install these extensions:
# - Flutter
# - Dart
# - ESLint
# - Prettier
# - Prisma
# - REST Client
# - GitLens
# - GitHub Copilot (optional, paid)
```

**Alternative - Cursor (AI-first IDE):**
```bash
# Download from: https://cursor.sh/
# Built-in AI coding assistant
# Same extensions as VS Code
```

#### 1.5 AI Coding Assistants

**Option 1: GitHub Copilot**
- Cost: $10/month (individual) or $19/month (business)
- Install in VS Code or Cursor
- Best for: Line-by-line code completion

**Option 2: Cursor AI**
- Cost: $20/month (includes Copilot++)
- Download: https://cursor.sh/
- Best for: Large code generation, refactoring

**Option 3: Claude.ai (Free tier available)**
- Use for: Architecture decisions, code review, debugging
- Copy/paste code blocks for analysis

**Recommendation:** Start with Claude.ai (free) + GitHub Copilot ($10/month)

---

## Project Architecture

### Directory Structure

```
tradepilot/
├── backend/                    # NestJS TypeScript API
│   ├── src/
│   │   ├── main.ts
│   │   ├── app.module.ts
│   │   ├── auth/              # Authentication module
│   │   ├── users/             # User management
│   │   ├── jobs/              # Job/project management
│   │   ├── quotes/            # Quote generation
│   │   ├── invoices/          # Invoice management
│   │   ├── payments/          # Stripe integration
│   │   ├── accounting/        # Xero integration
│   │   ├── ai/                # OpenAI GPT-4 integration
│   │   ├── scheduling/        # Job scheduling logic
│   │   ├── common/            # Shared utilities
│   │   └── database/          # Database config
│   ├── prisma/
│   │   ├── schema.prisma      # Database schema
│   │   └── migrations/
│   ├── test/
│   ├── .env
│   ├── package.json
│   └── tsconfig.json
│
├── mobile/                     # Flutter Dart App
│   ├── lib/
│   │   ├── main.dart
│   │   ├── app.dart
│   │   ├── core/              # Core utilities
│   │   │   ├── api/           # API client
│   │   │   ├── auth/          # Auth service
│   │   │   ├── database/      # SQLite offline DB
│   │   │   ├── sync/          # Background sync
│   │   │   └── storage/       # Local storage
│   │   ├── features/
│   │   │   ├── auth/          # Login/signup screens
│   │   │   ├── dashboard/     # Main dashboard
│   │   │   ├── jobs/          # Job list & detail
│   │   │   ├── quotes/        # Quote creation
│   │   │   ├── invoices/      # Invoice management
│   │   │   ├── schedule/      # Calendar view
│   │   │   └── settings/      # User settings
│   │   ├── shared/
│   │   │   ├── models/        # Data models
│   │   │   ├── widgets/       # Reusable widgets
│   │   │   └── utils/         # Helper functions
│   │   └── theme/             # App theming
│   ├── assets/
│   │   ├── images/
│   │   └── icons/
│   ├── test/
│   ├── pubspec.yaml
│   └── analysis_options.yaml
│
├── docs/                       # Documentation
│   ├── api-spec.md
│   ├── database-schema.md
│   └── setup.md
│
├── .github/
│   └── workflows/             # CI/CD pipelines
│
└── README.md
```

### Tech Stack Summary

**Frontend (Mobile + Web):**
- Flutter 3.24+
- Dart 3.5+
- sqflite (offline database)
- http / dio (API client)
- provider / riverpod (state management)
- go_router (navigation)

**Backend (API Server):**
- NestJS 10+
- TypeScript 5.3+
- Prisma (ORM)
- PostgreSQL 15+
- Redis 7+
- Passport JWT (authentication)

**Third-Party Services:**
- OpenAI GPT-4 API (quote generation)
- Stripe (payments)
- Xero (accounting)
- AWS S3 (file storage)
- AWS EC2/ECS (hosting)

---

## Week-by-Week Development Roadmap

### Week 1-2: Foundation & Learning

#### Week 1: Environment Setup & Dart Basics

**Goals:**
- Complete development environment setup
- Learn Dart fundamentals
- Create project repositories
- Set up CI/CD basics

**Day 1-2: Setup**
```bash
# Create GitHub repositories
gh repo create tradepilot-backend --private
gh repo create tradepilot-mobile --private

# Clone locally
git clone https://github.com/YOUR_USERNAME/tradepilot-backend.git
git clone https://github.com/YOUR_USERNAME/tradepilot-mobile.git

# Initialize NestJS backend
cd tradepilot-backend
nest new . --package-manager npm
npm install @nestjs/config @prisma/client prisma
npm install --save-dev @types/node

# Initialize Flutter mobile
cd ../tradepilot-mobile
flutter create . --org com.tradepilot --platforms=ios,android,web
```

**Day 3-5: Learn Dart**
- Complete: https://dart.dev/guides/language/language-tour
- Do: https://dart.dev/codelabs/async-await
- Practice: Build a simple Flutter counter app
- **AI Prompt to use:**
  ```
  I'm a TypeScript developer learning Dart. Can you explain [Dart concept] 
  and show me the TypeScript equivalent? For example, how do Dart Futures 
  compare to TypeScript Promises?
  ```

**Day 6-7: Project Setup**
```bash
# Backend: Set up Prisma
cd tradepilot-backend
npx prisma init

# Configure .env
DATABASE_URL="postgresql://user:password@localhost:5432/tradepilot"
JWT_SECRET="your-secret-key-change-this"
OPENAI_API_KEY="sk-..."

# Mobile: Add key dependencies
cd ../tradepilot-mobile
flutter pub add http dio provider go_router sqflite path shared_preferences
flutter pub add --dev build_runner json_serializable
```

**Week 1 Deliverable:** ✅ Dev environment ready, basic understanding of Dart

---

#### Week 2: Database Schema & Auth Setup

**Goals:**
- Design database schema
- Implement authentication (backend + mobile)
- Set up API structure

**Day 8-10: Database Design**

Create `backend/prisma/schema.prisma`:
```prisma
// Use AI to help generate this!
// Prompt: "Create a Prisma schema for a tradie management app with users, 
// jobs, quotes, invoices. Users should have email, password hash, name, 
// phone, business name, ABN. Include timestamps and soft deletes."

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id            String    @id @default(uuid())
  email         String    @unique
  passwordHash  String
  firstName     String
  lastName      String
  phone         String?
  businessName  String?
  abn           String?
  role          Role      @default(TRADIE)
  isActive      Boolean   @default(true)
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt
  deletedAt     DateTime?
  
  jobs          Job[]
  quotes        Quote[]
  invoices      Invoice[]
  
  @@index([email])
}

enum Role {
  TRADIE
  ADMIN
}

model Job {
  id              String    @id @default(uuid())
  userId          String
  customerName    String
  customerEmail   String?
  customerPhone   String
  customerAddress String
  jobType         String    // "electrical", "plumbing", etc.
  description     String
  status          JobStatus @default(PENDING)
  scheduledDate   DateTime?
  completedDate   DateTime?
  estimatedHours  Float?
  actualHours     Float?
  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt
  deletedAt       DateTime?
  
  user            User      @relation(fields: [userId], references: [id])
  quote           Quote?
  invoice         Invoice?
  
  @@index([userId, status])
  @@index([scheduledDate])
}

enum JobStatus {
  PENDING
  QUOTED
  SCHEDULED
  IN_PROGRESS
  COMPLETED
  CANCELLED
}

model Quote {
  id                String      @id @default(uuid())
  jobId             String      @unique
  userId            String
  quoteNumber       String      @unique
  lineItems         Json        // Array of {description, quantity, rate, amount}
  subtotal          Decimal     @db.Decimal(10, 2)
  gstAmount         Decimal     @db.Decimal(10, 2)
  totalAmount       Decimal     @db.Decimal(10, 2)
  status            QuoteStatus @default(DRAFT)
  expiryDate        DateTime?
  acceptedAt        DateTime?
  notes             String?
  aiGenerated       Boolean     @default(false)
  aiConfidence      Float?
  createdAt         DateTime    @default(now())
  updatedAt         DateTime    @updatedAt
  
  job               Job         @relation(fields: [jobId], references: [id])
  user              User        @relation(fields: [userId], references: [id])
  
  @@index([userId])
  @@index([quoteNumber])
}

enum QuoteStatus {
  DRAFT
  SENT
  ACCEPTED
  DECLINED
  EXPIRED
}

model Invoice {
  id              String        @id @default(uuid())
  jobId           String        @unique
  userId          String
  invoiceNumber   String        @unique
  lineItems       Json
  subtotal        Decimal       @db.Decimal(10, 2)
  gstAmount       Decimal       @db.Decimal(10, 2)
  totalAmount     Decimal       @db.Decimal(10, 2)
  paidAmount      Decimal       @db.Decimal(10, 2) @default(0)
  status          InvoiceStatus @default(DRAFT)
  dueDate         DateTime?
  paidDate        DateTime?
  xeroInvoiceId   String?
  stripePaymentId String?
  notes           String?
  createdAt       DateTime      @default(now())
  updatedAt       DateTime      @updatedAt
  
  job             Job           @relation(fields: [jobId], references: [id])
  user            User          @relation(fields: [userId], references: [id])
  
  @@index([userId])
  @@index([invoiceNumber])
  @@index([status])
}

enum InvoiceStatus {
  DRAFT
  SENT
  PAID
  OVERDUE
  CANCELLED
}
```

Run migration:
```bash
npx prisma migrate dev --name init
npx prisma generate
```

**Day 11-12: Backend Auth**

**AI Prompt:**
```
Create a NestJS authentication module using JWT and Passport. Include:
1. Register endpoint (POST /auth/register)
2. Login endpoint (POST /auth/login)  
3. Get current user endpoint (GET /auth/me)
4. Password hashing with bcrypt
5. JWT guard for protected routes
Use Prisma for database access.
```

Create `backend/src/auth/auth.module.ts`, `auth.service.ts`, `auth.controller.ts`

**Day 13-14: Flutter Auth UI**

**AI Prompt:**
```
Create a Flutter login screen with:
- Email and password text fields
- Form validation
- Login button that calls API
- "Register" link to signup screen
- Loading state during API call
- Error handling with SnackBar
Use Provider for state management.
```

Create `mobile/lib/features/auth/login_screen.dart`

**Week 2 Deliverable:** ✅ Working authentication (register, login, JWT tokens)

---

### Week 3-4: Core Backend APIs

**Goals:**
- Build CRUD APIs for jobs, quotes, invoices
- Implement business logic
- Add validation and error handling

**Week 3: Jobs & Quotes APIs**

**Day 15-17: Jobs Module**

**AI Prompt:**
```
Create a NestJS jobs module with:
- POST /jobs (create job)
- GET /jobs (list all jobs for authenticated user, with filters)
- GET /jobs/:id (get single job)
- PUT /jobs/:id (update job)
- DELETE /jobs/:id (soft delete)
- Include DTOs for validation using class-validator
- Add pagination for list endpoint
- Include related quote and invoice in single job response
```

**Day 18-21: Quotes Module**

**AI Prompt:**
```
Create a NestJS quotes module with:
- POST /quotes (create quote from job)
- GET /quotes (list quotes with filters)
- GET /quotes/:id (get single quote)
- PUT /quotes/:id (update quote)
- PUT /quotes/:id/send (mark as sent, send email)
- PUT /quotes/:id/accept (customer acceptance)
- Automatically calculate GST (10% of subtotal)
- Generate unique quote numbers (format: Q-2025-0001)
- Validate that lineItems total matches subtotal
```

**Week 4: Invoices & OpenAI Integration**

**Day 22-24: Invoices Module**

Similar to quotes, build full CRUD for invoices.

**Day 25-28: AI Quote Generation**

**AI Prompt:**
```
Create an OpenAI integration service for quote generation:
1. Endpoint: POST /quotes/generate
2. Input: job description, job type, customer address
3. Call GPT-4 API with structured prompt
4. Return: suggested line items with descriptions, quantities, rates
5. Include confidence score
6. Add safety validation (max quote amount, require human review for >$10k)
7. Store AI-generated flag in database
Use OpenAI SDK for Node.js.
```

Create `backend/src/ai/openai.service.ts`:
```typescript
import OpenAI from 'openai';

export class OpenAIService {
  private client: OpenAI;
  
  async generateQuoteItems(jobDescription: string, jobType: string) {
    const prompt = `You are an expert Australian ${jobType} estimator...`;
    // AI will help fill in the rest!
  }
}
```

**Week 3-4 Deliverable:** ✅ Complete backend APIs for jobs, quotes, invoices, AI generation

---

### Week 5-8: Mobile App Development

**Goals:**
- Build all mobile screens
- Implement offline database
- Create background sync
- Connect to backend APIs

#### Week 5: Flutter Project Structure & Navigation

**Day 29-31: App Structure**

**AI Prompt:**
```
Set up a Flutter app with:
1. go_router for navigation
2. Provider for state management
3. Theme configuration (primary color: electric blue, tradie-friendly design)
4. Bottom navigation bar with: Dashboard, Jobs, Schedule, More
5. Splash screen with logo
6. Automatic navigation to login if not authenticated
```

**Day 32-35: Dashboard Screen**

**AI Prompt:**
```
Create a Flutter dashboard screen showing:
- Welcome message with user's name
- Quick stats cards: Pending Jobs, Quotes Sent, Revenue This Month
- Recent jobs list (last 5)
- "Create Job" floating action button
- Pull-to-refresh
- Loading states and error handling
Use Provider to fetch data from API.
```

#### Week 6: Jobs & Quotes Screens

**Day 36-38: Job List & Detail**

**AI Prompt:**
```
Create Flutter screens for jobs:
1. Job list with search and filter (status, date range)
2. Job detail showing all info, with Edit and Delete options
3. Create/Edit job form with validation
4. "Generate Quote" button on job detail
Connect to backend APIs using http package.
```

**Day 39-42: Quote Screens**

**AI Prompt:**
```
Create Flutter quote screens:
1. Quote list (filterable by status)
2. Quote detail with line items table
3. Create quote form:
   - Add line items manually
   - OR use "AI Generate" button
   - Show AI suggestions with confidence score
   - Allow editing AI suggestions
4. Send quote button (marks as sent)
5. PDF preview (use pdf package)
```

#### Week 7: Offline Functionality

**CRITICAL WEEK - This is "the hill to die on"**

**Day 43-45: SQLite Setup**

**AI Prompt:**
```
Create a Flutter offline database layer using sqflite:
1. Create database schema matching backend models (users, jobs, quotes, invoices)
2. Migration system for version updates
3. CRUD operations for each model
4. Query methods: getJobs(), getJobById(), searchJobs(), etc.
5. Sync status tracking (is_synced boolean, last_synced timestamp)
Include full example for Job model.
```

Create `mobile/lib/core/database/database_helper.dart`

**Day 46-49: Sync Engine**

**AI Prompt:**
```
Create a Flutter background sync service:
1. Detect when app comes online (connectivity_plus package)
2. Queue local changes (creates, updates, deletes) while offline
3. Sync to backend when online (upload local changes first)
4. Download server changes (pull updates)
5. Conflict resolution (server wins, but notify user)
6. Sync status UI indicator (online/offline/syncing)
7. Manual sync trigger button
Use WorkManager for background processing.
```

This is complex - break into multiple AI conversations:
- Part 1: Sync queue system
- Part 2: Upload local changes
- Part 3: Download server changes
- Part 4: Conflict resolution
- Part 5: UI integration

**Day 50: Offline Testing**

Manually test offline mode:
1. Create job while offline → saves to SQLite
2. Turn on internet → syncs to server
3. Edit job on another device → syncs back
4. Create quote offline → AI generation fails gracefully

**Week 7 Deliverable:** ✅ App works completely offline, syncs when online

#### Week 8: Invoice & Schedule Screens

**Day 51-53: Invoice Screens**

Similar to quotes - list, detail, create/edit forms.

**Day 54-56: Schedule/Calendar View**

**AI Prompt:**
```
Create a Flutter calendar screen:
1. Monthly calendar view using table_calendar package
2. Show scheduled jobs on calendar dates
3. Tap date to see jobs for that day
4. Drag-and-drop to reschedule (optional MVP feature)
5. Color-code by job status
```

**Day 57: Polish & Bug Fixes**

Fix any UI issues, improve loading states, add better error messages.

**Week 5-8 Deliverable:** ✅ Fully functional mobile app with offline support

---

### Week 9-10: Integrations

**Goals:**
- Xero integration for invoices
- Stripe payment processing
- Email notifications
- Google Maps routing

#### Week 9: Xero Integration

**Day 58-61: Xero OAuth & Invoice Sync**

**AI Prompt:**
```
Implement Xero integration in NestJS:
1. OAuth 2.0 setup (xero-node SDK)
2. Store Xero tokens in database (encrypted)
3. Sync invoice to Xero when status changes to SENT
4. Endpoint: POST /accounting/xero/connect (initiate OAuth)
5. Endpoint: POST /invoices/:id/sync-xero (manual sync)
6. Webhook handler for payment updates from Xero
Include error handling for expired tokens.
```

**Day 62-64: Stripe Integration**

**AI Prompt:**
```
Implement Stripe payment processing:
1. Create Stripe customer on user registration
2. Generate payment link for invoice (Stripe Payment Links API)
3. Webhook handler for payment success
4. Update invoice status to PAID when payment received
5. Store stripePaymentId in invoice
Include test mode toggle for development.
```

#### Week 10: Maps & Notifications

**Day 65-67: Google Maps Integration**

**AI Prompt:**
```
Add Google Maps to Flutter app:
1. Show job location on map (google_maps_flutter package)
2. Get directions to job site
3. Geocode customer address (geocoding package)
4. Validate Australian addresses using G-NAF if possible
```

**Day 68-70: Email Notifications**

**AI Prompt:**
```
Create email notification system in NestJS:
1. Use nodemailer or AWS SES
2. Send emails for:
   - Quote sent to customer
   - Invoice sent to customer
   - Payment received confirmation
3. HTML email templates with branding
4. Queue emails with Bull (Redis-based queue)
```

**Week 9-10 Deliverable:** ✅ Working integrations with Xero, Stripe, Maps, Email

---

### Week 11-12: Testing & Bug Fixes

**Goals:**
- Write critical tests
- Fix bugs found during testing
- Improve performance
- Security audit

#### Week 11: Automated Testing

**Day 71-73: Backend Tests**

**AI Prompt:**
```
Write Jest tests for NestJS:
1. Unit tests for auth service (register, login, JWT validation)
2. Integration tests for jobs API (create, list, update, delete)
3. Test AI quote generation with mocked OpenAI responses
4. Test GST calculation accuracy
5. Test Xero integration with mocked API
Aim for 70%+ code coverage on critical paths.
```

**Day 74-77: Mobile Tests**

**AI Prompt:**
```
Write Flutter tests:
1. Unit tests for database operations (SQLite CRUD)
2. Widget tests for login screen
3. Widget tests for job list screen
4. Integration test: create job offline, sync when online
5. Test sync conflict resolution
```

#### Week 12: Bug Fixes & Performance

**Day 78-80: Bug Fixing**

- Test on real Android and iOS devices
- Fix any platform-specific issues
- Test offline → online → offline transitions
- Verify all forms validate correctly
- Check GST calculations

**Day 81-84: Performance Optimization**

**AI Prompt:**
```
Optimize Flutter app performance:
1. Add pagination/infinite scroll to job list (currently loads all)
2. Implement image caching for customer photos
3. Lazy load screens (don't load all routes at startup)
4. Profile using Flutter DevTools, fix jank
5. Reduce app size (remove unused assets)
```

**Week 11-12 Deliverable:** ✅ Stable, tested app with 70%+ coverage

---

### Week 13-16: Polish, Beta Prep, Launch

#### Week 13-14: UI/UX Polish

**Day 85-90: Design Improvements**

- Add app icon and splash screen
- Consistent spacing and typography
- Empty states for lists ("No jobs yet")
- Skeleton loaders instead of spinners
- Haptic feedback on buttons (iOS)
- Dark mode support (optional)

**AI Prompt:**
```
Improve Flutter UI polish:
1. Create custom app theme with consistent colors, text styles
2. Add skeleton loading screens (shimmer effect)
3. Improve empty states with illustrations
4. Add pull-to-refresh to all lists
5. Smooth page transitions
Use Flutter's ThemeData and animations.
```

**Day 91-98: In-App Tutorial & Help**

**AI Prompt:**
```
Add onboarding to Flutter app:
1. First-time user tutorial (show after registration)
2. Walkthrough of main features (jobs, quotes, offline mode)
3. Help documentation screen
4. FAQ section
5. Contact support button
Use intro_slider or tutorial_coach_mark package.
```

#### Week 15: Beta Testing Prep

**Day 99-102: App Store Preparation**

**iOS:**
```bash
# Set up Apple Developer Account ($99/year)
# Create App ID in App Store Connect
# Configure signing in Xcode
# Build for release
cd mobile
flutter build ios --release

# Archive and submit via Xcode
# Fill out app metadata, screenshots
# Submit for TestFlight beta review (1-2 days)
```

**Android:**
```bash
# Create Google Play Console account ($25 one-time)
# Generate signing key
keytool -genkey -v -keystore ~/tradepilot-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias tradepilot

# Build release APK
flutter build appbundle --release

# Upload to Google Play Console (internal testing track)
# Fill out app listing, screenshots
# Submit for review (few hours typically)
```

**Day 103-105: Backend Deployment**

**Deploy to AWS EC2:**
```bash
# Launch Ubuntu EC2 instance (t3.small, Sydney region)
# Install Node.js, PostgreSQL, Redis, PM2

# On server:
git clone https://github.com/YOUR_USERNAME/tradepilot-backend.git
cd tradepilot-backend
npm install
npx prisma migrate deploy
npm run build
pm2 start dist/main.js --name tradepilot-api

# Set up nginx reverse proxy
# Configure SSL with Let's Encrypt
# Point api.tradepilot.com.au to EC2
```

**Alternative - Deploy to AWS ECS (Docker):**
```bash
# Containerize backend
# Push to ECR
# Deploy to ECS Fargate
# Use RDS for PostgreSQL, ElastiCache for Redis
```

#### Week 16: Beta Launch

**Day 106-108: Recruit Beta Users**

Target: 10-20 Sydney electricians

**Outreach channels:**
1. Local Facebook groups (Sydney tradies)
2. LinkedIn direct messages
3. Electrical industry forums
4. Trade associations
5. Word of mouth

**Offer:**
- Free lifetime account (or 50% off forever)
- Direct support via phone/WhatsApp
- Feature requests prioritized
- Weekly feedback calls

**Day 109-112: Monitor & Support**

- Set up error monitoring (Sentry)
- Create support ticketing system (Zendesk or plain email)
- Daily check-ins with beta users
- Fix critical bugs within 24 hours
- Weekly usage analytics review

**Week 16 Deliverable:** ✅ 10-20 beta users actively testing

---

### Week 17-20: Beta Iteration

**Goals:**
- Gather feedback from real usage
- Fix bugs and usability issues
- Iterate on features
- Prepare for public launch

**Weekly cadence:**
1. **Monday:** Review previous week's feedback and analytics
2. **Tuesday-Thursday:** Implement fixes and improvements
3. **Friday:** Deploy updates, call 3-5 beta users for feedback
4. **Weekend:** Monitor for issues

**Key metrics to track:**
- Daily active users (DAU)
- Jobs created per user per week
- Quotes generated (manual vs AI)
- Invoices sent
- Time spent in app
- Offline sync success rate
- Crash rate
- Feature usage (what's used vs ignored)

**Red flags to watch for:**
- <40% weekly active users (poor engagement)
- High uninstall rate
- Users creating <2 jobs/week (not getting value)
- Complaints about offline sync
- Slow AI quote generation (>5 seconds)

**Iteration priorities:**
1. **Critical bugs** (crashes, data loss) → fix within 24 hours
2. **Offline sync issues** → fix within 48 hours
3. **Usability problems** (confusing UI) → fix within 1 week
4. **Feature requests** → evaluate, add to roadmap

**Week 20 Deliverable:** ✅ 70%+ weekly active usage, NPS >40, ready for public launch

---

## AI Coding Assistant Workflows

### How to Use AI Effectively

#### 1. Architecture & Design Phase

**Good prompt example:**
```
I'm building a tradie management app with Flutter and NestJS. I need to design 
the offline sync architecture. Requirements:
- Tradies work in areas with no cell signal
- All job/quote data must be available offline
- Changes made offline must sync when back online
- Handle conflicts if same job edited on multiple devices
- Background sync when app is closed

Can you suggest an architecture approach with:
1. Which Flutter packages to use
2. Database schema design (SQLite)
3. Sync queue system design
4. Conflict resolution strategy
5. Sample code structure
```

**Why it works:**
- Provides context (tradie app, Flutter/NestJS)
- Lists specific requirements
- Asks for structured response
- Requests code examples

#### 2. Implementation Phase

**Good prompt example:**
```
Create a NestJS service that generates quote line items using OpenAI GPT-4.

Requirements:
- Method: generateQuoteLineItems(jobDescription: string, jobType: string, address: string)
- Call GPT-4 API with prompt asking for itemized quote
- Return: array of {description, quantity, unit, rate, amount}
- Include confidence score (0-100)
- Handle errors gracefully
- Add validation: total amount must match sum of line items
- Use environment variable for OpenAI API key

Return TypeScript code using OpenAI SDK v4+.
```

**Why it works:**
- Specific method signature
- Clear requirements and validation rules
- Specifies technology versions
- Asks for error handling

#### 3. Debugging Phase

**Good prompt example:**
```
I have a Flutter sync issue. When I create a job offline and come back online,
the sync uploads the job to the backend successfully, but the local SQLite 
database doesn't update the is_synced flag to true, so it tries to upload 
again and creates a duplicate.

Here's my sync code:
[paste code]

What's wrong and how do I fix it?
```

**Why it works:**
- Describes exact problem behavior
- Includes relevant code
- Asks for specific fix

#### 4. Code Review Phase

**Good prompt example:**
```
Review this Flutter offline database code for potential issues:
[paste code]

Check for:
1. Memory leaks
2. Race conditions (multiple syncs running)
3. Data loss scenarios
4. Performance problems with large datasets
5. Security issues (SQL injection, etc.)
```

**Why it works:**
- Specific review criteria
- Focuses on common problem areas

### AI Assistant Daily Workflow

**Morning (Planning):**
1. Review today's tasks in GitHub Projects
2. Ask AI: "I need to implement [feature]. What's the best approach?"
3. Get architecture suggestions, then break into subtasks

**During Development:**
1. Use AI for boilerplate code generation
2. Use AI for complex logic implementation
3. Use AI to explain unfamiliar patterns
4. Use AI to write tests

**Evening (Review):**
1. Ask AI to review code for bugs
2. Ask AI to suggest improvements
3. Ask AI to help write commit messages

### Sample AI Conversations

#### Conversation 1: Implementing Feature

**You:**
```
I need to add invoice PDF generation to my NestJS backend. Requirements:
- Endpoint: GET /invoices/:id/pdf
- Generate PDF with invoice details, line items table, GST breakdown
- Include business logo and ABN
- Return PDF as downloadable file
- Use pdfkit or similar library

Show me the complete implementation.
```

**AI Response:**
```typescript
// invoices/invoices.controller.ts
import { Controller, Get, Param, Res } from '@nestjs/common';
import { Response } from 'express';
import { InvoicesService } from './invoices.service';

@Controller('invoices')
export class InvoicesController {
  constructor(private readonly invoicesService: InvoicesService) {}

  @Get(':id/pdf')
  async generatePDF(@Param('id') id: string, @Res() res: Response) {
    const pdfBuffer = await this.invoicesService.generateInvoicePDF(id);
    
    res.set({
      'Content-Type': 'application/pdf',
      'Content-Disposition': `attachment; filename=invoice-${id}.pdf`,
      'Content-Length': pdfBuffer.length,
    });
    
    res.end(pdfBuffer);
  }
}

// invoices/invoices.service.ts
import PDFDocument from 'pdfkit';
import { Injectable } from '@nestjs/common';

@Injectable()
export class InvoicesService {
  async generateInvoicePDF(id: string): Promise<Buffer> {
    const invoice = await this.prisma.invoice.findUnique({
      where: { id },
      include: { user: true, job: true },
    });
    
    if (!invoice) throw new NotFoundException('Invoice not found');
    
    return new Promise((resolve, reject) => {
      const doc = new PDFDocument({ margin: 50 });
      const buffers: Buffer[] = [];
      
      doc.on('data', buffers.push.bind(buffers));
      doc.on('end', () => resolve(Buffer.concat(buffers)));
      doc.on('error', reject);
      
      // Header
      doc.fontSize(20).text('INVOICE', 50, 50);
      doc.fontSize(10).text(`Invoice #: ${invoice.invoiceNumber}`, 50, 80);
      doc.text(`Date: ${invoice.createdAt.toLocaleDateString()}`, 50, 95);
      
      // Business details
      doc.text(invoice.user.businessName, 50, 120);
      doc.text(`ABN: ${invoice.user.abn}`, 50, 135);
      
      // Customer details
      doc.text('Bill To:', 50, 170);
      doc.text(invoice.job.customerName, 50, 185);
      doc.text(invoice.job.customerAddress, 50, 200);
      
      // Line items table
      const tableTop = 250;
      doc.text('Description', 50, tableTop);
      doc.text('Qty', 300, tableTop);
      doc.text('Rate', 350, tableTop);
      doc.text('Amount', 450, tableTop);
      
      let y = tableTop + 20;
      const lineItems = invoice.lineItems as any[];
      
      lineItems.forEach(item => {
        doc.text(item.description, 50, y);
        doc.text(item.quantity.toString(), 300, y);
        doc.text(`$${item.rate.toFixed(2)}`, 350, y);
        doc.text(`$${item.amount.toFixed(2)}`, 450, y);
        y += 20;
      });
      
      // Totals
      y += 20;
      doc.text('Subtotal:', 350, y);
      doc.text(`$${invoice.subtotal}`, 450, y);
      y += 20;
      doc.text('GST (10%):', 350, y);
      doc.text(`$${invoice.gstAmount}`, 450, y);
      y += 20;
      doc.fontSize(12).text('Total:', 350, y);
      doc.text(`$${invoice.totalAmount}`, 450, y);
      
      // Footer
      doc.fontSize(8).text(
        'Payment terms: Due within 14 days',
        50,
        700,
        { align: 'center' }
      );
      
      doc.end();
    });
  }
}
```

**You:** "This looks good but I want to add my logo. How do I add an image?"

**AI Response:**
```typescript
// Add this before the header section:
doc.image('path/to/logo.png', 50, 50, { width: 100 });

// Adjust header position to accommodate logo:
doc.fontSize(20).text('INVOICE', 180, 50);
doc.fontSize(10).text(`Invoice #: ${invoice.invoiceNumber}`, 180, 80);
```

#### Conversation 2: Debugging

**You:**
```
My Flutter offline sync is creating duplicate jobs. Here's what happens:
1. Create job offline → saved to SQLite with is_synced=false
2. Come online → sync uploads job to server (success, gets job ID back)
3. But SQLite row still shows is_synced=false
4. Next sync tries to upload again → duplicate job

Here's my code:
[paste SyncService.uploadJobs() method]

What's wrong?
```

**AI Response:**
```
The problem is you're not updating the local SQLite row after successful upload.
You get the server job ID back, but never update the local row.

Fix:
```dart
Future<void> uploadJobs() async {
  final unsyncedJobs = await _db.getUnsyncedJobs();
  
  for (var localJob in unsyncedJobs) {
    try {
      // Upload to server
      final response = await _api.createJob(localJob);
      final serverJobId = response['id'];
      
      // THIS IS WHAT YOU'RE MISSING:
      // Update local row with server ID and mark as synced
      await _db.updateJob(
        localJob.id,
        {
          'server_id': serverJobId,  // Store server ID
          'is_synced': 1,             // Mark as synced
          'last_synced_at': DateTime.now().toIso8601String(),
        },
      );
      
      print('Job ${localJob.id} synced successfully');
    } catch (e) {
      print('Failed to sync job ${localJob.id}: $e');
      // Don't update is_synced, will retry later
    }
  }
}
```

**You:** "Perfect! But what if the job was edited on another device? How do I detect conflicts?"

**AI continues with conflict resolution strategy...**

### Tips for Better AI Outputs

1. **Be specific about technology versions**
   - ❌ "Use Prisma"
   - ✅ "Use Prisma 5.x with PostgreSQL"

2. **Provide context**
   - ❌ "Create a login screen"
   - ✅ "Create a Flutter login screen for a tradie app, with email/password fields, form validation, and API integration using Provider for state management"

3. **Ask for explanations**
   - Include: "Explain why you chose this approach"
   - This helps you learn, not just copy/paste

4. **Iterate on responses**
   - Don't accept first answer if not perfect
   - Ask: "Can you improve this to handle edge case X?"

5. **Request tests**
   - Always ask: "Now write tests for this code"

6. **Break complex features into parts**
   - ❌ "Build the entire offline sync system"
   - ✅ "First, show me how to detect when app goes online/offline"
   - Then: "Now show me how to queue changes while offline"
   - Then: "Now show me conflict resolution logic"

---

## Critical Implementation Details

### 1. Offline Sync Architecture (MOST IMPORTANT)

**The Challenge:**
Tradie in basement creates Job A at 9am (offline). Job saved to SQLite with `local_id=1, server_id=null, is_synced=false`. At 10am, comes outside, app syncs. Must upload Job A to server without duplicating.

**The Solution:**

**Data Model:**
```sql
-- SQLite schema
CREATE TABLE jobs (
  local_id INTEGER PRIMARY KEY AUTOINCREMENT,
  server_id TEXT,           -- NULL until synced
  is_synced INTEGER DEFAULT 0,
  is_deleted INTEGER DEFAULT 0,
  last_modified_at TEXT,
  last_synced_at TEXT,
  -- ... other job fields
);

CREATE TABLE sync_queue (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  entity_type TEXT,         -- "job", "quote", "invoice"
  entity_local_id INTEGER,
  operation TEXT,           -- "create", "update", "delete"
  created_at TEXT,
  synced_at TEXT
);
```

**Sync Flow:**

```dart
// mobile/lib/core/sync/sync_service.dart

class SyncService {
  Future<void> sync() async {
    if (!await _isOnline()) return;
    
    // STEP 1: Upload local changes
    await _uploadChanges();
    
    // STEP 2: Download server changes
    await _downloadChanges();
  }
  
  Future<void> _uploadChanges() async {
    // Get all unsynced items from queue
    final queue = await _db.getUnsyncedQueue();
    
    for (var item in queue) {
      try {
        if (item.operation == 'create') {
          // Upload new entity
          final localEntity = await _db.getEntity(
            item.entityType,
            item.entityLocalId,
          );
          
          final response = await _api.create(
            item.entityType,
            localEntity.toJson(),
          );
          
          // Update local entity with server ID
          await _db.updateEntity(
            item.entityType,
            item.entityLocalId,
            {
              'server_id': response['id'],
              'is_synced': 1,
              'last_synced_at': DateTime.now().toIso8601String(),
            },
          );
          
          // Mark queue item as synced
          await _db.markQueueItemSynced(item.id);
          
        } else if (item.operation == 'update') {
          // Upload changes
          final localEntity = await _db.getEntity(
            item.entityType,
            item.entityLocalId,
          );
          
          await _api.update(
            item.entityType,
            localEntity.serverId!,  // Use server ID
            localEntity.toJson(),
          );
          
          await _db.updateEntity(
            item.entityType,
            item.entityLocalId,
            {
              'is_synced': 1,
              'last_synced_at': DateTime.now().toIso8601String(),
            },
          );
          
          await _db.markQueueItemSynced(item.id);
          
        } else if (item.operation == 'delete') {
          // Soft delete on server
          final localEntity = await _db.getEntity(
            item.entityType,
            item.entityLocalId,
          );
          
          if (localEntity.serverId != null) {
            await _api.delete(
              item.entityType,
              localEntity.serverId!,
            );
          }
          
          // Remove from local DB
          await _db.deleteEntity(
            item.entityType,
            item.entityLocalId,
          );
          
          await _db.markQueueItemSynced(item.id);
        }
      } catch (e) {
        print('Sync failed for ${item.entityType} ${item.entityLocalId}: $e');
        // Leave in queue, will retry next sync
      }
    }
  }
  
  Future<void> _downloadChanges() async {
    // Get last sync timestamp
    final lastSync = await _prefs.getString('last_sync_timestamp');
    
    // Fetch changes since last sync
    final changes = await _api.getChangesSince(lastSync);
    
    for (var change in changes) {
      // Check if entity exists locally
      final existing = await _db.getEntityByServerId(
        change.entityType,
        change.serverId,
      );
      
      if (existing == null) {
        // New entity from server
        await _db.insertEntity(
          change.entityType,
          {
            ...change.data,
            'server_id': change.serverId,
            'is_synced': 1,
            'last_synced_at': DateTime.now().toIso8601String(),
          },
        );
      } else {
        // Entity exists, check for conflict
        if (existing.lastModifiedAt.isAfter(change.updatedAt)) {
          // Local is newer, conflict!
          await _handleConflict(existing, change);
        } else {
          // Server is newer, update local
          await _db.updateEntity(
            change.entityType,
            existing.localId,
            {
              ...change.data,
              'is_synced': 1,
              'last_synced_at': DateTime.now().toIso8601String(),
            },
          );
        }
      }
    }
    
    // Save sync timestamp
    await _prefs.setString(
      'last_sync_timestamp',
      DateTime.now().toIso8601String(),
    );
  }
  
  Future<void> _handleConflict(LocalEntity local, ServerChange server) {
    // Simple strategy: server wins, but notify user
    // (Better UX: show conflict resolution UI)
    
    await _db.updateEntity(
      server.entityType,
      local.localId,
      {
        ...server.data,
        'is_synced': 1,
        'last_synced_at': DateTime.now().toIso8601String(),
      },
    );
    
    // Show notification to user
    await _notificationService.show(
      'Sync Conflict',
      'Job "${local.customerName}" was updated on another device. '
      'Server version has been kept.',
    );
  }
}
```

**Key Points:**
- Use `sync_queue` table to track all changes made offline
- Dual IDs: `local_id` (SQLite) and `server_id` (PostgreSQL)
- Upload before download (push local changes first)
- Conflict resolution: server wins, but notify user
- Retry failed syncs automatically

### 2. GST Calculation (CRITICAL - Legal Requirement)

Australian GST is 10% of the subtotal. Invoices must clearly show GST breakdown.

```typescript
// backend/src/quotes/dto/calculate-totals.dto.ts

export function calculateQuoteTotals(lineItems: LineItemDto[]): {
  subtotal: number;
  gstAmount: number;
  totalAmount: number;
} {
  // Sum all line items
  const subtotal = lineItems.reduce((sum, item) => {
    return sum + (item.quantity * item.rate);
  }, 0);
  
  // GST is 10% of subtotal
  const gstAmount = subtotal * 0.10;
  
  // Total includes GST
  const totalAmount = subtotal + gstAmount;
  
  return {
    subtotal: Math.round(subtotal * 100) / 100,      // Round to 2 decimals
    gstAmount: Math.round(gstAmount * 100) / 100,
    totalAmount: Math.round(totalAmount * 100) / 100,
  };
}
```

**Validation:**
```typescript
// Validate totals match
if (Math.abs(quote.totalAmount - (quote.subtotal + quote.gstAmount)) > 0.01) {
  throw new BadRequestException('GST calculation mismatch');
}
```

**Display on Invoice:**
```
Line items subtotal:  $1,000.00
GST (10%):              $100.00
                      ----------
TOTAL:               $1,100.00

All prices include GST unless otherwise stated.
```

### 3. AI Quote Generation Prompts

**System Prompt for GPT-4:**
```typescript
const systemPrompt = `You are an expert Australian ${jobType} estimator. 
Generate accurate quote line items based on job descriptions.

Rules:
1. Use Australian dollars (AUD)
2. Include GST in pricing (10%)
3. Be specific in descriptions (e.g., "Install 15A GPO outlet" not "Electrical work")
4. Break down into itemized line items
5. Include labor AND materials separately
6. Use realistic Australian market rates for ${jobType} in ${city}
7. Consider job complexity from description

Return ONLY valid JSON in this format:
{
  "lineItems": [
    {
      "description": "Detailed description",
      "quantity": 1,
      "unit": "each|hour|meter",
      "rate": 100.00,
      "amount": 100.00
    }
  ],
  "confidence": 85,
  "notes": "Any assumptions made"
}`;

const userPrompt = `Job Type: ${jobType}
Description: ${jobDescription}
Location: ${address}
Customer Type: ${customerType} (residential/commercial)

Generate itemized quote.`;
```

**Example API Call:**
```typescript
const completion = await openai.chat.completions.create({
  model: "gpt-4-turbo",
  messages: [
    { role: "system", content: systemPrompt },
    { role: "user", content: userPrompt }
  ],
  temperature: 0.3,  // Lower = more consistent
  max_tokens: 1000,
  response_format: { type: "json_object" },  // Force JSON
});

const result = JSON.parse(completion.choices[0].message.content);
```

**Validation:**
```typescript
// Validate AI response
if (!result.lineItems || result.lineItems.length === 0) {
  throw new Error('AI did not generate line items');
}

if (result.confidence < 50) {
  // Low confidence, flag for manual review
  return {
    ...result,
    requiresReview: true,
    reviewReason: 'Low AI confidence score'
  };
}

// Check total amount is reasonable
const totalAmount = result.lineItems.reduce((sum, item) => 
  sum + item.amount, 0
);

if (totalAmount > 10000) {
  // High-value quote, require manual review
  return {
    ...result,
    requiresReview: true,
    reviewReason: 'Quote exceeds $10,000 threshold'
  };
}

return result;
```

### 4. Xero Invoice Sync

**OAuth Flow:**
```typescript
// backend/src/accounting/xero/xero.service.ts

import { XeroClient } from 'xero-node';

export class XeroService {
  private xeroClient: XeroClient;
  
  constructor() {
    this.xeroClient = new XeroClient({
      clientId: process.env.XERO_CLIENT_ID,
      clientSecret: process.env.XERO_CLIENT_SECRET,
      redirectUris: [`${process.env.API_URL}/accounting/xero/callback`],
      scopes: 'openid profile email accounting.transactions',
    });
  }
  
  // Step 1: Initiate OAuth
  async getAuthorizationUrl(userId: string): Promise<string> {
    const consentUrl = await this.xeroClient.buildConsentUrl();
    
    // Store state token to verify callback
    await this.redis.set(
      `xero_auth_${userId}`,
      'pending',
      'EX',
      600  // 10 min expiry
    );
    
    return consentUrl;
  }
  
  // Step 2: Handle callback, save tokens
  async handleCallback(code: string, userId: string) {
    const tokenSet = await this.xeroClient.apiCallback(code);
    
    // Store tokens in database (encrypted)
    await this.prisma.userXeroIntegration.upsert({
      where: { userId },
      create: {
        userId,
        accessToken: this.encrypt(tokenSet.access_token),
        refreshToken: this.encrypt(tokenSet.refresh_token),
        expiresAt: new Date(Date.now() + tokenSet.expires_in * 1000),
      },
      update: {
        accessToken: this.encrypt(tokenSet.access_token),
        refreshToken: this.encrypt(tokenSet.refresh_token),
        expiresAt: new Date(Date.now() + tokenSet.expires_in * 1000),
      },
    });
  }
  
  // Step 3: Sync invoice to Xero
  async syncInvoice(invoiceId: string) {
    const invoice = await this.prisma.invoice.findUnique({
      where: { id: invoiceId },
      include: { user: true, job: true },
    });
    
    // Get user's Xero tokens
    const integration = await this.prisma.userXeroIntegration.findUnique({
      where: { userId: invoice.userId },
    });
    
    if (!integration) {
      throw new Error('Xero not connected for this user');
    }
    
    // Refresh token if expired
    if (integration.expiresAt < new Date()) {
      await this.refreshAccessToken(invoice.userId);
    }
    
    // Set access token
    await this.xeroClient.setTokenSet({
      access_token: this.decrypt(integration.accessToken),
      refresh_token: this.decrypt(integration.refreshToken),
    });
    
    // Create invoice in Xero
    const xeroInvoice = {
      Type: 'ACCREC',  // Accounts Receivable
      Contact: {
        Name: invoice.job.customerName,
        EmailAddress: invoice.job.customerEmail,
        Phones: [{ PhoneType: 'DEFAULT', PhoneNumber: invoice.job.customerPhone }],
      },
      Date: invoice.createdAt.toISOString().split('T')[0],
      DueDate: invoice.dueDate?.toISOString().split('T')[0],
      InvoiceNumber: invoice.invoiceNumber,
      LineItems: (invoice.lineItems as any[]).map(item => ({
        Description: item.description,
        Quantity: item.quantity,
        UnitAmount: item.rate,
        AccountCode: '200',  // Sales account code
        TaxType: 'OUTPUT2',  // GST on Income (10%)
      })),
      Status: 'SUBMITTED',
    };
    
    const response = await this.xeroClient.accountingApi.createInvoices(
      integration.xeroTenantId,
      { invoices: [xeroInvoice] }
    );
    
    // Save Xero invoice ID
    await this.prisma.invoice.update({
      where: { id: invoiceId },
      data: {
        xeroInvoiceId: response.body.invoices[0].invoiceID,
        lastSyncedToXero: new Date(),
      },
    });
    
    return response.body.invoices[0];
  }
}
```

### 5. Stripe Payment Links

**Simple approach for MVP:**
```typescript
// backend/src/payments/stripe.service.ts

import Stripe from 'stripe';

export class StripeService {
  private stripe: Stripe;
  
  constructor() {
    this.stripe = new Stripe(process.env.STRIPE_SECRET_KEY, {
      apiVersion: '2023-10-16',
    });
  }
  
  async createPaymentLink(invoiceId: string): Promise<string> {
    const invoice = await this.prisma.invoice.findUnique({
      where: { id: invoiceId },
      include: { user: true, job: true },
    });
    
    // Create Stripe payment link
    const paymentLink = await this.stripe.paymentLinks.create({
      line_items: [
        {
          price_data: {
            currency: 'aud',
            product_data: {
              name: `Invoice ${invoice.invoiceNumber}`,
              description: `Job: ${invoice.job.description}`,
            },
            unit_amount: Math.round(invoice.totalAmount * 100), // Cents
          },
          quantity: 1,
        },
      ],
      after_completion: {
        type: 'redirect',
        redirect: {
          url: `${process.env.APP_URL}/invoices/${invoiceId}/paid`,
        },
      },
      metadata: {
        invoiceId: invoice.id,
        userId: invoice.userId,
      },
    });
    
    // Save payment link to invoice
    await this.prisma.invoice.update({
      where: { id: invoiceId },
      data: { stripePaymentLink: paymentLink.url },
    });
    
    return paymentLink.url;
  }
  
  // Webhook handler for payment success
  async handleWebhook(event: Stripe.Event) {
    if (event.type === 'checkout.session.completed') {
      const session = event.data.object as Stripe.Checkout.Session;
      const invoiceId = session.metadata.invoiceId;
      
      // Mark invoice as paid
      await this.prisma.invoice.update({
        where: { id: invoiceId },
        data: {
          status: 'PAID',
          paidAmount: session.amount_total / 100,
          paidDate: new Date(),
          stripePaymentId: session.payment_intent as string,
        },
      });
      
      // Send confirmation email
      await this.emailService.sendPaymentConfirmation(invoiceId);
    }
  }
}
```

---

## Testing & Deployment

### Testing Strategy

#### 1. Backend Unit Tests (Jest)

```bash
# Run tests
cd backend
npm test

# Watch mode during development
npm test -- --watch

# Coverage report
npm test -- --coverage
```

**Example test:**
```typescript
// backend/src/quotes/quotes.service.spec.ts

describe('QuotesService', () => {
  let service: QuotesService;
  let prisma: PrismaService;
  
  beforeEach(async () => {
    const module = await Test.createTestingModule({
      providers: [
        QuotesService,
        {
          provide: PrismaService,
          useValue: {
            quote: {
              create: jest.fn(),
              findUnique: jest.fn(),
            },
          },
        },
      ],
    }).compile();
    
    service = module.get<QuotesService>(QuotesService);
    prisma = module.get<PrismaService>(PrismaService);
  });
  
  describe('calculateTotals', () => {
    it('should calculate GST correctly', () => {
      const lineItems = [
        { description: 'Labor', quantity: 2, rate: 100, amount: 200 },
        { description: 'Materials', quantity: 1, rate: 150, amount: 150 },
      ];
      
      const totals = service.calculateTotals(lineItems);
      
      expect(totals.subtotal).toBe(350);
      expect(totals.gstAmount).toBe(35);  // 10% of 350
      expect(totals.totalAmount).toBe(385);
    });
    
    it('should round to 2 decimal places', () => {
      const lineItems = [
        { description: 'Test', quantity: 3, rate: 33.33, amount: 99.99 },
      ];
      
      const totals = service.calculateTotals(lineItems);
      
      expect(totals.subtotal).toBe(99.99);
      expect(totals.gstAmount).toBe(10.00);
      expect(totals.totalAmount).toBe(109.99);
    });
  });
  
  describe('createQuote', () => {
    it('should create quote with valid data', async () => {
      const createDto = {
        jobId: 'job-123',
        lineItems: [
          { description: 'Test', quantity: 1, rate: 100, amount: 100 },
        ],
      };
      
      const mockQuote = {
        id: 'quote-123',
        ...createDto,
        subtotal: 100,
        gstAmount: 10,
        totalAmount: 110,
      };
      
      jest.spyOn(prisma.quote, 'create').mockResolvedValue(mockQuote as any);
      
      const result = await service.create(createDto, 'user-123');
      
      expect(result).toEqual(mockQuote);
      expect(prisma.quote.create).toHaveBeenCalledWith({
        data: expect.objectContaining({
          userId: 'user-123',
          jobId: 'job-123',
          subtotal: 100,
          gstAmount: 10,
          totalAmount: 110,
        }),
      });
    });
  });
});
```

#### 2. Mobile Tests (Flutter)

```bash
# Run tests
cd mobile
flutter test

# Run with coverage
flutter test --coverage
genhtml coverage/lcov.info -o coverage/html
open coverage/html/index.html
```

**Example widget test:**
```dart
// mobile/test/features/auth/login_screen_test.dart

void main() {
  group('LoginScreen', () {
    testWidgets('should display email and password fields', (tester) async {
      await tester.pumpWidget(
        MaterialApp(home: LoginScreen()),
      );
      
      expect(find.byType(TextField), findsNWidgets(2));
      expect(find.text('Email'), findsOneWidget);
      expect(find.text('Password'), findsOneWidget);
    });
    
    testWidgets('should show error on invalid email', (tester) async {
      await tester.pumpWidget(
        MaterialApp(home: LoginScreen()),
      );
      
      // Enter invalid email
      await tester.enterText(
        find.byKey(Key('email_field')),
        'invalid-email',
      );
      
      // Tap login button
      await tester.tap(find.byKey(Key('login_button')));
      await tester.pump();
      
      // Should show validation error
      expect(find.text('Enter a valid email'), findsOneWidget);
    });
    
    testWidgets('should call API on valid login', (tester) async {
      final mockAuthService = MockAuthService();
      
      await tester.pumpWidget(
        ChangeNotifierProvider<AuthService>(
          create: (_) => mockAuthService,
          child: MaterialApp(home: LoginScreen()),
        ),
      );
      
      // Enter valid credentials
      await tester.enterText(
        find.byKey(Key('email_field')),
        'test@example.com',
      );
      await tester.enterText(
        find.byKey(Key('password_field')),
        'password123',
      );
      
      // Mock successful login
      when(mockAuthService.login(any, any))
        .thenAnswer((_) async => true);
      
      // Tap login
      await tester.tap(find.byKey(Key('login_button')));
      await tester.pump();
      
      // Verify API was called
      verify(mockAuthService.login('test@example.com', 'password123'))
        .called(1);
    });
  });
}
```

#### 3. Integration Tests

**Test offline sync end-to-end:**
```dart
// mobile/integration_test/offline_sync_test.dart

void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();
  
  group('Offline Sync', () {
    testWidgets('create job offline, sync when online', (tester) async {
      // Launch app
      await tester.pumpWidget(TradePilotApp());
      await tester.pumpAndSettle();
      
      // Login
      await tester.enterText(find.byKey(Key('email')), 'test@example.com');
      await tester.enterText(find.byKey(Key('password')), 'password');
      await tester.tap(find.byKey(Key('login_button')));
      await tester.pumpAndSettle();
      
      // Turn off internet (mock connectivity)
      await tester.runAsync(() async {
        await ConnectivityService.instance.setOffline();
      });
      
      // Create job
      await tester.tap(find.byIcon(Icons.add));
      await tester.pumpAndSettle();
      
      await tester.enterText(
        find.byKey(Key('customer_name')),
        'John Doe',
      );
      await tester.enterText(
        find.byKey(Key('customer_phone')),
        '0412345678',
      );
      await tester.tap(find.byKey(Key('save_job')));
      await tester.pumpAndSettle();
      
      // Verify job saved locally
      final db = await DatabaseHelper.instance.database;
      final jobs = await db.query('jobs', where: 'is_synced = 0');
      expect(jobs.length, 1);
      expect(jobs[0]['customer_name'], 'John Doe');
      
      // Turn on internet
      await tester.runAsync(() async {
        await ConnectivityService.instance.setOnline();
      });
      
      // Trigger sync
      await tester.drag(find.byType(ListView), Offset(0, 300));
      await tester.pumpAndSettle(Duration(seconds: 3));
      
      // Verify synced
      final syncedJobs = await db.query('jobs', where: 'is_synced = 1');
      expect(syncedJobs.length, 1);
      expect(syncedJobs[0]['server_id'], isNotNull);
    });
  });
}
```

### Deployment

#### Backend Deployment (AWS EC2)

**Step 1: Launch EC2 Instance**
```bash
# AWS Console:
# - EC2 → Launch Instance
# - Ubuntu 22.04 LTS
# - t3.small (2 vCPU, 2GB RAM) - $15/month
# - Sydney region (ap-southeast-2)
# - Security group: Allow SSH (22), HTTP (80), HTTPS (443)
# - Elastic IP (static IP address)

# SSH into instance
ssh -i your-key.pem ubuntu@YOUR_ELASTIC_IP
```

**Step 2: Install Dependencies**
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Node.js 20
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# Install PostgreSQL
sudo apt install postgresql postgresql-contrib
sudo -u postgres psql -c "CREATE DATABASE tradepilot;"
sudo -u postgres psql -c "CREATE USER tradepilot WITH PASSWORD 'your_password';"
sudo -u postgres psql -c "GRANT ALL PRIVILEGES ON DATABASE tradepilot TO tradepilot;"

# Install Redis
sudo apt install redis-server
sudo systemctl enable redis-server

# Install nginx
sudo apt install nginx
sudo systemctl enable nginx

# Install PM2 (process manager)
sudo npm install -g pm2
```

**Step 3: Deploy Backend**
```bash
# Clone repo
cd /var/www
sudo git clone https://github.com/YOUR_USERNAME/tradepilot-backend.git
cd tradepilot-backend

# Install dependencies
sudo npm install

# Create .env file
sudo nano .env
```

```env
NODE_ENV=production
PORT=3000

DATABASE_URL="postgresql://tradepilot:your_password@localhost:5432/tradepilot"

JWT_SECRET="your-super-secret-jwt-key-change-this"
JWT_EXPIRES_IN="7d"

OPENAI_API_KEY="sk-..."

STRIPE_SECRET_KEY="sk_live_..."
STRIPE_WEBHOOK_SECRET="whsec_..."

XERO_CLIENT_ID="..."
XERO_CLIENT_SECRET="..."

AWS_ACCESS_KEY_ID="..."
AWS_SECRET_ACCESS_KEY="..."
AWS_REGION="ap-southeast-2"
AWS_S3_BUCKET="tradepilot-files"

FRONTEND_URL="https://app.tradepilot.com.au"
API_URL="https://api.tradepilot.com.au"
```

```bash
# Run migrations
sudo npx prisma migrate deploy
sudo npx prisma generate

# Build production bundle
sudo npm run build

# Start with PM2
pm2 start dist/main.js --name tradepilot-api
pm2 save
pm2 startup
```

**Step 4: Configure Nginx**
```bash
sudo nano /etc/nginx/sites-available/tradepilot
```

```nginx
server {
    listen 80;
    server_name api.tradepilot.com.au;
    
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

```bash
# Enable site
sudo ln -s /etc/nginx/sites-available/tradepilot /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx

# Install SSL (Let's Encrypt)
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d api.tradepilot.com.au
```

**Step 5: Set Up Monitoring**
```bash
# PM2 monitoring
pm2 install pm2-logrotate
pm2 set pm2-logrotate:max_size 10M
pm2 set pm2-logrotate:retain 7

# Install monitoring (optional)
# Sentry, Datadog, or CloudWatch
```

#### Mobile App Deployment

**iOS (TestFlight)**
```bash
cd mobile

# Build for release
flutter build ios --release

# Open Xcode
open ios/Runner.xcworkspace

# In Xcode:
# 1. Select "Any iOS Device" target
# 2. Product → Archive
# 3. Distribute App → App Store Connect
# 4. Upload to TestFlight
# 5. Add beta testers in App Store Connect
```

**Android (Google Play Internal Testing)**
```bash
# Create keystore (one-time)
keytool -genkey -v -keystore ~/tradepilot-key.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias tradepilot

# Configure signing (android/key.properties)
storePassword=your_password
keyPassword=your_password
keyAlias=tradepilot
storeFile=/Users/you/tradepilot-key.jks

# Build release bundle
flutter build appbundle --release

# Upload to Google Play Console
# 1. Create app in Play Console
# 2. Production → Internal testing → Create release
# 3. Upload build/app/outputs/bundle/release/app-release.aab
# 4. Add testers via email list
```

---

## Troubleshooting & Resources

### Common Issues

#### 1. Flutter Build Fails

**Problem:** `flutter build` fails with dependency errors

**Solution:**
```bash
# Clean build cache
flutter clean
flutter pub get

# Update dependencies
flutter pub upgrade

# If still failing, delete pubspec.lock
rm pubspec.lock
flutter pub get
```

#### 2. Prisma Migration Fails

**Problem:** Migration fails with "relation already exists"

**Solution:**
```bash
# Reset database (DEVELOPMENT ONLY - DELETES DATA)
npx prisma migrate reset

# Or manually drop tables
psql -U tradepilot -d tradepilot -c "DROP SCHEMA public CASCADE; CREATE SCHEMA public;"
npx prisma migrate deploy
```

#### 3. Offline Sync Not Working

**Problem:** Jobs created offline don't sync when online

**Checklist:**
- [ ] Check `sync_queue` table has entries
- [ ] Verify `is_synced` flag is false
- [ ] Check network connectivity detection
- [ ] Look for errors in sync service logs
- [ ] Verify API authentication token is valid
- [ ] Check server_id is being saved after upload

**Debug:**
```dart
// Add logging to sync service
print('Starting sync...');
print('Unsynced jobs: ${unsyncedJobs.length}');
for (var job in unsyncedJobs) {
  print('Syncing job ${job.localId}...');
  try {
    // ... upload logic
    print('Job ${job.localId} synced, server ID: ${response.id}');
  } catch (e) {
    print('Error syncing job ${job.localId}: $e');
  }
}
```

#### 4. AI Quote Generation Too Slow

**Problem:** GPT-4 API takes >10 seconds to respond

**Solutions:**
- Use `gpt-4-turbo` instead of `gpt-4` (faster)
- Reduce `max_tokens` (1000 is enough for quotes)
- Cache common job types locally
- Show loading indicator immediately
- Allow user to continue editing while AI generates

#### 5. App Rejected from App Store

**Common rejection reasons:**
- Missing privacy policy
- Crash on launch
- Broken functionality
- Insufficient description
- Missing screenshots

**Solution:**
```
# Add privacy policy
1. Create privacy policy page (use generator like termly.io)
2. Link in app settings screen
3. Add to app store listing

# Test thoroughly
- Test on real devices (not just simulator)
- Test offline mode extensively
- Fix all crashes before submission
```

### Learning Resources

**Flutter:**
- Official docs: https://docs.flutter.dev/
- Flutter Codelabs: https://docs.flutter.dev/codelabs
- Flutter YouTube channel: https://www.youtube.com/@flutterdev
- Flutter Community: https://flutter.dev/community

**NestJS:**
- Official docs: https://docs.nestjs.com/
- NestJS Courses: https://courses.nestjs.com/
- GitHub repo: https://github.com/nestjs/nest

**Prisma:**
- Docs: https://www.prisma.io/docs
- Schema reference: https://www.prisma.io/docs/reference/api-reference/prisma-schema-reference

**AI Coding:**
- GitHub Copilot docs: https://docs.github.com/copilot
- Cursor docs: https://cursor.sh/docs
- Prompt engineering guide: https://platform.openai.com/docs/guides/prompt-engineering

**Australian Compliance:**
- ASIC business names: https://asic.gov.au/for-business-and-companies/business-names/
- ATO GST info: https://www.ato.gov.au/business/gst/
- Privacy Act: https://www.oaic.gov.au/privacy/

### Getting Help

**When Stuck:**
1. Search GitHub issues (NestJS, Flutter, Prisma repos)
2. Ask Claude/ChatGPT with full error message + code
3. Stack Overflow (tag with #flutter, #nestjs, #prisma)
4. Reddit: r/FlutterDev, r/Nestjs_framework
5. Discord: Flutter Community, NestJS Discord

**Provide This Info When Asking:**
- Error message (full stack trace)
- Code that causes error
- What you've tried
- Expected vs actual behavior
- Environment (Flutter version, Node version, OS)

---

## Next Steps

### Week 1 Action Items

**By End of Week 1, You Should Have:**
- [ ] Development environment fully set up
- [ ] GitHub repos created (backend + mobile)
- [ ] Basic NestJS backend running locally
- [ ] Basic Flutter app running on simulator/emulator
- [ ] Database schema designed in Prisma
- [ ] Completed Dart language tour
- [ ] First AI-assisted code generated

**Your First AI Prompts to Try:**

1. **Backend Setup:**
```
Create a NestJS authentication module with:
- User registration endpoint
- Login endpoint with JWT
- Password hashing with bcrypt
- Auth guard for protected routes
Use Prisma for database access.
Show complete code for auth.service.ts and auth.controller.ts.
```

2. **Mobile Setup:**
```
Create a Flutter login screen with:
- Email text field with validation
- Password text field (obscured)
- Login button
- "Don't have an account? Register" link
- Loading state during API call
- Error display with SnackBar
Use Provider for state management.
```

### Timeline Checkpoints

**Week 4:** Backend APIs complete (jobs, quotes, invoices)
**Week 8:** Mobile app functional with offline support
**Week 10:** Integrations working (Xero, Stripe, Maps)
**Week 12:** Testing complete, bugs fixed
**Week 16:** Beta testing with 10-20 electricians
**Week 20:** Public launch ready

### Budget Allocation

**Development (16-20 weeks):**
- Your time: $0 (sweat equity) or $80,000-$120,000 if hiring
- AI coding tools: $30/month × 5 months = $150
- AWS (dev): $50/month × 5 months = $250
- Domains: $50/year
- Apple Developer: $99/year
- Google Play: $25 one-time
- **Total MVP: $574 (if you do coding yourself)**

**Post-Launch (Monthly):**
- AWS hosting: $400/month (grows with users)
- OpenAI API: $50-200/month (based on quote volume)
- Stripe fees: 1.75% of revenue
- Third-party APIs: $200/month
- **Total: ~$650-850/month + 1.75% of revenue**

---

## Final Thoughts

**You're building TradePilot to solve a real problem:** Tradies spend 18.3 hours weekly on admin, losing evenings and weekends. Your app gives them that time back.

**Critical success factors:**
1. **Offline-first** - This is non-negotiable
2. **Mobile-first** - 70% of dev effort on mobile
3. **AI-assisted** quoting - Transparent, not black box
4. **Focus ruthlessly** - Say no to feature creep
5. **Launch fast** - 16-20 weeks to beta, not 12 months

**The path ahead:**
- Weeks 1-4: Build foundation
- Weeks 5-12: Build features
- Weeks 13-16: Polish and prep
- Weeks 17-20: Beta testing
- Day 121: Public launch
- Day 210: 50 paying customers

**You've got this!** With AI coding assistants, your TypeScript background, and this roadmap, you can build TradePilot even as a solo founder. The market is validated, the gaps are clear, and the opportunity is real.

Start with Week 1, Day 1. Set up your environment. Generate your first AI-assisted code. Build one feature at a time. Stay focused on the core value: **saving tradies' time.**

The tradies are waiting. Let's build something they'll love.

---

**Questions?** Re-read relevant sections, ask Claude/ChatGPT, or join Flutter/NestJS communities. You've got everything you need right here.

**Ready to start?** Tomorrow morning, run:
```bash
nest new tradepilot-backend
flutter create tradepilot-mobile
```

And you're off to the races. 🚀

---

*This guide will be updated as you progress. Save it, reference it, and adjust as needed for your specific situation.*
