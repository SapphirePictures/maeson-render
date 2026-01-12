# 🚀 Quick Start Guide - Maeson Real Estate

This guide will help you get your real estate website up and running in minutes!

## 📋 Prerequisites

Before you begin, make sure you have:
- ✅ Node.js installed (v14 or higher) - [Download here](https://nodejs.org/)
- ✅ MongoDB installed locally OR a MongoDB Atlas account - [Get free account](https://www.mongodb.com/cloud/atlas)
- ✅ Code editor (VS Code recommended)

## 🎯 Step-by-Step Setup

### Step 1: Install Backend Dependencies

Open terminal in VS Code and run:

```bash
cd "Maeson Backend"
npm install
```

Wait for all packages to install (this may take 2-3 minutes).

### Step 2: Configure Backend Environment

1. Open the file `.env.example` in the "Maeson Backend" folder
2. Copy its contents
3. Create a new file named `.env` in the same folder
4. Paste the contents and update these values:

```env
# Required - Change these!
PORT=5000
MONGODB_URI=mongodb://localhost:27017/maeson-realestate
JWT_SECRET=change_this_to_a_random_secret_string_12345
FRONTEND_URL=http://localhost:5173

# Optional - For image uploads (can add later)
CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=

# Optional - For emails (can add later)
EMAIL_USER=
EMAIL_PASSWORD=
```

**Important:** Change the `JWT_SECRET` to any random string (e.g., "mySecretKey2025")

### Step 3: Start MongoDB

**Option A - Local MongoDB:**
If you installed MongoDB locally, it should already be running. If not:
- Windows: MongoDB usually starts automatically
- Mac/Linux: Run `mongod` in a new terminal

**Option B - MongoDB Atlas (Cloud):**
1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create free account and cluster
3. Get your connection string
4. Replace `MONGODB_URI` in `.env` with your connection string

### Step 4: Start the Backend Server

In the terminal (still in "Maeson Backend" folder):

```bash
npm run dev
```

You should see:
```
🚀 Server running in development mode on port 5000
📦 MongoDB Connected: localhost
```

**✅ Backend is ready!** Keep this terminal open.

### Step 5: Install Frontend Dependencies

Open a **NEW terminal** (don't close the backend one) and run:

```bash
cd "Real Estate Agency Website"
npm install
```

Wait for installation to complete.

### Step 6: Start the Frontend

In the same terminal:

```bash
npm run dev
```

You should see:
```
VITE ready in XXX ms
Local: http://localhost:5173/
```

**✅ Frontend is ready!**

### Step 7: Test the Application

1. Open your browser and go to: **http://localhost:5173**
2. You should see the Maeson Realty homepage
3. Click "Sign Up" in the header
4. Create a test account
5. Explore the features!

## 🎉 You're All Set!

Your real estate platform is now running with:
- ✅ User authentication (register/login)
- ✅ Property listings
- ✅ Search and filters
- ✅ User favorites
- ✅ Property inquiries
- ✅ User profiles

## 🧪 Testing Features

### Test User Registration
1. Click "Sign Up"
2. Fill in the form:
   - First Name: John
   - Last Name: Doe
   - Email: john@example.com
   - Password: password123
   - Role: Buyer
3. Click "Create Account"
4. You'll be logged in automatically

### Test Adding Properties (For Sellers/Agents)
Currently, properties need to be added via the API. You can:
1. Use a tool like Postman
2. Or wait for the admin panel (coming soon)

### Test Favorites
1. Browse properties
2. Click on a property
3. Click the heart icon to save it
4. Go to "My Favorites" from the user menu

## ❗ Troubleshooting

### Backend won't start
**Error: "MongoDB connection failed"**
- Check if MongoDB is running
- Verify `MONGODB_URI` in `.env` is correct
- For Atlas, check your IP is whitelisted

**Error: "Port 5000 already in use"**
- Change `PORT=5001` in `.env`
- Restart the backend server

### Frontend won't start
**Error: "Failed to fetch"**
- Make sure backend is running on port 5000
- Check `.env` file in frontend has `VITE_API_URL=http://localhost:5000/api`

**Error: "Module not found"**
- Delete `node_modules` folder
- Run `npm install` again

### Can't login/register
**Error: "Network Error"**
- Backend is not running - start it first
- Check browser console for specific errors

**Error: "Invalid credentials"**
- Make sure you're using the correct email/password
- Check caps lock is off

### No properties showing
- The database is empty initially
- You need to add properties via the API
- Or use the static data temporarily

## 📝 Adding Sample Properties

To test with some properties, you can add them via the API:

1. First, register and login to get a token
2. Use Postman or curl to POST to `http://localhost:5000/api/properties`
3. Include your token in headers: `Authorization: Bearer YOUR_TOKEN`
4. Send property data as JSON

**Example property:**
```json
{
  "title": "Luxury Villa in Ikoyi",
  "description": "Beautiful 5-bedroom villa with pool",
  "price": 850000000,
  "propertyType": "house",
  "listingType": "sale",
  "address": {
    "street": "123 Main St",
    "city": "Lagos",
    "state": "Lagos",
    "zipCode": "100001"
  },
  "bedrooms": 5,
  "bathrooms": 6,
  "squareFeet": 5000,
  "features": ["Pool", "Garden", "Garage"],
  "amenities": ["Gym", "Security"],
  "images": [
    {
      "url": "https://images.unsplash.com/photo-1600596542815-ffad4c1539a9"
    }
  ]
}
```

## 🔧 Development Workflow

### When working on the project:

1. **Always start backend first:**
   ```bash
   cd "Maeson Backend"
   npm run dev
   ```

2. **Then start frontend:**
   ```bash
   cd "Real Estate Agency Website"
   npm run dev
   ```

3. **Make changes and see them live:**
   - Backend: Changes require restart (Ctrl+C then `npm run dev`)
   - Frontend: Changes auto-reload in browser

## 📚 What's Next?

Now that your app is running, you can:

1. **Customize the design** - Edit files in `src/components`
2. **Add more features** - Check the backend API docs
3. **Deploy to production** - See deployment guide (coming soon)
4. **Add Cloudinary** - For image uploads
5. **Configure emails** - For notifications

## 🆘 Need Help?

If you get stuck:
1. Check the error message in the terminal
2. Look at browser console (F12) for frontend errors
3. Review the [INTEGRATION_GUIDE.md](./INTEGRATION_GUIDE.md) for detailed info
4. Check the backend README.md for API documentation

## 🎯 Quick Reference

**Backend URL:** http://localhost:5000
**Frontend URL:** http://localhost:5173
**API Base:** http://localhost:5000/api

**Stop servers:** Press `Ctrl+C` in the terminal

**Restart servers:**
- Backend: `npm run dev`
- Frontend: `npm run dev`

---

**Status**: ✅ Setup Complete!
**Version**: 1.0.0
**Last Updated**: December 17, 2025
