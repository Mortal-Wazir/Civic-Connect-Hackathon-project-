# Quick Storage Fix - Recreate Bucket

## 🚀 **Fastest Fix (2 minutes)**

The RLS error is from complex storage policies. Let's just recreate the bucket cleanly:

### **Step 1: Delete Old Bucket**
1. Go to: https://supabase.com/dashboard/project/rdnmkvmgdbakulwopvuj
2. Click **Storage**
3. If "images" bucket exists:
   - Click the **3 dots** next to it
   - Click **Delete**
   - Confirm deletion

### **Step 2: Create Fresh Bucket**
1. Click **"Create Bucket"**
2. **Settings**:
   - **Name**: `images`
   - **Public**: ✅ **ON**
   - **File size limit**: `10485760` (10MB)
   - **Allowed MIME types**: Leave empty
3. Click **"Create"**

### **Step 3: Test Upload**
1. **Refresh your app**
2. **Sign in**
3. **Report Issue** → **Upload Photo**
4. **Should work now!**

## ✅ **Why This Works**

### **Fresh Bucket Benefits:**
- ✅ **No RLS policies** to cause conflicts
- ✅ **Default permissions** that work
- ✅ **Public access** enabled
- ✅ **Simple setup** without complexity

### **What You Get:**
- ✅ **Photo uploads** working
- ✅ **Image previews** in forms
- ✅ **Photos on map** markers
- ✅ **Mobile camera** support

## 🎯 **Alternative: Keep Existing Bucket**

If you don't want to delete the bucket, you can run the SQL script `006_fix_storage_simple.sql` in the SQL Editor to fix the RLS policies.

**But recreating is faster and more reliable!**
