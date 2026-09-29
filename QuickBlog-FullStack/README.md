# ✍️ QuickBlog — Full-Stack AI-Powered Blogging Platform

> A modern, full-stack blogging application built with **React 19**, **Node.js**, **Express 5**, **MongoDB**, and **Google Gemini AI** — deployed on **AWS EC2** with **Nginx** reverse proxy and **PM2** process management.

🌐 **Live Demo**: [http://13.204.75.144](http://13.204.75.144)

---

## 📸 Screenshots

| Home Page | Blog Post | Admin Dashboard |
|:---------:|:---------:|:---------------:|
| Hero section with blog listing & category filters | Full blog view with comments & social sharing | Analytics dashboard with blog & comment management |

---

## 🏗️ System Architecture

```
┌──────────────────────────────────────────────────────────┐
│                     AWS EC2 Instance                     │
│                  (Amazon Linux 2023)                     │
│                                                          │
│  ┌────────────────────────────────────────────────────┐  │
│  │              Nginx (Port 80)                       │  │
│  │  ┌──────────────────┐  ┌────────────────────────┐  │  │
│  │  │  Static Files     │  │  Reverse Proxy         │  │  │
│  │  │  /client/dist     │  │  /api/* → :3000        │  │  │
│  │  │  (React Build)    │  │  (Express Backend)     │  │  │
│  │  └──────────────────┘  └────────────────────────┘  │  │
│  └────────────────────────────────────────────────────┘  │
│                                                          │
│  ┌────────────────────────────────────────────────────┐  │
│  │          PM2 Process Manager                       │  │
│  │          └── server.js (Express 5, Port 3000)      │  │
│  └────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────┘
          │                │                │
          ▼                ▼                ▼
   ┌─────────────┐  ┌───────────┐   ┌──────────────┐
   │ MongoDB     │  │ ImageKit  │   │ Google       │
   │ Atlas       │  │ CDN       │   │ Gemini AI    │
   │ (Database)  │  │ (Images)  │   │ (Content)    │
   └─────────────┘  └───────────┘   └──────────────┘
```

---

## ✨ Features

### 🌍 Public (Reader) Features
- **Home Page** — Hero section with featured blogs, category-based filtering (Technology, Startup, Lifestyle, Finance)
- **Blog Detail Page** — Full blog view with rich HTML content, publication date, category badge, and cover image
- **Commenting System** — Readers can submit comments on blog posts (moderated by admin before public display)
- **Newsletter Subscription** — Email subscription section for user engagement
- **Social Sharing** — Share blog posts on Facebook, Twitter, and Google+
- **Responsive Design** — Fully responsive UI powered by Tailwind CSS v4

### 🔐 Admin Panel Features
- **Secure JWT Authentication** — Token-based admin login with protected routes
- **Dashboard** — Real-time analytics showing total blogs, comments, drafts, and recent blog activity
- **Create Blog with AI** — Write blogs using a rich Quill text editor with **Google Gemini AI** auto-content generation
- **Image Upload via ImageKit** — Upload blog cover images with automatic WebP conversion, quality optimization, and CDN delivery
- **Manage Blogs** — List all blogs, publish/unpublish (draft toggle), and delete blogs
- **Comment Moderation** — View all comments, approve or reject them before they appear publicly

---

## 🛠️ Tech Stack

### Frontend
| Technology | Purpose |
|:-----------|:--------|
| **React 19** | UI library for building interactive component-based interfaces |
| **Vite 6** | Next-generation frontend build tool with instant HMR (Hot Module Replacement) |
| **React Router v7** | Client-side routing and navigation for SPA |
| **Tailwind CSS v4** | Utility-first CSS framework for rapid responsive styling |
| **Quill Editor** | Rich text editor (WYSIWYG) for blog content creation |
| **Axios** | Promise-based HTTP client for API communication |
| **Motion (Framer Motion)** | Smooth animations and micro-interactions |
| **Moment.js** | Date formatting and relative timestamps |
| **React Hot Toast** | Elegant toast notifications for user feedback |

### Backend
| Technology | Purpose |
|:-----------|:--------|
| **Node.js** | JavaScript runtime for server-side execution |
| **Express 5** | Minimal, fast web framework for building REST APIs |
| **MongoDB + Mongoose** | NoSQL document database with elegant ODM (Object Data Modeling) |
| **JSON Web Token (JWT)** | Stateless authentication for securing admin API endpoints |
| **Multer** | Middleware for handling multipart/form-data (file uploads) |
| **ImageKit SDK** | Cloud-based image storage, optimization, and CDN delivery |
| **Google Gemini AI (@google/genai)** | AI-powered blog content generation using Gemini 2.0 Flash model |
| **dotenv** | Loads environment variables from `.env` file |
| **CORS** | Cross-Origin Resource Sharing middleware |

### DevOps & Deployment
| Technology | Purpose |
|:-----------|:--------|
| **AWS EC2** | Cloud virtual server (Amazon Linux 2023) hosting the full application |
| **Nginx** | High-performance web server and reverse proxy |
| **PM2** | Production process manager for Node.js with auto-restart and startup hooks |
| **MongoDB Atlas** | Managed cloud database cluster |
| **Git + GitHub** | Version control and source code hosting |

---

## 📁 Project Structure

```
QuickBlog-FullStack/
│
├── client/                          # Frontend (React + Vite)
│   ├── public/                      # Static public assets
│   ├── src/
│   │   ├── assets/                  # Images, icons, and static data
│   │   │   └── assets.js            # Asset exports, blog data, footer data
│   │   ├── components/              # Reusable UI components
│   │   │   ├── BlogCard.jsx         # Individual blog card for listing
│   │   │   ├── BlogList.jsx         # Blog grid with category filtering
│   │   │   ├── Footer.jsx           # Site footer with quick links
│   │   │   ├── Header.jsx           # Hero section with search
│   │   │   ├── Loader.jsx           # Loading spinner component
│   │   │   ├── Navbar.jsx           # Navigation bar
│   │   │   ├── Newsletter.jsx       # Email subscription section
│   │   │   └── admin/               # Admin-specific components
│   │   │       ├── BlogTableItem.jsx
│   │   │       ├── CommentTableItem.jsx
│   │   │       ├── Login.jsx         # Admin login form
│   │   │       └── Sidebar.jsx       # Admin sidebar navigation
│   │   ├── context/
│   │   │   └── AppContext.jsx        # Global state management (React Context API)
│   │   ├── pages/
│   │   │   ├── Home.jsx              # Public home page
│   │   │   ├── Blog.jsx              # Individual blog detail page
│   │   │   └── admin/                # Admin panel pages
│   │   │       ├── Layout.jsx        # Admin layout with sidebar
│   │   │       ├── Dashboard.jsx     # Admin analytics dashboard
│   │   │       ├── AddBlog.jsx       # Create new blog (with AI generation)
│   │   │       ├── ListBlog.jsx      # Manage existing blogs
│   │   │       └── Comments.jsx      # Moderate user comments
│   │   ├── App.jsx                   # Root component with route definitions
│   │   ├── main.jsx                  # React entry point
│   │   └── index.css                 # Global styles and Tailwind imports
│   ├── .env.example                  # Environment variable template
│   ├── vercel.json                   # Vercel SPA rewrite config
│   ├── vite.config.js                # Vite build configuration
│   └── package.json                  # Frontend dependencies
│
├── server/                           # Backend (Node.js + Express)
│   ├── configs/
│   │   ├── db.js                     # MongoDB connection setup
│   │   ├── gemini.js                 # Google Gemini AI SDK configuration
│   │   └── imageKit.js               # ImageKit SDK configuration
│   ├── controllers/
│   │   ├── adminController.js        # Admin login, dashboard, comment moderation
│   │   └── blogController.js         # CRUD operations, comments, AI generation
│   ├── middleware/
│   │   ├── auth.js                   # JWT authentication middleware
│   │   └── multer.js                 # File upload middleware configuration
│   ├── models/
│   │   ├── Blog.js                   # Mongoose schema for blog posts
│   │   └── Comment.js                # Mongoose schema for comments
│   ├── routes/
│   │   ├── adminRoutes.js            # Admin API endpoints
│   │   └── blogRoutes.js             # Blog & comment API endpoints
│   ├── server.js                     # Express app entry point
│   ├── .env.example                  # Environment variable template
│   ├── vercel.json                   # Vercel serverless function config
│   └── package.json                  # Backend dependencies
│
├── .gitignore                        # Git ignore rules (protects .env files)
└── README.md                         # This file
```

---

## 🔌 API Endpoints

### Public Blog Routes (`/api/blog`)
| Method | Endpoint | Description |
|:-------|:---------|:------------|
| `GET` | `/api/blog/all` | Fetch all published blogs |
| `GET` | `/api/blog/:blogId` | Fetch a single blog by ID |
| `POST` | `/api/blog/add-comment` | Submit a comment on a blog |
| `POST` | `/api/blog/comments` | Get approved comments for a blog |

### Protected Admin Routes (`/api/admin` & `/api/blog`)
| Method | Endpoint | Auth | Description |
|:-------|:---------|:-----|:------------|
| `POST` | `/api/admin/login` | ❌ | Admin login (returns JWT token) |
| `GET` | `/api/admin/dashboard` | ✅ | Get dashboard analytics |
| `GET` | `/api/admin/blogs` | ✅ | Get all blogs (including drafts) |
| `GET` | `/api/admin/comments` | ✅ | Get all comments (including unapproved) |
| `POST` | `/api/admin/approve-comment` | ✅ | Approve a comment for public display |
| `POST` | `/api/admin/delete-comment` | ✅ | Delete a comment |
| `POST` | `/api/blog/add` | ✅ | Create a new blog post (with image upload) |
| `POST` | `/api/blog/delete` | ✅ | Delete a blog post and its comments |
| `POST` | `/api/blog/toggle-publish` | ✅ | Toggle blog publish/draft status |
| `POST` | `/api/blog/generate` | ✅ | Generate blog content using Gemini AI |

---

## 🚀 Getting Started (Local Development)

### Prerequisites
- **Node.js** v18+ installed
- **MongoDB Atlas** account (free tier)
- **ImageKit** account (free tier)
- **Google Gemini API Key** (free via [Google AI Studio](https://aistudio.google.com/app/apikey))

### 1. Clone the Repository
```bash
git clone https://github.com/YOUR_USERNAME/QuickBlog-FullStack.git
cd QuickBlog-FullStack
```

### 2. Setup Backend
```bash
cd server
npm install
cp .env.example .env
# Edit .env with your actual credentials
```

### 3. Setup Frontend
```bash
cd ../client
npm install
cp .env.example .env
# Edit .env if needed (default: http://localhost:3000)
```

### 4. Run the Application
```bash
# Terminal 1 — Start Backend
cd server
npm run server

# Terminal 2 — Start Frontend
cd client
npm run dev
```

Open `http://localhost:5173` in your browser.

---

## ☁️ AWS EC2 Deployment

This application is deployed on an **AWS EC2 instance** running **Amazon Linux 2023** with the following production stack:

| Component | Role |
|:----------|:-----|
| **Nginx** | Serves the React production build and proxies `/api` requests to Express |
| **PM2** | Keeps the Node.js backend running 24/7 with automatic crash recovery |
| **SELinux** | Security-Enhanced Linux policies configured for Nginx file access |

### Deployment Commands Summary
```bash
# Install dependencies on Amazon Linux
sudo dnf update -y
sudo dnf install -y nodejs git nginx
sudo npm install -g pm2

# Clone, install, and configure
git clone <repo-url> QuickBlog-FullStack
cd QuickBlog-FullStack/server && npm install && nano .env
cd ../client && npm install && npm run build

# Start backend with PM2
cd ../server
pm2 start server.js --name quickblog-backend
pm2 save && pm2 startup

# Configure Nginx reverse proxy
sudo nano /etc/nginx/conf.d/quickblog.conf
sudo chcon -Rt httpd_sys_content_t /path/to/client/dist
sudo systemctl enable nginx && sudo systemctl restart nginx
```

---

## 🔐 Environment Variables

Create a `.env` file in both `server/` and `client/` directories. See `.env.example` files for reference.

### Server (`server/.env`)
| Variable | Description |
|:---------|:------------|
| `JWT_SECRET` | Secret key for signing JWT tokens |
| `ADMIN_EMAIL` | Admin login email |
| `ADMIN_PASSWORD` | Admin login password |
| `MONGODB_URI` | MongoDB Atlas connection string |
| `IMAGEKIT_PUBLIC_KEY` | ImageKit public API key |
| `IMAGEKIT_PRIVATE_KEY` | ImageKit private API key |
| `IMAGEKIT_URL_ENDPOINT` | ImageKit URL endpoint |
| `GEMINI_API_KEY` | Google Gemini AI API key |

### Client (`client/.env`)
| Variable | Description |
|:---------|:------------|
| `VITE_BASE_URL` | Backend API base URL (e.g., `http://localhost:3000`) |

---

## 🧠 AI Integration

QuickBlog integrates **Google Gemini 2.0 Flash** for intelligent blog content generation:

1. Admin navigates to **Add Blog** page
2. Enters a topic/prompt (e.g., *"Benefits of cloud computing"*)
3. Clicks **Generate** — the backend sends the prompt to Gemini AI via `@google/genai` SDK
4. AI-generated content is returned and loaded into the Quill rich text editor
5. Admin can edit, enhance, and publish the generated content

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">
  Built with ❤️ using React, Node.js, MongoDB & Google Gemini AI
</p>
