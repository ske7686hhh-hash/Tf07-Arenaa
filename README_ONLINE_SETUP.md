# TF07 Arena – Online + Admin setup (Firebase, free)

1. console.firebase.google.com -> Add project.
2. Build -> Authentication -> Get started -> enable "Email/Password".
   Users tab -> Add user -> apna email + password (yehi tumhara ADMIN login hai).
3. Build -> Firestore Database -> Create database (production mode).
4. Firestore -> Rules tab me yeh paste karo (ske7686hhh@gmail.com ki jagah apna admin email) -> Publish:

rules_version = '2';
service cloud.firestore {
  match /databases/{db}/documents {
    function admin() { return request.auth != null && request.auth.token.email == 'ske7686hhh@gmail.com'; }
    match /tournaments/{d} { allow read: if true; allow write: if admin(); }
    match /scores/{d}      { allow read: if true; allow write: if admin(); }
    match /teams/{d}       { allow read: if true; allow create: if true; allow update, delete: if admin(); }
    match /regs/{d}        { allow create: if true; allow read, update, delete: if admin(); }
  }
}

5. Project settings (gear) -> General -> "Your apps" -> Web app (</>) register -> apiKey aur projectId copy karo.
6. app/src/main/assets/index.html me top ke paas CFG me teeno bharo:
   var CFG={apiKey:'...',projectId:'...',adminEmail:'ske7686hhh@gmail.com'};
7. GitHub par upload karke APK build karo.

Admin login kaise khule: Me tab -> "MY PROFILE" title par 5 baar tap -> email/password.
Rules ki wajah se sirf tumhara email tournaments/room/results badal sakta hai.
