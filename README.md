# Maeson Real Estate Backend API

A comprehensive backend API for a real estate website built with Node.js, Express, and MongoDB.

## Features

- 🔐 **Authentication & Authorization**: JWT-based auth with role-based access control (Buyer, Seller, Agent, Admin)
- 🏡 **Property Management**: Full CRUD operations for property listings
- 🖼️ **Image Upload**: Cloudinary integration for property images
- 📧 **Inquiry System**: Users can send inquiries about properties
- ⭐ **Reviews & Ratings**: Property reviews with admin approval
- ❤️ **Favorites**: Save favorite properties
- 🔍 **Advanced Search**: Filter by price, location, property type, and more
- 📱 **User Profiles**: Comprehensive user management for buyers, sellers, and agents
- 🛡️ **Security**: Helmet, CORS, rate limiting, and password hashing

## Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JWT (JSON Web Tokens)
- **Image Upload**: Cloudinary
- **Email**: Nodemailer
- **Validation**: Express-validator
- **Security**: Helmet, CORS, bcryptjs

## Project Structure

```
maeson-backend/
├── config/
│   ├── database.js          # MongoDB connection
│   └── cloudinary.js        # Cloudinary configuration
├── controllers/
│   ├── authController.js    # Authentication logic
│   ├── propertyController.js # Property operations
│   ├── userController.js    # User management
│   ├── inquiryController.js # Inquiry handling
│   ├── reviewController.js  # Review management
│   └── favoriteController.js # Favorites logic
├── middleware/
│   ├── auth.js              # Authentication middleware
│   ├── errorHandler.js      # Error handling
│   └── upload.js            # File upload middleware
├── models/
│   ├── User.js              # User schema
│   ├── Property.js          # Property schema
│   ├── Inquiry.js           # Inquiry schema
│   ├── Review.js            # Review schema
│   └── Favorite.js          # Favorite schema
├── routes/
│   ├── authRoutes.js        # Auth endpoints
│   ├── propertyRoutes.js    # Property endpoints
│   ├── userRoutes.js        # User endpoints
│   ├── inquiryRoutes.js     # Inquiry endpoints
│   ├── reviewRoutes.js      # Review endpoints
│   └── favoriteRoutes.js    # Favorite endpoints
├── utils/
│   ├── auth.js              # Auth utilities
│   └── cloudinary.js        # Cloudinary utilities
├── .env.example             # Environment variables template
├── .gitignore              # Git ignore file
├── package.json            # Dependencies
└── server.js               # Entry point
```

## Installation

### Prerequisites

- Node.js (v14 or higher)
- MongoDB (local or MongoDB Atlas)
- Cloudinary account (for image uploads)
- Gmail account (for email notifications)

### Setup Steps

1. **Clone or navigate to the project directory**

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   
   Copy `.env.example` to `.env`:
   ```bash
   copy .env.example .env
   ```

   Edit `.env` and fill in your configuration:
   ```env
   PORT=5000
   NODE_ENV=development

   # MongoDB - Use one of these:
   MONGODB_URI=mongodb://localhost:27017/maeson-realestate
   # OR for MongoDB Atlas:
   # MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/maeson-realestate

   # JWT Secret (change this!)
   JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
   JWT_EXPIRE=7d

   # Cloudinary (sign up at cloudinary.com)
   CLOUDINARY_CLOUD_NAME=your_cloud_name
   CLOUDINARY_API_KEY=your_api_key
   CLOUDINARY_API_SECRET=your_api_secret

   # Email (for Gmail, enable "App Passwords" in your Google account)
   EMAIL_HOST=smtp.gmail.com
   EMAIL_PORT=587
   EMAIL_USER=your_email@gmail.com
   EMAIL_PASSWORD=your_app_password
   EMAIL_FROM=noreply@maeson.com

   # Frontend URL (for CORS)
   FRONTEND_URL=http://localhost:3000
   ```

4. **Start MongoDB**
   
   If using local MongoDB:
   ```bash
   # Make sure MongoDB is running on your system
   ```

   If using MongoDB Atlas, just ensure your connection string is correct in `.env`

5. **Run the application**

   Development mode (with auto-restart):
   ```bash
   npm run dev
   ```

   Production mode:
   ```bash
   npm start
   ```

6. **Test the API**
   
   Open your browser or Postman and visit:
   ```
   http://localhost:5000/api/health
   ```

   You should see:
   ```json
   {
     "status": "success",
     "message": "Maeson Real Estate API is running",
     "timestamp": "2025-12-15T..."
   }
   ```

## API Endpoints

### Authentication (`/api/auth`)

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| POST | `/register` | Register new user | Public |
| POST | `/login` | Login user | Public |
| GET | `/me` | Get current user | Private |
| PUT | `/updatedetails` | Update user details | Private |
| PUT | `/updatepassword` | Update password | Private |

### Properties (`/api/properties`)

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| GET | `/` | Get all properties (with filters) | Public |
| GET | `/featured` | Get featured properties | Public |
| GET | `/:id` | Get single property | Public |
| POST | `/` | Create property | Private (Seller/Agent/Admin) |
| PUT | `/:id` | Update property | Private (Owner/Admin) |
| DELETE | `/:id` | Delete property | Private (Owner/Admin) |
| POST | `/:id/images` | Upload property images | Private (Owner/Admin) |

**Query Parameters for GET /properties:**
- `propertyType`: house, apartment, condo, townhouse, villa, land, commercial, office
- `listingType`: sale, rent, lease
- `status`: available, pending, sold, rented
- `city`: filter by city
- `state`: filter by state
- `minPrice`: minimum price
- `maxPrice`: maximum price
- `bedrooms`: minimum bedrooms
- `bathrooms`: minimum bathrooms
- `search`: text search in title/description
- `sort`: price-asc, price-desc, oldest, or default (newest)
- `page`: page number (default: 1)
- `limit`: items per page (default: 10)

### Users (`/api/users`)

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| GET | `/` | Get all users | Private (Admin) |
| GET | `/agents` | Get all agents | Public |
| GET | `/:id` | Get user by ID | Public |
| GET | `/:id/properties` | Get user's properties | Public |
| PUT | `/:id` | Update user | Private (Admin) |
| DELETE | `/:id` | Delete user | Private (Admin) |

### Inquiries (`/api/inquiries`)

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| POST | `/` | Create inquiry | Private |
| GET | `/sent` | Get sent inquiries | Private |
| GET | `/received` | Get received inquiries | Private |
| PUT | `/:id/status` | Update inquiry status | Private (Recipient) |
| DELETE | `/:id` | Delete inquiry | Private (Sender) |

### Reviews (`/api/reviews`)

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| GET | `/property/:propertyId` | Get property reviews | Public |
| POST | `/` | Create review | Private |
| GET | `/user` | Get user's reviews | Private |
| PUT | `/:id` | Update review | Private (Owner) |
| DELETE | `/:id` | Delete review | Private (Owner/Admin) |
| PUT | `/:id/approve` | Approve review | Private (Admin) |

### Favorites (`/api/favorites`)

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| GET | `/` | Get user's favorites | Private |
| POST | `/` | Add to favorites | Private |
| PUT | `/:id` | Update favorite notes | Private |
| DELETE | `/:id` | Remove from favorites | Private |
| GET | `/check/:propertyId` | Check if favorited | Private |

## User Roles

- **Buyer**: Can view properties, send inquiries, write reviews, save favorites
- **Seller**: All buyer permissions + create and manage their properties
- **Agent**: All seller permissions + can be assigned to properties
- **Admin**: Full access to all resources, can approve reviews

## Authentication

The API uses JWT (JSON Web Tokens) for authentication. Include the token in the Authorization header:

```
Authorization: Bearer YOUR_JWT_TOKEN
```

## Example Requests

### Register a User

```bash
POST http://localhost:5000/api/auth/register
Content-Type: application/json

{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "password": "password123",
  "phone": "+1234567890",
  "role": "buyer"
}
```

### Create a Property

```bash
POST http://localhost:5000/api/properties
Authorization: Bearer YOUR_TOKEN
Content-Type: application/json

{
  "title": "Beautiful Family Home",
  "description": "Spacious 4-bedroom house in a quiet neighborhood",
  "price": 450000,
  "propertyType": "house",
  "listingType": "sale",
  "address": {
    "street": "123 Main St",
    "city": "Springfield",
    "state": "IL",
    "zipCode": "62701"
  },
  "bedrooms": 4,
  "bathrooms": 3,
  "squareFeet": 2500,
  "features": ["Garage", "Backyard", "Fireplace"],
  "amenities": ["Pool", "Gym", "Park nearby"]
}
```

### Search Properties

```bash
GET http://localhost:5000/api/properties?city=Springfield&minPrice=200000&maxPrice=500000&bedrooms=3&sort=price-asc
```

## Email Setup (Gmail)

To enable email notifications:

1. Go to your Google Account settings
2. Enable 2-Step Verification
3. Generate an "App Password" for Mail
4. Use this app password in your `.env` file as `EMAIL_PASSWORD`

## Cloudinary Setup

1. Sign up at [cloudinary.com](https://cloudinary.com)
2. Get your Cloud Name, API Key, and API Secret from the dashboard
3. Add them to your `.env` file

## Common Issues

### MongoDB Connection Error
- Make sure MongoDB is running
- Check your connection string in `.env`
- For Atlas, ensure your IP is whitelisted

### Port Already in Use
- Change the PORT in `.env` to a different number

### Cloudinary Upload Fails
- Verify your Cloudinary credentials
- Check file size (max 5MB per image)

## Development

For development with auto-reload:

```bash
npm run dev
```

This uses nodemon to automatically restart the server when files change.

## Production Deployment

1. Set `NODE_ENV=production` in your environment
2. Use a proper MongoDB instance (MongoDB Atlas recommended)
3. Set a strong `JWT_SECRET`
4. Configure proper CORS settings for your frontend domain
5. Consider adding rate limiting for production
6. Use HTTPS in production

## Support

For issues or questions, please check:
- MongoDB connection issues: Verify `.env` configuration
- Authentication errors: Check JWT_SECRET and token format
- File upload issues: Verify Cloudinary credentials

## License

ISC

---

**Built with ❤️ for Maeson Real Estate**
