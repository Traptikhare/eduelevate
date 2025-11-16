# 🎓 EduElevate Backend API

Complete REST API for EduElevate platform built with Node.js, Express, and MongoDB.

## 🚀 Features

- ✅ User Authentication (Register/Login with JWT)
- ✅ Opportunities CRUD (Create, Read, Update, Delete)
- ✅ Application Tracking
- ✅ Resume Management
- ✅ User Profile Management
- ✅ Bookmarks System
- ✅ Role-based Access Control (Student/Admin)
- ✅ MongoDB Database with Mongoose
- ✅ Password Hashing with bcrypt
- ✅ Input Validation

## 📋 Prerequisites

Before running the backend, make sure you have:

- **Node.js** (v14 or higher) - [Download](https://nodejs.org/)
- **MongoDB** (local or MongoDB Atlas) - [Download](https://www.mongodb.com/try/download/community)
- **npm** or **yarn** package manager

## ⚙️ Installation

### Step 1: Navigate to backend folder
```bash
cd c:\Users\Lenovo\OneDrive\Documents\PROJECT1\eduelevate_backend
```

### Step 2: Install dependencies
```bash
npm install
```

### Step 3: Configure environment variables
Edit the `.env` file and update:
```env
MONGO_URI=mongodb://localhost:27017/eduelevate
JWT_SECRET=your_secret_key_here
PORT=5000
```

**For MongoDB Atlas (Cloud):**
```env
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/eduelevate
```

### Step 4: Start MongoDB (if using local)
```bash
# Windows
net start MongoDB

# Mac/Linux
sudo systemctl start mongod
```

### Step 5: Run the server
```bash
# Development mode (with auto-restart)
npm run dev

# Production mode
npm start
```

Server will run on: **http://localhost:5000**

## 📡 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user (Protected)

### Opportunities
- `GET /api/opportunities` - Get all opportunities (with filters)
- `GET /api/opportunities/:id` - Get single opportunity
- `POST /api/opportunities` - Create opportunity (Admin only)
- `PUT /api/opportunities/:id` - Update opportunity (Admin only)
- `DELETE /api/opportunities/:id` - Delete opportunity (Admin only)

### Applications
- `GET /api/applications` - Get user's applications (Protected)
- `POST /api/applications` - Apply to opportunity (Protected)
- `PUT /api/applications/:id` - Update application status (Protected)
- `DELETE /api/applications/:id` - Withdraw application (Protected)

### Resumes
- `GET /api/resumes` - Get all resumes (Protected)
- `GET /api/resumes/:id` - Get single resume (Protected)
- `POST /api/resumes` - Create resume (Protected)
- `PUT /api/resumes/:id` - Update resume (Protected)
- `DELETE /api/resumes/:id` - Delete resume (Protected)

### Users
- `GET /api/users/profile` - Get user profile (Protected)
- `PUT /api/users/profile` - Update profile (Protected)
- `POST /api/users/bookmarks/:id` - Add/Remove bookmark (Protected)

## 🧪 Testing API with Postman

### 1. Register User
```
POST http://localhost:5000/api/auth/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123",
  "college": "IIT Delhi",
  "course": "Computer Science"
}
```

### 2. Login User
```
POST http://localhost:5000/api/auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "password123"
}
```

Response will include a `token`. Copy this token!

### 3. Get Opportunities (use token)
```
GET http://localhost:5000/api/opportunities
Authorization: Bearer YOUR_TOKEN_HERE
```

### 4. Create Opportunity (Admin only)
```
POST http://localhost:5000/api/opportunities
Authorization: Bearer YOUR_ADMIN_TOKEN
Content-Type: application/json

{
  "title": "Google Internship",
  "type": "Internship",
  "company": "Google",
  "description": "Summer internship program",
  "stream": "Computer Science",
  "deadline": "2025-12-31",
  "stipend": "₹80,000/month"
}
```

## 🔐 Authentication

The API uses JWT (JSON Web Tokens) for authentication.

**To access protected routes:**
1. Login to get a token
2. Include token in Authorization header:
   ```
   Authorization: Bearer YOUR_TOKEN_HERE
   ```

## 📁 Project Structure

```
eduelevate_backend/
├── models/               # Database models
│   ├── User.js
│   ├── Opportunity.js
│   ├── Application.js
│   └── Resume.js
├── routes/               # API routes
│   ├── auth.js
│   ├── opportunities.js
│   ├── applications.js
│   ├── resumes.js
│   └── users.js
├── middleware/           # Custom middleware
│   └── auth.js
├── .env                  # Environment variables
├── server.js             # Main server file
├── package.json          # Dependencies
└── README.md            # This file
```

## 🗄️ Database Models

### User
- name, email, password (hashed)
- role (student/admin)
- college, course, graduationYear
- bookmarks (array of opportunity IDs)

### Opportunity
- title, type, company, description
- stream, location, stipend, duration
- deadline, requirements, eligibility
- createdBy (admin user)

### Application
- user (ref to User)
- opportunity (ref to Opportunity)
- status (Applied, Shortlisted, Interview, Selected, Rejected)
- timeline (array of status updates)
- notes, resume, coverLetter

### Resume
- user (ref to User)
- name, email, phone, location, summary
- education, experience, skills, projects, certifications
- template (professional/modern/creative)

## 🔧 Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `MONGO_URI` | MongoDB connection string | `mongodb://localhost:27017/eduelevate` |
| `JWT_SECRET` | Secret key for JWT tokens | `your_secret_key` |
| `PORT` | Server port | `5000` |
| `FRONTEND_URL` | Frontend URL for CORS | `http://localhost:3000` |

## 🐛 Troubleshooting

### MongoDB Connection Error
```
Error: connect ECONNREFUSED 127.0.0.1:27017
```
**Solution:** Make sure MongoDB is running
```bash
# Windows
net start MongoDB

# Check if MongoDB is running
mongo --version
```

### Port Already in Use
```
Error: listen EADDRINUSE: address already in use :::5000
```
**Solution:** Change PORT in `.env` file or kill the process using port 5000

### JWT Token Invalid
```
Error: Not authorized to access this route
```
**Solution:** Make sure you're sending the correct token in Authorization header

## 📚 Dependencies

- **express** - Web framework
- **mongoose** - MongoDB ODM
- **bcryptjs** - Password hashing
- **jsonwebtoken** - JWT authentication
- **cors** - Cross-origin resource sharing
- **dotenv** - Environment variables
- **express-validator** - Input validation
- **multer** - File uploads (for resume PDFs)

## 🚀 Deployment

### Deploy to Heroku
```bash
# Install Heroku CLI
heroku login
heroku create eduelevate-api
git push heroku main
```

### Deploy to Railway/Render
1. Push code to GitHub
2. Connect repository to Railway/Render
3. Add environment variables
4. Deploy!

## 📞 Support

For issues or questions:
- Create an issue on GitHub
- Email: support@eduelevate.com

---

**Made with ❤️ by EduElevate Team**
