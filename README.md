# CampusIQ — Smart Campus Attendance

Responsive React/Vite starter for a college attendance management project. Includes overview analytics, role-preview settings, QR generation, browser QR scanning, attendance records, student/teacher pages, subject/class cards, reports, CSV export, and Firebase Auth/Firestore hooks.

## 1. Run locally

Install Node.js 18+ and then:

```bash
npm install
cp .env.example .env
npm run dev
```

Open the local address printed by Vite. Without Firebase environment values, the app opens in demo mode with sample records.

## 2. Connect Firebase

1. Create a project in the Firebase Console.
2. Enable **Authentication → Email/Password**.
3. Create a **Cloud Firestore** database.
4. Copy the web app configuration values into `.env` using the names in `.env.example`.
5. Restart the Vite server after editing `.env`.

New registrations are assigned the `student` role. For real admin/teacher roles, set roles only through a trusted admin workflow or server-side process. Never let a user grant themselves a privileged role.

## 3. Important production work still required

This is a project starter, not a secure production attendance system. Before using real student data:

- Implement strict Firestore Security Rules for role-based access and data ownership.
- Move session creation and attendance marking into a trusted backend (Cloud Functions or Node/Express).
- Generate cryptographically random, short-lived QR tokens on the server. Store token hashes, expiry, session status and class association server-side. Do not trust client-provided expiry or student IDs.
- Validate the QR token, authenticated student, expiry, duplicate attendance, and campus distance on the server in a single transaction.
- Store official campus coordinates in protected configuration. Browser geolocation requires permission and HTTPS; coordinates can be spoofed, so geolocation alone is not proof of presence.
- Add user/role management, audit logs, consent/retention rules, and error monitoring.
- The sample dashboard rows and charts are mock data; they are not live database analytics yet.

## 4. Current Firebase wiring

- Firebase Authentication: email/password login and registration.
- Firestore: creates a user profile after registration and writes QR session metadata when signed in.
- Most dashboard tables and charts use sample data for UI demonstration. Replace these with Firestore queries after securing the data model and backend.
