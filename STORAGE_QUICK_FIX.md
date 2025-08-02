# Quick Storage Fix - 2 Minutes

## 🎯 **Storage Issue Diagnosis**

Since everything else works, the storage issue is likely:
- ❌ **No "images" bucket** exists
- ❌ **Bucket exists but not public**
- ❌ **Bucket has wrong name**

## 🚀 **Quick Fix Steps**

### **Step 1: Check Current Storage**
1. Go to: https://supabase.com/dashboard/project/rdnmkvmgdbakulwopvuj
2. Click **"Storage"** in left sidebar
3. Look for **"images"** bucket

### **Step 2A: If No "images" Bucket**
1. Click **"Create Bucket"**
2. **Name**: `images` (exactly this name)
3. **Public**: ✅ **Turn ON** (very important!)
4. **File size limit**: `10485760` (10MB)
5. Click **"Create"**

### **Step 2B: If "images" Bucket Exists**
1. Click on the **"images"** bucket
2. Click **"Settings"** (gear icon)
3. Make sure **"Public"** is ✅ **ON**
4. Save if you made changes

### **Step 3: Test Upload**
1. Refresh your app
2. Try reporting an issue with photo
3. Should work now!

## 🔍 **What to Look For**

### **Correct Setup:**
- ✅ Bucket named exactly `images`
- ✅ Shows **"Public"** badge
- ✅ No errors when clicking on it

### **Common Issues:**
- ❌ Bucket named `image` (missing 's')
- ❌ Bucket is private (no public badge)
- ❌ No bucket exists at all

## 🛠️ **If Still Not Working**

### **Check Browser Console:**
1. Open your app
2. Press **F12** (developer tools)
3. Go to **Console** tab
4. Try uploading image
5. Look for error messages

### **Common Error Messages:**
- **"Bucket not found"** → Create the bucket
- **"Upload not allowed"** → Make bucket public
- **"Invalid file type"** → Try different image format

## ✅ **After Fix**

Your app will have:
- ✅ **Photo upload** working
- ✅ **Image preview** before submit
- ✅ **Photos display** on map markers
- ✅ **Mobile camera** support

## 🎉 **Verification Steps**

### **Test Upload:**
1. Sign in to your app
2. Click **"Report Issue"**
3. Click **"Upload Photo"**
4. Select an image
5. Should see preview
6. Submit the issue
7. Photo should appear on map

### **Check Storage:**
1. Go back to Supabase Storage
2. Click on **"images"** bucket
3. Should see your uploaded file
4. Click on file to verify it's accessible

**The storage fix is usually just creating the bucket or making it public!**
