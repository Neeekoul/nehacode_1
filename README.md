# nehacode_1
this is project realated to:-
Build a React Native app that depends entirely on a Flask backend.
 The mobile app must act as a thin client — no business logic inside.🧱 System Architecture (Non-Negotiable)
React Native App  →  Flask API  →  MongoDB
                         ↓
                    YouTube (hidden behind backend logic)

📌 The app should never directly use YouTube links.

📱 Mobile App (React Native)
Rule:
❗ The app must NOT contain business logic, filtering logic, or hardcoded content.
It should only:
Call APIs
Store JWT
Render data
Send user actions

1️⃣ Authentication Screens
Signup
Name
Email
Password
Login
Email
Password
On success:
Store JWT securely
Navigate to Dashboard

2️⃣ Dashboard (Home Screen)
Show 2 video tiles fetched from backend.
Each tile shows:
Thumbnail
Title
Short description
Clicking a tile opens:
🎬 Video Player Screen
Plays the video
Controls:
Play / Pause
Seek bar
Mute / Unmute
⚠️ BUT:
 The app must not expose YouTube URLs.
 They must implement a video wrapper strategy (details below).

3️⃣ Settings Screen
Show user name + email
Logout button (clears JWT)

🧠 Backend (Flask + MongoDB)
This is where most evaluation happens.

🔐 Auth Requirements
Use JWT authentication
Endpoints
Method
Endpoint
Purpose
POST
/auth/signup
Register user
POST
/auth/login
Login
GET
/auth/me
Return user profile
POST
/auth/logout
(Invalidate token OR mock logic)

Passwords must be hashed.

🎥 Video System (Important)
Backend stores video records like:
{
  "title": "How Startups Fail",
  "description": "Lessons from real founders",
  "youtube_id": "abc123xyz",
  "thumbnail_url": "...",
  "is_active": true
}


API:
Method
Endpoint
Purpose
GET
/dashboard
Returns 2 videos only
GET
/video/<id>/stream
Returns playable stream URL or proxy


🔥 The Twist (Important)
They cannot send raw YouTube URLs like:
https://youtube.com/watch?v=abc123
They must implement one of these approaches:
Option A (Simpler):
 Backend sends an embed-safe URL or masked format.
Option B (Better):
 Backend returns:
{
  "video_id": "...",
  "playback_token": "signed_token"
}

And app requests /video/<id>/stream?token=...
This tests:
API design
Security thinking
Abstraction skills

🗃 Database Models
User
id
name
email
password_hash
created_at

Video
id
title
description
youtube_id
thumbnail_url
is_active


🧪 What You’re Testing (Secretly)
Skill
How this exposes it
API-first thinking
App is useless without backend
Auth knowledge
JWT flow
Architecture maturity
Separation of concerns
Mobile/backend integration
RN + Flask
Security awareness
Hiding YouTube source
Data modeling
User + video
Clean engineering
No logic in frontend
Ownership
Does it fully work?


⭐ Bonus (Top 10% Candidates)
Refresh tokens
Token expiry handling
Rate limiting login
Basic logging
Deployment link
Pagination-ready dashboard
Video watch tracking endpoint
