# Civic Connect

A platform for reporting and tracking civic issues in your community using OpenStreetMap and Leaflet.js.

## 🚀 Setup Instructions

1. **Environment Variables Needed:**
   \`\`\`
   NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
   \`\`\`

2. **Supabase Setup:**
   - Run the SQL scripts in order (001, 002, 003)
   - Enable Google OAuth in Authentication settings
   - Create an "images" storage bucket for issue photos

3. **No API Keys Required:**
   - Uses OpenStreetMap tiles (completely free)
   - No Mapbox token needed
   - No additional map service setup required

## 🗺️ **Features**

- **Interactive Map**: OpenStreetMap with Leaflet.js
- **Issue Reporting**: Photo upload, location selection, categorization
- **Gamification**: Coin rewards and leaderboards
- **Community Moderation**: Flagging system
- **Responsive Design**: Mobile-first approach
- **Dark/Light Theme**: Theme toggle support

## 🛠️ **Tech Stack**

- **Frontend**: Next.js 14, React, TypeScript
- **Styling**: Tailwind CSS, shadcn/ui
- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth (Google OAuth + Email)
- **Maps**: Leaflet.js with OpenStreetMap
- **Storage**: Supabase Storage

The platform is completely free to run with no API key requirements for mapping functionality!
