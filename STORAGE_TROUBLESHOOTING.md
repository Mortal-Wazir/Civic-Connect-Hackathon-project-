# Storage Troubleshooting Guide

## 🔍 **Quick Diagnosis**

### **Check These in Order:**

#### **1. Bucket Exists?**
- Go to Supabase → Storage
- Look for **"images"** bucket
- If missing → Create it

#### **2. Bucket is Public?**
- Click on "images" bucket
- Should show **"Public"** badge
- If private → Make it public

#### **3. Correct Name?**
- Must be exactly `images` (plural)
- Not `image`, `photos`, or anything else
- Case sensitive

## 🚀 **Step-by-Step Fix**

### **Option A: Create New Bucket**
\`\`\`
1. Supabase Dashboard → Storage
2. "Create Bucket"
3. Name: images
4. Public: ON
5. Create
\`\`\`

### **Option B: Fix Existing Bucket**
\`\`\`
1. Click on existing bucket
2. Settings (gear icon)
3. Toggle "Public" to ON
4. Save changes
\`\`\`

## 🧪 **Test Upload**

### **Simple Test:**
1. Open your app
2. Sign in
3. Report Issue → Upload Photo
4. Select any image file
5. Should see preview

### **If Upload Fails:**
- Check browser console (F12)
- Look for specific error message
- Common fixes below

## 🔧 **Common Error Fixes**

### **"Bucket not found"**
- ✅ Create "images" bucket
- ✅ Make sure name is exactly `images`

### **"Upload not allowed"**  
- ✅ Make bucket public
- ✅ Check bucket settings

### **"Invalid file type"**
- ✅ Try JPEG or PNG file
- ✅ File should be under 10MB

### **"Authentication required"**
- ✅ Make sure you're signed in
- ✅ Refresh page and try again

## 📱 **Mobile Testing**

### **Test on Phone:**
1. Open app on mobile
2. Report Issue
3. Upload Photo → Camera
4. Take photo
5. Should work same as desktop

## ✅ **Success Indicators**

### **Storage Working When:**
- ✅ Image preview shows after selection
- ✅ Upload progress appears
- ✅ No error messages in console
- ✅ Photo appears on map after submit
- ✅ Can see file in Supabase Storage

### **Still Having Issues?**
- Try different image file
- Try different browser
- Check internet connection
- Clear browser cache

**Most storage issues are fixed by just creating the public "images" bucket!**
