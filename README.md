📌 Smart Bookmark App

A full-stack real-time bookmark management application built using Next.js (App Router) and Supabase.

The app allows authenticated users to securely manage personal bookmarks with instant cross-tab synchronization.

🚀 Live Demo

👉 View Live App

(Replace with your actual Vercel URL)

🧩 Project Overview

Smart Bookmark App enables users to:

🔐 Authenticate using Google OAuth

➕ Create personal bookmarks

❌ Delete bookmarks

🔒 Access private data secured with Row Level Security (RLS)

⚡ Experience real-time updates across multiple browser sessions

📱 Use a responsive UI built with Tailwind CSS

This project demonstrates modern full-stack development using a serverless architecture.

🏗️ Architecture
Layer	Technology
Frontend	Next.js (App Router)
Backend	Supabase (PostgreSQL + Auth + Realtime)
Authentication	Google OAuth via Supabase
Database Security	Row Level Security (RLS)
Deployment	Vercel
🔐 Authentication Flow

User signs in with Google OAuth

Supabase handles authentication and session management

User ID from Supabase Auth is linked to bookmark records

Row Level Security ensures users can only access their own records

🗄️ Database Design
Table: bookmarks
create table bookmarks (
  id uuid primary key default uuid_generate_v4(),
  user_id uuid references auth.users(id) on delete cascade,
  title text not null,
  url text not null,
  created_at timestamp default now()
);

🔒 Row Level Security
alter table bookmarks enable row level security;

create policy "Users can access their own bookmarks"
on bookmarks
for all
using (auth.uid() = user_id)
with check (auth.uid() = user_id);

⚡ Real-Time Implementation

Supabase Realtime subscriptions listen for:

INSERT

DELETE

UPDATE

Whenever a change occurs, the UI automatically refreshes the bookmark list — enabling real-time synchronization across multiple browser tabs.

📦 Local Setup
1️⃣ Clone the repository
git clone https://github.com/YOUR_USERNAME/smart-bookmark-app.git

2️⃣ Navigate into the project
cd smart-bookmark-app

3️⃣ Install dependencies
npm install

4️⃣ Start development server
npm run dev


Visit:

http://localhost:3000

🔐 Environment Variables

Create a .env.local file and add:

NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key

🛠️ Key Technical Highlights

✅ Implemented secure multi-user architecture using RLS

✅ Integrated third-party OAuth authentication

✅ Built full CRUD functionality with Supabase

✅ Implemented real-time data subscriptions

✅ Deployed full-stack app using serverless infrastructure

✅ Structured using modern Next.js App Router

🧠 Challenges & Solutions
Challenge	Solution
OAuth redirect errors	Configured correct callback URL in Google Cloud
Insert blocked by RLS	Added with check (auth.uid() = user_id)
Realtime not triggering	Enabled replication for bookmarks table
Session not persisting	Used onAuthStateChange listener
📌 Future Improvements

✏️ Edit bookmark functionality

🔍 Search & filter bookmarks

🏷️ Add tags/categories

🌙 Dark mode support

👨‍💻 Author

Raghu Naga Rohit Kampati
Aspiring Software Engineer
GitHub
