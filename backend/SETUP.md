# TradePilot Backend Setup

## Overview
NestJS + TypeScript backend for TradePilot - a tradie management application.

## Prerequisites
- Node.js 20.x or higher
- PostgreSQL 15+
- npm or yarn

## Installation

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Set up environment variables:**
   ```bash
   cp .env.example .env
   ```

   Edit `.env` and update the following:
   - `DATABASE_URL`: Your PostgreSQL connection string
   - `JWT_SECRET`: A secure random string for JWT signing
   - `OPENAI_API_KEY`: Your OpenAI API key (for AI quote generation)
   - Other API keys as needed (Stripe, Xero, AWS)

3. **Set up the database:**
   ```bash
   # Create the database (if not exists)
   createdb tradepilot

   # Run Prisma migrations
   npx prisma migrate dev --name init

   # Generate Prisma client
   npx prisma generate
   ```

## Running the Application

### Development mode
```bash
npm run start:dev
```

The API will be available at `http://localhost:3000/api`

### Production mode
```bash
npm run build
npm run start:prod
```

## Database Management

### View database in Prisma Studio
```bash
npx prisma studio
```

### Create a new migration
```bash
npx prisma migrate dev --name your_migration_name
```

### Reset database (⚠️ CAUTION: Deletes all data)
```bash
npx prisma migrate reset
```

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login and get JWT token
- `GET /api/auth/me` - Get current user (requires authentication)

### Example Register Request
```json
{
  "email": "john@example.com",
  "password": "securepassword123",
  "firstName": "John",
  "lastName": "Doe",
  "phone": "0412345678",
  "businessName": "John's Electrical",
  "abn": "12345678901"
}
```

### Example Login Request
```json
{
  "email": "john@example.com",
  "password": "securepassword123"
}
```

### Authentication
Include the JWT token in the Authorization header for protected routes:
```
Authorization: Bearer <your_jwt_token>
```

## Project Structure

```
backend/
├── src/
│   ├── auth/              # Authentication module
│   │   ├── dto/           # Data transfer objects
│   │   ├── guards/        # Auth guards
│   │   ├── strategies/    # Passport strategies
│   │   ├── auth.controller.ts
│   │   ├── auth.service.ts
│   │   └── auth.module.ts
│   ├── database/          # Database module
│   │   ├── prisma.service.ts
│   │   └── database.module.ts
│   ├── app.module.ts      # Root module
│   └── main.ts            # Application entry point
├── prisma/
│   └── schema.prisma      # Database schema
├── .env                   # Environment variables
└── package.json
```

## Development Guidelines

### Adding a New Module
```bash
nest g module feature-name
nest g controller feature-name
nest g service feature-name
```

### Code Style
- Use ESLint and Prettier (configured)
- Run `npm run lint` to check code style
- Run `npm run format` to auto-format code

## Testing

### Run unit tests
```bash
npm run test
```

### Run e2e tests
```bash
npm run test:e2e
```

### Test coverage
```bash
npm run test:cov
```

## Troubleshooting

### Prisma Client Not Found
```bash
npx prisma generate
```

### Database Connection Issues
1. Check PostgreSQL is running
2. Verify DATABASE_URL in .env
3. Ensure database exists: `createdb tradepilot`

### Port Already in Use
Change the PORT in .env file or kill the process using the port:
```bash
lsof -ti:3000 | xargs kill
```

## Next Steps

According to the TradePilot Development Guide:
- [ ] Create Jobs module (Week 3)
- [ ] Create Quotes module (Week 3)
- [ ] Create Invoices module (Week 4)
- [ ] Implement AI quote generation with OpenAI (Week 4)
- [ ] Add Xero integration (Week 9)
- [ ] Add Stripe payment processing (Week 9)

## Resources

- [NestJS Documentation](https://docs.nestjs.com/)
- [Prisma Documentation](https://www.prisma.io/docs)
- [TradePilot Development Guide](../TradePilot-Development-Guide.md)
