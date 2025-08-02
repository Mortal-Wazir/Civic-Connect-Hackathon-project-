# Civic Connect Setup Guide

## 🚀 Quick Setup Instructions

Your Supabase project is configured! Follow these steps to complete the setup:

### 1. Database Setup

Go to your Supabase project dashboard:
**https://supabase.com/dashboard/project/rdnmkvmgdbakulwopvuj**

#### Run SQL Scripts (in order):

1. **SQL Editor** → **New Query** → Copy and run `scripts/001_create_tables.sql`
2. **New Query** → Copy and run `scripts/002_seed_categories.sql`  
3. **New Query** → Copy and run `scripts/003_create_functions.sql`
4. **New Query** → Copy and run `scripts/005_fix_storage_policies.sql` (creates bucket + fixes image upload)

### 2. That's It!

The storage bucket will be created automatically by script 005. No manual bucket creation needed!

### 3. Environment Variables

Your `.env.local` file is already configured with:
\`\`\`
NEXT_PUBLIC_SUPABASE_URL=https://rdnmkvmgdbakulwopvuj.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
\`\`\`

### 4. Test the Application

1. Run `npm run dev`
2. Open http://localhost:3000
3. Allow location access
4. Sign up/Sign in
5. Try reporting an issue with a photo (up to 50MB)

## 🎯 Features Available

- ✅ **Interactive Map** with OpenStreetMap (no API key needed)
- ✅ **Issue Reporting** with photo upload (50MB limit)
- ✅ **User Authentication** (Email + Password)
- ✅ **Gamification** (coins and leaderboard)
- ✅ **Community Moderation** (flagging system)
- ✅ **Responsive Design** (mobile-first)
- ✅ **Dark/Light Theme** toggle

## 🔧 Troubleshooting

**If Script 005 Fails with Permission Error:**
- This is normal for some Supabase accounts
- Just create the "images" bucket manually:
  1. Go to **Storage** → **Create Bucket**
  2. Name: `images`
  3. Public: ✅ ON
  4. File size limit: `52428800` (50MB)
  5. Create

**Database Status Component**: The app will show a setup status indicator until all scripts are run successfully.

**Location Issues**: The app defaults to NYC if location access is denied.

## 📱 Ready to Use!

Once setup is complete, your Civic Connect platform will be fully functional with:
- Real-time issue reporting with 50MB image uploads
- Interactive mapping with OpenStreetMap
- User gamification and community features
- Mobile-responsive design with camera support

No additional API keys required!
