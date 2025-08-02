# Storage Issue Diagnosis & Fix

## 🚨 **Issues Found**

### **1. Environment Variable Error:**
- ❌ `NPM_RC cannot be accessed on the client`
- ❌ `NPM_TOKEN cannot be accessed on the client`
- ✅ **Fixed**: Removed these from .env.local

### **2. Storage Bucket Issue:**
- ❌ `buckets: Array(0)` - No buckets found by the app
- ❌ `Images bucket found: undefined`
- ❌ SQL shows bucket exists, but app can't see it

## 🎯 **Root Cause**

The **script 005 created the bucket in the database** but there's a **permission/visibility issue** preventing the app from seeing it.

## ✅ **Solution: Manual Bucket Creation**

Since the app can't see the bucket created by SQL, let's create it manually:

### **Step 1: Delete Existing Bucket (if any)**
1. Go to: https://supabase.com/dashboard/project/rdnmkvmgdbakulwopvuj
2. Click **Storage**
3. If you see any buckets, delete them

### **Step 2: Create New Bucket**
1. Click **"Create Bucket"**
2. **Settings**:
   - **Name**: `images`
   - **Public**: ✅ **Turn ON**
   - **File size limit**: `52428800` (50MB)
   - **Allowed MIME types**: Leave empty
3. Click **"Create"**

### **Step 3: Test**
1. **Restart your dev server**: `npm run dev`
2. **Refresh your app**
3. **Check console** - should now show `buckets: Array(1)`
4. **Setup message should disappear**

## 🔧 **Why This Happened**

### **SQL vs UI Creation:**
- ✅ **SQL script** created database entry
- ❌ **App visibility** requires proper UI creation
- ✅ **Manual creation** ensures proper permissions

### **Environment Variables:**
- ❌ **NPM tokens** were causing client-side errors
- ✅ **Only NEXT_PUBLIC_** variables should be in .env.local
- ✅ **Fixed** by cleaning up environment file

## 🎉 **After Fix**

You should see:
- ✅ **No NPM_RC/NPM_TOKEN errors**
- ✅ **`buckets: Array(1)`** in console
- ✅ **`Images bucket found: {id: "images", ...}`**
- ✅ **`Storage configured: true`**
- ✅ **Setup message disappears**
- ✅ **Image upload works**
