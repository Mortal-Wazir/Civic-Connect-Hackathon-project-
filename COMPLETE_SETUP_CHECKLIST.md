# Complete Setup Checklist

## 🎯 **Current Status Check**

The app is showing "Setup Required" because it's checking for:
- ✅ **Database tables** (profiles, categories, issues)
- ✅ **Categories seeded** (pothole, garbage, etc.)
- ✅ **Storage bucket** (images bucket)

## 🚀 **Complete Setup Steps**

### **Step 1: Database Tables**
Go to: https://supabase.com/dashboard/project/rdnmkvmgdbakulwopvuj

**SQL Editor** → **New Query** → Copy and paste each script:

#### **Script 1: Create Tables**
\`\`\`sql
-- Create tables for Civic Connect platform

-- Users table (extends Supabase auth.users)
CREATE TABLE IF NOT EXISTS public.profiles (
  id UUID REFERENCES auth.users(id) PRIMARY KEY,
  email TEXT,
  full_name TEXT,
  avatar_url TEXT,
  coins INTEGER DEFAULT 0,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Issue categories
CREATE TABLE IF NOT EXISTS public.categories (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  icon TEXT NOT NULL,
  color TEXT NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Civic issues/reports
CREATE TABLE IF NOT EXISTS public.issues (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id UUID REFERENCES public.profiles(id) NOT NULL,
  title TEXT NOT NULL,
  description TEXT NOT NULL,
  category_id INTEGER REFERENCES public.categories(id) NOT NULL,
  latitude DECIMAL(10, 8) NOT NULL,
  longitude DECIMAL(11, 8) NOT NULL,
  address TEXT,
  image_url TEXT,
  status TEXT DEFAULT 'open' CHECK (status IN ('open', 'in_progress', 'resolved', 'closed')),
  upvotes INTEGER DEFAULT 0,
  flag_count INTEGER DEFAULT 0,
  is_hidden BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Issue flags for spam protection
CREATE TABLE IF NOT EXISTS public.issue_flags (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  issue_id UUID REFERENCES public.issues(id) NOT NULL,
  user_id UUID REFERENCES public.profiles(id) NOT NULL,
  reason TEXT NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  UNIQUE(issue_id, user_id)
);

-- Issue upvotes
CREATE TABLE IF NOT EXISTS public.issue_upvotes (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  issue_id UUID REFERENCES public.issues(id) NOT NULL,
  user_id UUID REFERENCES public.profiles(id) NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  UNIQUE(issue_id, user_id)
);

-- Enable Row Level Security
ALTER TABLE public.profiles ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.categories ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.issues ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.issue_flags ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.issue_upvotes ENABLE ROW LEVEL SECURITY;

-- RLS Policies
CREATE POLICY "Public profiles are viewable by everyone" ON public.profiles FOR SELECT USING (true);
CREATE POLICY "Users can update own profile" ON public.profiles FOR UPDATE USING (auth.uid() = id);

CREATE POLICY "Categories are viewable by everyone" ON public.categories FOR SELECT USING (true);

CREATE POLICY "Issues are viewable by everyone" ON public.issues FOR SELECT USING (NOT is_hidden);
CREATE POLICY "Users can insert own issues" ON public.issues FOR INSERT WITH CHECK (auth.uid() = user_id);
CREATE POLICY "Users can update own issues" ON public.issues FOR UPDATE USING (auth.uid() = user_id);

CREATE POLICY "Users can flag issues" ON public.issue_flags FOR INSERT WITH CHECK (auth.uid() = user_id);
CREATE POLICY "Users can view flags" ON public.issue_flags FOR SELECT USING (true);

CREATE POLICY "Users can upvote issues" ON public.issue_upvotes FOR INSERT WITH CHECK (auth.uid() = user_id);
CREATE POLICY "Users can view upvotes" ON public.issue_upvotes FOR SELECT USING (true);
CREATE POLICY "Users can remove own upvotes" ON public.issue_upvotes FOR DELETE USING (auth.uid() = user_id);
\`\`\`

#### **Script 2: Seed Categories**
\`\`\`sql
-- Insert default categories
INSERT INTO public.categories (name, icon, color) VALUES
  ('Pothole', '🕳️', '#ef4444'),
  ('Garbage', '🗑️', '#f97316'),
  ('Street Light', '💡', '#eab308'),
  ('Traffic Signal', '🚦', '#22c55e'),
  ('Water Issue', '💧', '#3b82f6'),
  ('Graffiti', '🎨', '#8b5cf6'),
  ('Broken Sidewalk', '🚶', '#6b7280'),
  ('Other', '❓', '#64748b')
ON CONFLICT DO NOTHING;
\`\`\`

#### **Script 3: Create Functions**
\`\`\`sql
-- Function to handle new user signup
CREATE OR REPLACE FUNCTION public.handle_new_user()
RETURNS TRIGGER AS $$
BEGIN
  INSERT INTO public.profiles (id, email, full_name, avatar_url)
  VALUES (
    NEW.id,
    NEW.email,
    NEW.raw_user_meta_data->>'full_name',
    NEW.raw_user_meta_data->>'avatar_url'
  );
  RETURN NEW;
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Trigger for new user signup
DROP TRIGGER IF EXISTS on_auth_user_created ON auth.users;
CREATE TRIGGER on_auth_user_created
  AFTER INSERT ON auth.users
  FOR EACH ROW EXECUTE FUNCTION public.handle_new_user();

-- Function to award coins for new issues
CREATE OR REPLACE FUNCTION public.award_coins_for_issue()
RETURNS TRIGGER AS $$
BEGIN
  UPDATE public.profiles
  SET coins = coins + 10
  WHERE id = NEW.user_id;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Trigger to award coins when issue is created
DROP TRIGGER IF EXISTS on_issue_created ON public.issues;
CREATE TRIGGER on_issue_created
  AFTER INSERT ON public.issues
  FOR EACH ROW EXECUTE FUNCTION public.award_coins_for_issue();

-- Function to hide issues with multiple flags
CREATE OR REPLACE FUNCTION public.check_issue_flags()
RETURNS TRIGGER AS $$
BEGIN
  UPDATE public.issues
  SET is_hidden = TRUE
  WHERE id = NEW.issue_id
  AND (SELECT COUNT(*) FROM public.issue_flags WHERE issue_id = NEW.issue_id) >= 3;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Trigger to check flags
DROP TRIGGER IF EXISTS on_issue_flagged ON public.issue_flags;
CREATE TRIGGER on_issue_flagged
  AFTER INSERT ON public.issue_flags
  FOR EACH ROW EXECUTE FUNCTION public.check_issue_flags();
\`\`\`

### **Step 2: Create Storage Bucket**
1. **Go to Storage** section in Supabase
2. **Click "Create Bucket"**
3. **Name**: `images`
4. **Public**: ✅ **Turn ON**
5. **Click "Create"**

### **Step 3: Refresh App**
After completing both steps, refresh your app and the setup message should disappear!

## ✅ **Verification**

### **Check Database:**
- Go to **Table Editor** in Supabase
- You should see: `profiles`, `categories`, `issues` tables
- Categories table should have 8 rows (pothole, garbage, etc.)

### **Check Storage:**
- Go to **Storage** in Supabase  
- You should see `images` bucket with "Public" badge

### **Check App:**
- Refresh your Civic Connect app
- Setup message should be gone
- You should see the map and be able to report issues

## 🎉 **After Setup Complete**

Your app will have:
- ✅ **Full functionality** - reporting, viewing, authentication
- ✅ **Image uploads** working
- ✅ **User profiles** and gamification
- ✅ **Mobile responsive** design
- ✅ **Dark/light theme** support

**Run the 3 scripts in order, create the storage bucket, and you're done!**
