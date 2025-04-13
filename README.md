# DBA-QuaraNThangz
Your neighborhood tech specialist

# Quara N Thangz Digital & Spiritual Services

## Services Offered

### Logo & Branding Design
- **Budget ($250)**
- **Standard ($500)**
- **Premium ($800)**

**Add-ons**:
- Vector Files ($50)
- Animated Logos ($100)

### Website Design
- **Budget ($1000)**
- **Standard ($2500)**
- **Premium ($5000)**

**Add-ons**:
- SEO Optimization ($300)
- E-commerce Integration ($500)

### Custom Tarot & Oracle Decks
- **WTF Tarot Chronicles ($50)**
- **90s R&B Queens Oracle Deck ($100)**
- **Proverbs 31 Woman Deck ($150)**

### Energy Balancing & Chakra Alignment
- **Single Session ($90)**
- **3 Sessions Package ($250)**
- **5 Sessions Package ($400)**

---

For more details or to request a service, please visit our [website](https://quara-n-thangz.square.site/).

---

## Tech Stack

- React (Frontend)
- Firebase (Auth + Firestore)
- Tailwind CSS (Styling)
- Stripe (Payments Integration)
- Spotify API Toolkit (Optional Music Integration)

---

## Firebase Auth + Firestore Setup (Sample)

### `firebaseConfig.js`
```js
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";
import { getFirestore } from "firebase/firestore";

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_STORAGE_BUCKET",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID",
  measurementId: "YOUR_MEASUREMENT_ID"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

export { auth, db };
```

---

## Components

### `Login.jsx`
```jsx
import { useState } from "react";
import { signInWithEmailAndPassword } from "firebase/auth";
import { auth } from "../../firebase/firebaseConfig";

export default function Login() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  const handleLogin = async () => {
    try {
      await signInWithEmailAndPassword(auth, email, password);
      alert("Login successful!");
    } catch (error) {
      alert("Login failed: " + error.message);
    }
  };

  return (
    <div className="p-4 max-w-sm mx-auto">
      <h2 className="text-xl font-bold mb-2">Login</h2>
      <input 
        type="email" 
        value={email} 
        onChange={(e) => setEmail(e.target.value)} 
        placeholder="Email" 
        className="w-full p-2 border mb-2" 
      />
      <input 
        type="password" 
        value={password} 
        onChange={(e) => setPassword(e.target.value)} 
        placeholder="Password" 
        className="w-full p-2 border mb-2" 
      />
      <button onClick={handleLogin} className="bg-indigo-700 text-white px-4 py-2 rounded">Login</button>
    </div>
  );
}
```

### `Register.jsx`
```jsx
import { useState } from "react";
import { createUserWithEmailAndPassword } from "firebase/auth";
import { auth } from "../../firebase/firebaseConfig";

export default function Register() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  const handleRegister = async () => {
    try {
      await createUserWithEmailAndPassword(auth, email, password);
      alert("Account created!");
    } catch (error) {
      alert("Registration failed: " + error.message);
    }
  };

  return (
    <div className="p-4 max-w-sm mx-auto">
      <h2 className="text-xl font-bold mb-2">Register</h2>
      <input 
        type="email" 
        value={email} 
        onChange={(e) => setEmail(e.target.value)} 
        placeholder="Email" 
        className="w-full p-2 border mb-2" 
      />
      <input 
        type="password" 
        value={password} 
        onChange={(e) => setPassword(e.target.value)} 
        placeholder="Password" 
        className="w-full p-2 border mb-2" 
      />
      <button onClick={handleRegister} className="bg-emerald-700 text-white px-4 py-2 rounded">Register</button>
    </div>
  );
}
```

### `AdminDashboard.jsx`
```jsx
import { useEffect, useState } from "react";
import { db } from "../firebase/firebaseConfig";
import { collection, getDocs } from "firebase/firestore";

export default function AdminDashboard() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    const fetchUsers = async () => {
      const querySnapshot = await getDocs(collection(db, "users"));
      setUsers(querySnapshot.docs.map(doc => ({ id: doc.id, ...doc.data() })));
    };

    fetchUsers();
  }, []);

  return (
    <div className="p-4">
      <h1 className="text-xl font-bold mb-4">Admin Dashboard</h1>
      <ul className="space-y-2">
        {users.map(user => (
          <li key={user.id} className="p-2 border rounded bg-white shadow-sm">
            {user.email || "Unnamed user"} - Role: {user.role || "User"}
          </li>
        ))}
      </ul>
    </div>
  );
}
```

---

## Firestore User Template
```json
{
  "email": "",
  "role": "user",
  "settings": {
    "theme": "light",
    "ritualPreferences": []
  },
  "createdAt": "TIMESTAMP"
}
```

---

## Coming Soon
- Stripe payment gateway integration
- Spotify playlist toolkit based on spiritual mood
- Ritual templates per deck
- Admin controls to assign user rituals & manage spiritual services
