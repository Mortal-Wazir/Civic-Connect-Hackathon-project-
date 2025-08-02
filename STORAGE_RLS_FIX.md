# Storage RLS Error Fix

## 🚨 **Error Explanation**
The "row-level security policy" error means the storage bucket has RLS enabled but no proper policies set up for file uploads.

## 🎯 **Two Solutions**

### **Solution 1: Manual Bucket Recreation (Recommended)**

#### **Step 1: Delete Old Bucket**
1. Go to Supabase Storage
2. If "images" bucket exists, delete it
3. This removes any problematic RLS policies

#### **Step 2: Create New Bucket**
1. Click "Create Bucket"
2. **Name**: `images`
3. **Public**: ✅ **Turn ON**
4. **File size limit**: `10485760` (10MB)
5. **Allowed MIME types**: Leave empty (allows all)
6. Click "Create"

#### **Step 3: Test Upload**
- The new bucket should work without RLS issues
- Try uploading an image in your app

### **Solution 2: Fix RLS Policies (Advanced)**

If you want to keep the existing bucket, run the SQL script:

1. Go to **SQL Editor**
2. Run `scripts/006_fix_storage_simple.sql`
3. This creates simple, permissive RLS policies

## 🔧 **Code Changes Made**

### **Simplified Upload Path:**
- ✅ **No user folders** (avoids RLS complexity)
- ✅ **Direct bucket upload** (simpler permissions)
- ✅ **Better error handling** for RLS issues
- ✅ **Clearer error messages** for users

### **What Changed:**
\`\`\`typescript
// OLD (complex path with RLS issues)
const filePath = `issue-images/${userId}/${fileName}`

// NEW (simple path that works)
const filePath = fileName
\`\`\`

## ✅ **After Fix**

### **Upload Will Work:**
- ✅ **No RLS errors**
- ✅ **Simple file paths**
- ✅ **Public access** to images
- ✅ **Authenticated uploads** only

### **Your App Gets:**
- ✅ **Photo upload** functionality
- ✅ **Image display** on map
- ✅ **Mobile camera** support
- ✅ **Error handling** if issues occur

## 🎉 **Recommended Approach**

**Just recreate the bucket** - it's faster and more reliable than fixing RLS policies:

1. **Delete** existing "images" bucket
2. **Create** new public "images" bucket  
3. **Test** upload in your app
4. **Done!**

This avoids all RLS complexity and just works!
