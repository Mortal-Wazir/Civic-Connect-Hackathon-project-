# Simple Setup Guide - Just 2 Steps!

## 🚀 **Super Simple Setup**

### **Step 1: Create Storage Bucket**
1. Go to: https://supabase.com/dashboard/project/rdnmkvmgdbakulwopvuj
2. Click **Storage** → **Create Bucket**
3. Name: `images`
4. Make it **Public** ✅
5. Click **Create**

### **Step 2: Run Database Scripts**
1. Go to **SQL Editor**
2. Run these 3 scripts in order:
   - `001_create_tables.sql`
   - `002_seed_categories.sql` 
   - `003_create_functions.sql`

## ✅ **That's It!**

Your app will now:
- ✅ **Accept any image file** (JPEG, PNG, GIF, WebP)
- ✅ **Upload up to 10MB** images
- ✅ **Work without complex setup**
- ✅ **Continue even if upload fails**
- ✅ **Show simple error messages**

## 🎯 **No Complex Configuration Needed**

- ❌ **No NPM tokens**
- ❌ **No complex policies** 
- ❌ **No special permissions**
- ❌ **No environment variable complexity**

Just create the bucket, run the scripts, and it works!

## 🔧 **If Upload Doesn't Work**

1. **Check bucket exists**: Go to Storage and verify "images" bucket is there
2. **Check bucket is public**: Make sure the public toggle is ON
3. **Try again**: The app will work even if some uploads fail

The app is designed to be **simple and forgiving** - it will work even if image upload has issues!
