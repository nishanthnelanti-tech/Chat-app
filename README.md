# Chat App

A full-stack real-time chat application built with Node.js and React. Users can create accounts, authenticate securely, search for contacts, and send messages instantly with real-time synchronization using WebSockets. The app features user profiles, profile picture uploads to Cloudinary, theme customization, and online status indicators.

## Stack

- **Language(s):** JavaScript (Node.js backend, React frontend)
- **Framework / runtime:** Express.js, React 18 with Vite
- **Notable libraries:** 
  - **Backend:** Socket.io (real-time messaging), Mongoose (MongoDB ORM), bcryptjs (password hashing), jsonwebtoken (authentication)
  - **Frontend:** Zustand (state management), React Router, Tailwind CSS + DaisyUI (styling), Axios (HTTP client)

## Project Structure

```
Chat-app/
├── backend/                    # Node.js Express server
│   ├── src/
│   │   ├── controllers/        # Request handlers (auth, messages)
│   │   ├── models/             # MongoDB schemas (User, Message)
│   │   ├── routes/             # API endpoints (/api/auth, /api/messages)
│   │   ├── middleware/         # Auth verification, JWT validation
│   │   ├── lib/                # Database, Socket.io, Cloudinary, utilities
│   │   └── index.js            # Server entry point with middleware setup
│   └── package.json
│
├── frontend/                   # React + Vite application
│   ├── src/
│   │   ├── pages/              # Route pages (HomePage, LoginPage, SignUpPage, ProfilePage, SettingsPage)
│   │   ├── components/         # Reusable UI (Navbar, ChatContainer, Sidebar, MessageInput, ChatHeader)
│   │   ├── store/              # Zustand stores (useAuthStore, useChatStore, useThemeStore)
│   │   ├── constants/          # App constants and configuration
│   │   ├── lib/                # Frontend utilities
│   │   ├── App.jsx             # Router and main layout
│   │   └── main.jsx            # React entry point
│   └── package.json
│
└── package.json                # Root package.json with build scripts
```

## How It Works

On startup, the server connects to MongoDB and initializes Socket.io for real-time messaging. The frontend (React + Vite) authenticates users via JWT stored in cookies. When authenticated, users access the HomePage where they can:

1. **View Contacts** - Sidebar displays all users (fetched via REST API)
2. **Select & Chat** - Click on a contact to view message history in ChatContainer
3. **Send Messages** - Type and send messages via MessageInput component
4. **Real-time Sync** - Socket.io listeners instantly sync new messages across connected clients
5. **Manage Profile** - Upload profile pictures, customize theme, view settings

Zustand stores manage:
- **useAuthStore** - Logged-in user, authentication state
- **useChatStore** - Selected contact, messages, chat list
- **useThemeStore** - Theme preference (light/dark)

## Getting Started

### Prerequisites

- Node.js (v14 or higher)
- MongoDB database
- Cloudinary account (for image uploads)

### Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the `backend/` directory:
   ```env
   PORT=5000
   MONGODB_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<database>
   JWT_SECRET=your_jwt_secret_key_here
   CLOUDINARY_NAME=your_cloudinary_name
   CLOUDINARY_API_KEY=your_cloudinary_api_key
   CLOUDINARY_API_SECRET=your_cloudinary_api_secret
   NODE_ENV=development
   ```

4. Start the development server:
   ```bash
   npm run dev
   ```
   The backend will run on `http://localhost:5000`

### Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm run dev
   ```
   The frontend will run on `http://localhost:5173`

### Running Both Together

From the root directory:

1. Build and install all dependencies:
   ```bash
   npm run build
   ```

2. Start the backend server (which will serve the built frontend in production):
   ```bash
   npm start
   ```

## Available Scripts

### Backend

- `npm run dev` - Start development server with nodemon (auto-reload)
- `npm start` - Start production server

### Frontend

- `npm run dev` - Start Vite development server with HMR
- `npm run build` - Build for production
- `npm run preview` - Preview production build locally
- `npm run lint` - Run ESLint to check code quality

## Features

✅ User Authentication
- Secure signup and login with bcryptjs password hashing
- JWT-based authentication with cookie storage
- Protected routes and API endpoints

✅ Real-time Messaging
- Instant message delivery using Socket.io
- Online/offline status indicators
- Message history persistence with MongoDB

✅ User Profiles
- Profile picture upload to Cloudinary
- View and edit user profile information
- Online status tracking

✅ Search & Contacts
- Search for users by username
- Maintain contact list
- See online status of contacts

✅ Theme Customization
- Light/Dark theme support with DaisyUI
- Theme preference persistence

✅ Modern UI
- Responsive design with Tailwind CSS
- Skeleton loading states
- Toast notifications for user feedback
- Icon library (lucide-react)

## API Endpoints

### Authentication Routes (`/api/auth`)
- `POST /signup` - Register a new user
- `POST /login` - Login with credentials
- `POST /logout` - Logout and clear session
- `GET /check-auth` - Verify current authentication status
- `PUT /update-profile` - Update user profile

### Message Routes (`/api/messages`)
- `GET /users` - Get all users for contacts list
- `GET /:id` - Get message history with a specific user
- `POST /send/:id` - Send a message to a user

## Socket.io Events

### Client → Server
- `connect` - User connects to chat
- `disconnect` - User disconnects from chat
- `send_message` - Send a new message

### Server → Client
- `receive_message` - Receive a new message
- `user_online` - User comes online
- `user_offline` - User goes offline
- `get_online_users` - Get list of currently online users

## Technologies Used

### Backend
- **Express.js** - Web framework
- **Mongoose** - MongoDB object modeling
- **Socket.io** - Real-time bidirectional communication
- **bcryptjs** - Password hashing
- **jsonwebtoken** - JWT authentication
- **cookie-parser** - Cookie middleware
- **cors** - Cross-Origin Resource Sharing
- **Cloudinary** - Image hosting service
- **dotenv** - Environment variable management

### Frontend
- **React 18** - UI library
- **Vite** - Build tool and dev server
- **React Router DOM** - Client-side routing
- **Zustand** - State management
- **Axios** - HTTP client
- **Socket.io Client** - Real-time communication
- **Tailwind CSS** - Utility-first CSS framework
- **DaisyUI** - Tailwind CSS component library
- **Lucide React** - Icon library
- **React Hot Toast** - Toast notifications
- **ESLint** - Code linting

## Project Pages

- **HomePage** - Main chat interface with sidebar and chat container
- **LoginPage** - User login form
- **SignUpPage** - User registration form
- **ProfilePage** - View and edit user profile
- **SettingsPage** - App settings and preferences

## Components

### Navigation & Layout
- **Navbar** - Top navigation bar
- **Sidebar** - Contact list and user selection

### Chat Interface
- **ChatContainer** - Display messages and chat area
- **ChatHeader** - Show selected contact info
- **MessageInput** - Input form for sending messages
- **NoChatSelected** - Placeholder when no chat is selected

### UI Elements
- **AuthImagePattern** - Background pattern for auth pages
- **Skeleton Loading States** - Loading placeholders

## Future Enhancements

- Group chat support
- Message encryption
- File sharing
- Voice/Video calling
- Message search and filtering
- Message reactions and emojis
- User typing indicators
- Message read receipts

## Contributing

Feel free to fork this project and submit pull requests with improvements!

## License

This project is licensed under the ISC License - see the LICENSE file for details.

## Support

For issues, bugs, or feature requests, please create an issue in the repository.

---

**Happy Chatting!** 💬
