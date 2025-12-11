# Doctor Appointment System

A full-stack web application for managing doctor appointments with separate interfaces for users, doctors, and administrators. Built with Node.js, Express, MongoDB, and React.

## Features

### User Features
- User registration and authentication
- Browse available doctors
- Book appointments with doctors
- View appointment history
- Check appointment availability
- Receive notifications
- Apply to become a doctor

### Doctor Features
- Doctor profile management
- View appointment requests
- Update appointment status (pending/approved/rejected)
- Manage working hours and availability
- View appointment history

### Admin Features
- View all users and doctors
- Approve/reject doctor applications
- Manage user accounts
- Monitor system activity

## Technology Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM for MongoDB
- **JWT** - Authentication
- **bcryptjs** - Password hashing
- **dotenv** - Environment variables

### Frontend
- **React** - UI library
- Pre-built production build included

## Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (v14 or higher)
- npm or yarn
- MongoDB (local installation or MongoDB Atlas account)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd Production-Doctor-Appointment-system-main
```

2. Install backend dependencies:
```bash
npm install
```

3. Create a `.env` file in the root directory:
```env
PORT=8080
NODE_MODE=development
MONGO_URL=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key
```

4. Update the MongoDB connection string in `.env`:
   - For local MongoDB: `mongodb://localhost:27017/doctor-appointment`
   - For MongoDB Atlas: Use your cluster connection string

5. If you need to rebuild the frontend (optional):
```bash
cd client
npm install
npm run build
cd ..
```

## Running the Application

### Production Mode
The application is configured to serve the pre-built React app. Simply run:
```bash
npm start
```

The server will start on `http://localhost:8080` (or the port specified in your `.env` file).

### Development Mode
To run both backend and frontend concurrently in development mode:
```bash
npm run dev
```

This will start:
- Backend server on the configured port
- React development server (if client directory has source files)

### Individual Commands
- Start server only: `npm start`
- Start client only: `npm run client` (requires client source files)
- Start server with nodemon: `npm run server` (note: there's a typo in package.json - "serevr.js")

## Project Structure

```
Production-Doctor-Appointment-system-main/
├── client/
│   └── build/              # Pre-built React application
├── config/
│   └── db.js              # MongoDB connection configuration
├── controllers/
│   ├── adminCtrl.js       # Admin-related controllers
│   ├── doctorCtrl.js      # Doctor-related controllers
│   └── userCtrl.js        # User-related controllers
├── middlewares/
│   └── authMiddleware.js  # JWT authentication middleware
├── models/
│   ├── appointmentModel.js # Appointment schema
│   ├── doctorModel.js      # Doctor schema
│   └── userModels.js       # User schema
├── routes/
│   ├── adminRoutes.js     # Admin API routes
│   ├── doctorRoutes.js    # Doctor API routes
│   └── userRoutes.js      # User API routes
├── server.js              # Main server file
├── package.json           # Dependencies and scripts
└── .env                   # Environment variables (create this)
```

## API Endpoints

### User Routes (`/api/v1/user`)
- `POST /register` - Register a new user
- `POST /login` - User login
- `POST /getUserData` - Get authenticated user data
- `POST /apply-doctor` - Apply to become a doctor
- `POST /get-all-notification` - Get user notifications
- `POST /delete-all-notification` - Clear notifications
- `GET /getAllDoctors` - Get list of all doctors
- `POST /book-appointment` - Book an appointment
- `POST /booking-availability` - Check appointment availability
- `GET /user-appointments` - Get user's appointments

### Doctor Routes (`/api/v1/doctor`)
- `POST /getDoctorInfo` - Get doctor information
- `POST /updateProfile` - Update doctor profile
- `POST /getDoctorById` - Get doctor by ID
- `GET /doctor-appointments` - Get doctor's appointments
- `POST /update-status` - Update appointment status

### Admin Routes (`/api/v1/admin`)
- `GET /getAllUsers` - Get all users
- `GET /getAllDoctors` - Get all doctors (including pending)
- `POST /changeAccountStatus` - Approve/reject doctor applications

**Note:** Most endpoints require JWT authentication via the `authMiddleware`.

## Database Models

### User Model
- name, email, password
- isAdmin, isDoctor (boolean flags)
- notification, seennotification arrays

### Doctor Model
- userId, firstName, lastName, phone, email
- website, address, specialization
- experience, feesPerCunsaltation
- status (pending/approved/rejected)
- timings (working hours)

### Appointment Model
- userId, doctorId
- doctorInfo, userInfo
- date, time, status
- timestamps

## Environment Variables

Create a `.env` file with the following variables:

```env
PORT=8080
NODE_MODE=development
MONGO_URL=mongodb://localhost:27017/doctor-appointment
JWT_SECRET=your_secret_key_here
```

## Security Features

- Password hashing with bcryptjs
- JWT-based authentication
- Protected routes with middleware
- Environment variable configuration

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

This project is licensed under the MIT License.

## Author

techinfyt

## Notes

- The React frontend is pre-built in the `client/build` directory
- To modify the frontend, you'll need the React source files
- Ensure MongoDB is running before starting the server
- Default server port is 8080 (configurable via `.env`)

## Troubleshooting

- **MongoDB connection error**: Ensure MongoDB is running and the connection string in `.env` is correct
- **Port already in use**: Change the PORT in `.env` or stop the process using that port
- **JWT errors**: Ensure JWT_SECRET is set in `.env`
- **Build errors**: If modifying frontend, ensure all dependencies are installed in the client directory

