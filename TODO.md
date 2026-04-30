# eDemand Error Fixes - TODO

Current Working Directory: d:/node wap projects 2026/Azo App Project/eDemand v4.7.0/eDemand web v4.7.0

## Issues:
1. LoadScript warnings from Google Maps (api calls causing re-renders)
2. 404 on /undefined (dynamic route undefined param)  
3. /become-provider?lang=en auto-redirects to home

## Step-by-Step Plan:

### 1. Fix API Middleware Content-Type ✅
**File:** src/api/apiMiddleware.js
- Always sets 'multipart/form-data' → breaks JSON APIs
- Dynamic: FormData → multipart, else application/json
- Prevents re-renders → fixes LoadScript warnings  
**Status:** Completed - apiMiddleware.js ✅**

**File:** src/api/apiMiddleware.js
- Always sets 'multipart/form-data' → breaks JSON APIs
- Dynamic: FormData → multipart, else application/json
- Prevents re-renders → fixes LoadScript warnings

### 2. Fix Become Provider Redirect ✅ COMPLETE
**Root Cause:** Layout.jsx redirects non-public routes to /home without location data
**File:** src/utils/Helper.js 
- Added `"/become-provider"` to `publicRoutes` array
- **Now exempt from location redirect** ✅

**File:** src/pages/become-provider/index.jsx  
- Read file, identify auth/redirect logic
- Add bypass for public access or fix condition

### 3. Optimize LandingPage API Calls [PENDING]  
**File:** src/components/LandingPage/LandingPage.jsx
- Memoize callbacks to prevent re-renders
- useCallback/useMemo for API functions

### 4. Find/Fix /undefined 404 [PENDING]
- Search router.push() with undefined params
- Fix dynamic routes [slug]/[...slug]

### 5. Test & Verify [PENDING]
```
npm run dev
Test: http://localhost:3004/become-provider?lang=en
Check console/network for errors
```

**Next:** Implement Step 1 (apiMiddleware.js)

