# SkillTracker - Full-Stack Next.js Skill Tracking App

A modern, full-stack web application for tracking skills and maintaining consistent practice routines. Built with Next.js 14, Supabase, and Tailwind CSS.

## Features

- **Email/Password Authentication**: Secure user authentication with Supabase Auth
- **Skill Management**: Add, edit, delete, and track multiple skills
- **Smart Status System**: Automatically calculates skill status (Fresh/Stale/Decayed) based on practice history
- **Responsive Design**: Fully responsive mobile-first design that works on all devices
- **Real-time Updates**: Instant updates when practicing skills or making changes
- **Protected Routes**: Secure dashboard accessible only to authenticated users
- **Modern UI**: Clean, professional interface using Tailwind CSS and shadcn/ui components

## Tech Stack

- **Frontend**: Next.js 14 (App Router), React, TypeScript
- **Styling**: Tailwind CSS, shadcn/ui components
- **Backend**: Supabase (PostgreSQL database, Authentication, RLS)
- **Deployment**: Ready for Vercel deployment

## Database Schema

### Skills Table
- `id` - UUID primary key
- `user_id` - Foreign key to auth.users
- `skill_name` - Name of the skill
- `category` - Skill category
- `last_practiced` - Last practice timestamp
- `threshold` - Days until skill becomes stale
- `created_at` - Creation timestamp
- `updated_at` - Last update timestamp

### Status Calculation
- **Fresh**: Last practiced within threshold days
- **Stale**: Last practiced between threshold and 2x threshold days
- **Decayed**: Last practiced more than 2x threshold days ago

## Setup Instructions

### 1. Prerequisites

- Node.js 18+ installed
- A Supabase account (free tier works fine)

### 2. Clone and Install

```bash
# Clone the repository
git clone <your-repo-url>
cd skilltracker

# Install dependencies
npm install
```

### 3. Supabase Setup

1. Create a new project at [supabase.com](https://supabase.com)
2. The database schema has already been set up via migrations
3. Get your project credentials:
   - Go to Project Settings > API
   - Copy the Project URL
   - Copy the anon/public key

### 4. Environment Variables

Create a `.env.local` file in the root directory:

```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

Replace the placeholder values with your actual Supabase credentials.

### 5. Run Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Deployment to Vercel

### 1. Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <your-github-repo-url>
git push -u origin main
```

### 2. Deploy to Vercel

1. Go to [vercel.com](https://vercel.com) and sign in
2. Click "New Project"
3. Import your GitHub repository
4. Add environment variables:
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
5. Click "Deploy"

Your app will be live in minutes!

## Project Structure

```
├── app/
│   ├── dashboard/          # Protected dashboard page
│   ├── login/              # Login page
│   ├── signup/             # Signup page
│   ├── layout.tsx          # Root layout with AuthProvider
│   └── page.tsx            # Landing page
├── components/
│   ├── ui/                 # shadcn/ui components
│   ├── AddSkillForm.tsx    # Form to add new skills
│   ├── Navbar.tsx          # Responsive navigation bar
│   └── SkillsTable.tsx     # Skills table with CRUD operations
├── contexts/
│   └── AuthContext.tsx     # Authentication context provider
├── lib/
│   ├── auth.ts             # Authentication functions
│   ├── supabase.ts         # Supabase client configuration
│   └── status-calculator.ts # Skill status calculation logic
└── .env.local              # Environment variables (create this)
```

## Usage

### Creating an Account
1. Click "Get Started" on the landing page
2. Fill in your name, email, and password
3. You'll be automatically logged in and redirected to the dashboard

### Adding Skills
1. On the dashboard, use the "Add New Skill" form
2. Enter the skill name, category, and practice threshold (in days)
3. Click "Add Skill"

### Managing Skills
- **Update Practice**: Click the refresh icon to mark a skill as practiced today
- **Edit**: Click the edit icon to modify skill details
- **Delete**: Click the trash icon to remove a skill

### Understanding Status
- **Fresh** (Green): You've practiced within your threshold
- **Stale** (Yellow): It's been longer than your threshold but less than 2x
- **Decayed** (Red): It's been more than 2x your threshold - time to practice!

## Security Features

- Row Level Security (RLS) enabled on all database tables
- Users can only access their own data
- Secure password hashing via Supabase Auth
- Protected routes redirect to login if not authenticated
- CSRF protection and secure session handling

## Development

### Type Checking
```bash
npm run typecheck
```

### Build for Production
```bash
npm run build
```

### Lint
```bash
npm run lint
```

## Support

For issues or questions, please open an issue on GitHub.

## License

MIT License - feel free to use this project for personal or commercial purposes.
