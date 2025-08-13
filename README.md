# 📱 React Native mit TypeScript & Bun – Einführung für Anfänger

Willkommen! Heute lernst du, was **React Native** ist, warum wir es brauchen, und wie man es mit **TypeScript** & **Bun** installiert. Außerdem gibt es ein paar kleine Codebeispiele.

---

## 1️⃣ Was ist React Native?

**React Native** ist ein Framework, mit dem wir **mobile Apps** für **Android** und **iOS** bauen können – **mit JavaScript oder TypeScript**.  
Das Coole: Wir schreiben nur **einen Code**, und React Native übersetzt ihn so, dass die App auf beiden Plattformen funktioniert.

📝 **Beispiel**:  
- Dein Code in React Native → läuft als App auf Android, iOS **oder** Web.  
- Kein doppelter Code für jede Plattform nötig.

---

## 2️⃣ Warum brauchen wir React Native?

- 📱 **Cross-Platform** → Ein Code für iOS und Android
- 🕸️ **Web** → Mit Expo kann man auch Web-Apps bauen
- ⚡ **Schnelle Entwicklung** → Hot Reload & Fast Refresh
- 🌍 **Große Community** → Viele fertige Komponenten und Libraries
- 💡 **JavaScript & TypeScript** → Leicht zu lernen, wenn man schon Web-Entwicklung kennt
- 🔌 **Native Funktionen** → Kamera, GPS, Push Notifications, etc.

---

## 3️⃣ Was ist TypeScript in React Native?

**TypeScript** ist wie JavaScript, aber mit **Typen**.  
Das hilft dir, Fehler schon beim Programmieren zu finden.

📝 **Beispiel:**
```ts
// JavaScript (ohne Typen)
function greet(name) {
  return "Hallo " + name;
}

// TypeScript (mit Typen)
function greet(name: string): string {
  return "Hallo " + name;
}
```
---


## 4️⃣ Was ist Bun und warum hier?
**Bun** ist ein superschneller JavaScript- & TypeScript-Runner (wie Node.js, aber schneller).
Wir können damit schnell Pakete installieren und Skripte ausführen.

---

## 5️⃣ Was ist Expo?

**Expo** ist ein Framework und eine Plattform für React Native, die die Entwicklung erheblich vereinfacht.

### 🔹 Expo Vorteile:
- 📱 **Expo Go App** → Keine lokale Android/iOS-Entwicklungsumgebung nötig
- 🔄 **Hot Reload** → Änderungen werden sofort auf dem Handy angezeigt
- 🛠️ **Viele fertige APIs** → Kamera, Sensoren, Notifications, etc.
- 🌐 **Web Support** → App läuft auch im Browser
- 📦 **Easy Build** → Apps können einfach für App Stores gebaut werden

### 🔹 Expo Go vs. Development Build:
- **Expo Go**: Fertige App zum Testen (begrenzte native Module)
- **Development Build**: Custom Build mit allen nativen Modulen

---

## 6️⃣ Installation/Initialisierung – Schritt für Schritt
**🔹 Voraussetzungen:**
- Git installiert
- Bun installiert (bun.sh)
- Expo Go App auf dem Handy (Android / iOS Store)


---

### 6.1 Neues Projekt erstellen (mit TypeScript)
```bash
# Neues React Native Projekt erstellen
bun create expo my-app --template tabs@latest

# In das Projekt wechseln
cd my-app

# TypeScript aktivieren (falls noch nicht vorhanden)
bun add -d typescript @types/react @types/react-native

# Expo CLI global installieren
bun add -g @expo/cli
```

---

### 6.2 App starten
```bash
# App im Entwicklungsmodus starten
bun dev
# oder
expo start

# Für Web
expo start --web

# Für Android Emulator
expo start --android

# Für iOS Simulator (nur auf Mac)
expo start --ios
```

- 📱 Danach den QR-Code in der Konsole mit der Expo Go App scannen → App läuft auf deinem Handy.

---

## 7️⃣ Fullstack Todo App Setup (Login/Register + Todo CRUD)

### 🏗️ Projektstruktur:
```
fullstack-todo/
│
├── backend/        # Bun + TypeScript REST API
│   ├── src/
│   │   ├── models/         # Mongoose Schemas
│   │   ├── controllers/    # Route Handler
│   │   ├── middleware/     # Auth & Validation
│   │   ├── routes/         # API Routes
│   │   ├── utils/          # Helper Functions
│   │   └── index.ts        # Server Entry Point
│   ├── package.json
│   └── tsconfig.json
│
├── frontend/       # React Native App (Expo + TypeScript)
│   ├── src/
│   │   ├── components/     # Reusable Components
│   │   ├── screens/        # App Screens
│   │   ├── auth/           # Login/Register
│   │   ├── services/       # API Calls
│   │   ├── utils/          # Helper Functions
│   │   └── types/          # TypeScript Types
│   ├── App.tsx
│   ├── package.json
│   └── tsconfig.json
│
└── README.md
```

---

### 7.1 Backend Setup (Bun + Express + MongoDB)

#### 📦 Backend Dependencies:
```bash
# Backend Verzeichnis erstellen
mkdir fullstack-todo && cd fullstack-todo
mkdir backend && cd backend

# package.json erstellen
bun init -y

# Core Dependencies
bun add express cors dotenv helmet compression
bun add mongoose jsonwebtoken bcrypt
bun add express-rate-limit express-validator
bun add morgan cookie-parser

# Dev Dependencies
bun add -d @types/express @types/cors @types/jsonwebtoken 
bun add -d @types/bcrypt @types/morgan @types/cookie-parser
bun add -d typescript tsx nodemon @types/compression
```

#### 📋 Backend package.json (Updated):
```json
{
  "name": "fullstack-todo-backend",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "tsx --watch src/index.ts",
    "build": "tsc",
    "start": "node dist/index.js",
    "start:prod": "NODE_ENV=production node dist/index.js",
    "test": "bun test",
    "lint": "eslint src --ext .ts",
    "format": "prettier --write src"
  },
  "dependencies": {
    "express": "^4.19.2",
    "mongoose": "^8.5.0",
    "jsonwebtoken": "^9.0.2",
    "bcrypt": "^5.1.1",
    "cors": "^2.8.5",
    "dotenv": "^16.4.5",
    "helmet": "^7.1.0",
    "compression": "^1.7.4",
    "express-rate-limit": "^7.3.1",
    "express-validator": "^7.1.0",
    "morgan": "^1.10.0",
    "cookie-parser": "^1.4.6"
  },
  "devDependencies": {
    "@types/express": "^4.17.21",
    "@types/jsonwebtoken": "^9.0.6",
    "@types/bcrypt": "^5.0.2",
    "@types/cors": "^2.8.17",
    "@types/morgan": "^1.9.9",
    "@types/cookie-parser": "^1.4.7",
    "@types/compression": "^1.7.5",
    "typescript": "^5.5.0",
    "tsx": "^4.16.0",
    "nodemon": "^3.1.4"
  }
}
```

---

### 7.2 Frontend Setup (React Native + Expo)

#### 📱 Frontend Dependencies:
```bash
# Zurück zum Hauptverzeichnis
cd ..

# React Native Expo App erstellen
bun create expo frontend --template tabs@latest
cd frontend

# Zusätzliche Dependencies für Todo App
bun add @react-native-async-storage/async-storage
bun add @hookform/resolvers axios
bun add expo-router expo-secure-store
bun add expo-status-bar expo-splash-screen
bun add nativewind react-hook-form zod
bun add react-native-gesture-handler react-native-reanimated
bun add react-native-safe-area-context react-native-screens

# Dev Dependencies
bun add -d @expo/cli tailwindcss
```

#### 📋 Frontend package.json (Todo App):
```json
{
  "name": "fullstack-todo-mobile",
  "main": "expo-router/entry",
  "version": "1.0.0",
  "scripts": {
    "start": "bun exec expo start",
    "android": "bun exec expo start --android",
    "ios": "bun exec expo start --ios",
    "web": "bun exec expo start --web",
    "lint": "bun exec expo lint",
    "test": "bun test",
    "build:android": "bun exec expo build:android",
    "build:ios": "bun exec expo build:ios"
  },
  "dependencies": {
    "@hookform/resolvers": "^5.0.1",
    "@react-native-async-storage/async-storage": "2.1.2",
    "axios": "^1.7.0",
    "expo": "~53.0.0",
    "expo-auth-session": "~6.2.0",
    "expo-constants": "^17.1.7",
    "expo-router": "^5.0.0",
    "expo-secure-store": "^14.0.0",
    "expo-splash-screen": "^0.30.0",
    "expo-status-bar": "^2.2.0",
    "nativewind": "^4.1.23",
    "react": "19.0.0",
    "react-dom": "19.0.0",
    "react-hook-form": "^7.56.4",
    "react-native": "0.79.5",
    "react-native-gesture-handler": "~2.24.0",
    "react-native-reanimated": "~3.17.4",
    "react-native-safe-area-context": "5.4.0",
    "react-native-screens": "~4.11.1",
    "react-native-web": "^0.20.0",
    "zod": "^3.25.28"
  },
  "devDependencies": {
    "@babel/core": "^7.25.2",
    "@expo/cli": "^0.24.17",
    "@expo/config-plugins": "^10.1.1",
    "@testing-library/react-native": "^12.4.0",
    "@types/react": "~19.0.10",
    "jest": "^29.7.0",
    "react-test-renderer": "18.3.1",
    "tailwindcss": "^3.4.0",
    "typescript": "~5.8.3"
  },
  "private": true
}
```

---

## 8️⃣ Terminal Commands Übersicht

### 🔹 Projekt initialisieren:
```bash
# 1. Hauptordner erstellen
mkdir fullstack-todo && cd fullstack-todo

# 2. Backend Setup
mkdir backend && cd backend
bun init -y
bun add express mongoose jsonwebtoken bcrypt cors dotenv
bun add -d typescript @types/express @types/mongoose tsx

# 3. Frontend Setup
cd ..
bun create expo frontend --template tabs@latest
cd frontend
bun add @react-navigation/native axios

# 4. Development starten
# Terminal 1 (Backend):
cd backend && bun dev

# Terminal 2 (Frontend):
cd frontend && bun start
```

### 🔹 Expo Commands:
```bash
# App starten
expo start                    # QR Code für Expo Go
expo start --web             # Im Browser öffnen
expo start --android         # Android Emulator
expo start --ios             # iOS Simulator (nur Mac)
expo start --clear-cache     # Cache leeren

# Build Commands (EAS Build)
eas build --platform android # Android APK/AAB
eas build --platform ios     # iOS IPA (nur Mac)
eas build --platform all     # Beide Plattformen

# Development Build
eas build --profile development --platform android
expo install --fix           # Kompatible Packages installieren

# Projekt Management
expo doctor                   # Projekt auf Probleme prüfen
expo logout / expo login      # Account Management
npx create-expo-app --template # Template Liste anzeigen

# Testing & Debugging
expo start --dev-client      # Mit Development Build
expo start --tunnel          # Über Internet teilen
```

---

## 9️⃣ Moderne Konfigurationsdateien

### 🔹 app.json/app.config.js (Expo Config):
```json
{
  "expo": {
    "name": "Todo App",
    "slug": "fullstack-todo-app",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "userInterfaceStyle": "automatic",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "assetBundlePatterns": ["**/*"],
    "ios": {
      "supportsTablet": true,
      "bundleIdentifier": "com.yourname.todoapp"
    },
    "android": {
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#ffffff"
      },
      "package": "com.yourname.todoapp"
    },
    "web": {
      "favicon": "./assets/favicon.png",
      "bundler": "metro"
    },
    "plugins": [
      "expo-router",
      "expo-secure-store",
      [
        "expo-splash-screen",
        {
          "backgroundColor": "#ffffff",
          "image": "./assets/splash.png",
          "dark": {
            "image": "./assets/splash-dark.png",
            "backgroundColor": "#000000"
          }
        }
      ]
    ],
    "scheme": "todoapp",
    "extra": {
      "router": {
        "origin": false
      },
      "eas": {
        "projectId": "your-project-id"
      }
    }
  }
}
```

### 🔹 tailwind.config.js (NativeWind):
```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./App.{js,jsx,ts,tsx}",
    "./app/**/*.{js,jsx,ts,tsx}",
    "./components/**/*.{js,jsx,ts,tsx}"
  ],
  presets: [require("nativewind/preset")],
  theme: {
    extend: {
      colors: {
        primary: "#3B82F6",
        secondary: "#64748B",
        success: "#10B981",
        warning: "#F59E0B",
        danger: "#EF4444"
      }
    }
  },
  plugins: []
};
```

### 🔹 .env Beispiel (Backend):
```env
# Database
MONGODB_URI=mongodb://localhost:27017/todoapp
MONGODB_URI_PROD=mongodb+srv://user:pass@cluster.mongodb.net/todoapp

# JWT
JWT_SECRET=your-super-secret-jwt-key-here
JWT_EXPIRES_IN=7d

# Server
PORT=3000
NODE_ENV=development

# CORS
FRONTEND_URL=http://localhost:8081
ALLOWED_ORIGINS=http://localhost:8081,exp://192.168.1.100:8081

# Rate Limiting
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
```

---

## 🔟 Beispiel Code-Struktur

### 🔹 Backend Models (Mongoose mit TypeScript):
```typescript
// backend/src/models/User.ts
import mongoose, { Document, Schema } from 'mongoose';
import bcrypt from 'bcrypt';

export interface IUser extends Document {
  _id: string;
  email: string;
  password: string;
  name: string;
  avatar?: string;
  createdAt: Date;
  updatedAt: Date;
  comparePassword(password: string): Promise<boolean>;
}

const userSchema = new Schema<IUser>({
  email: { 
    type: String, 
    required: true, 
    unique: true,
    lowercase: true,
    trim: true
  },
  password: { 
    type: String, 
    required: true,
    minlength: 6
  },
  name: { 
    type: String, 
    required: true,
    trim: true
  },
  avatar: {
    type: String,
    default: null
  }
}, {
  timestamps: true
});

// Hash password before saving
userSchema.pre('save', async function(next) {
  if (!this.isModified('password')) return next();
  this.password = await bcrypt.hash(this.password, 12);
  next();
});

// Compare password method
userSchema.methods.comparePassword = async function(password: string) {
  return bcrypt.compare(password, this.password);
};

export default mongoose.model<IUser>('User', userSchema);
```

### 🔹 Todo Model:
```typescript
// backend/src/models/Todo.ts
import mongoose, { Document, Schema } from 'mongoose';

export interface ITodo extends Document {
  title: string;
  description?: string;
  completed: boolean;
  priority: 'low' | 'medium' | 'high';
  dueDate?: Date;
  user: mongoose.Types.ObjectId;
  createdAt: Date;
  updatedAt: Date;
}

const todoSchema = new Schema<ITodo>({
  title: {
    type: String,
    required: true,
    trim: true,
    maxlength: 100
  },
  description: {
    type: String,
    trim: true,
    maxlength: 500
  },
  completed: {
    type: Boolean,
    default: false
  },
  priority: {
    type: String,
    enum: ['low', 'medium', 'high'],
    default: 'medium'
  },
  dueDate: {
    type: Date,
    default: null
  },
  user: {
    type: Schema.Types.ObjectId,
    ref: 'User',
    required: true
  }
}, {
  timestamps: true
});

export default mongoose.model<ITodo>('Todo', todoSchema);
```

### 🔹 Frontend Auth Service (mit Expo Secure Store):
```typescript
// frontend/src/services/auth.ts
import axios from 'axios';
import * as SecureStore from 'expo-secure-store';
import { API_URL } from '../config';

interface LoginResponse {
  token: string;
  user: {
    id: string;
    email: string;
    name: string;
  };
}

export const authService = {
  // Login
  login: async (email: string, password: string): Promise<LoginResponse> => {
    const response = await axios.post(`${API_URL}/auth/login`, {
      email,
      password
    });
    
    // Token sicher speichern
    await SecureStore.setItemAsync('token', response.data.token);
    return response.data;
  },

  // Register
  register: async (name: string, email: string, password: string): Promise<LoginResponse> => {
    const response = await axios.post(`${API_URL}/auth/register`, {
      name,
      email,
      password
    });
    
    await SecureStore.setItemAsync('token', response.data.token);
    return response.data;
  },

  // Logout
  logout: async (): Promise<void> => {
    await SecureStore.deleteItemAsync('token');
  },

  // Get stored token
  getToken: async (): Promise<string | null> => {
    return await SecureStore.getItemAsync('token');
  },

  // Check if user is authenticated
  isAuthenticated: async (): Promise<boolean> => {
    const token = await SecureStore.getItemAsync('token');
    return !!token;
  }
};
```

### 🔹 Frontend Todo Service:
```typescript
// frontend/src/services/todoService.ts
import axios from 'axios';
import * as SecureStore from 'expo-secure-store';
import { API_URL } from '../config';

export interface Todo {
  _id: string;
  title: string;
  description?: string;
  completed: boolean;
  priority: 'low' | 'medium' | 'high';
  dueDate?: string;
  createdAt: string;
  updatedAt: string;
}

// Axios Interceptor für Authorization Header
axios.interceptors.request.use(async (config) => {
  const token = await SecureStore.getItemAsync('token');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

export const todoService = {
  // Get all todos
  getTodos: async (): Promise<Todo[]> => {
    const response = await axios.get(`${API_URL}/todos`);
    return response.data;
  },

  // Create todo
  createTodo: async (todo: Partial<Todo>): Promise<Todo> => {
    const response = await axios.post(`${API_URL}/todos`, todo);
    return response.data;
  },

  // Update todo
  updateTodo: async (id: string, updates: Partial<Todo>): Promise<Todo> => {
    const response = await axios.put(`${API_URL}/todos/${id}`, updates);
    return response.data;
  },

  // Delete todo
  deleteTodo: async (id: string): Promise<void> => {
    await axios.delete(`${API_URL}/todos/${id}`);
  },

  // Toggle completion
  toggleComplete: async (id: string): Promise<Todo> => {
    const response = await axios.patch(`${API_URL}/todos/${id}/toggle`);
    return response.data;
  }
};
```

---

## 🔟 Ein kleines Beispiel – Counter App

```tsx
// App.tsx
import React, { useState } from "react";
import { Text, View, Button, StyleSheet } from "react-native";

export default function App() {
  const [count, setCount] = useState<number>(0);

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Zähler: {count}</Text>
      <Button title="Hochzählen" onPress={() => setCount(count + 1)} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  text: {
    fontSize: 24,
    marginBottom: 20,
  },
});
```

---

## 1️⃣1️⃣ Neue Features in React Native (2025)
🚀 **New Architecture** → Bessere Performance

🖼️ **Fabric Renderer** → Schnelleres UI-Rendering

⚡ **Hermes Engine** → Schnellere JavaScript-Ausführung

🛠️ **Improved Dev Tools** → Bessere Debugging-Möglichkeiten

🌐 **Expo Router** → Einfaches Navigieren zwischen Screens

📱 **Expo SDK 50** → Neue APIs und bessere TypeScript-Unterstützung

---

## 1️⃣2️⃣ Nützliche Links & Ressourcen

### 📚 Dokumentation:
- [React Native Docs](https://reactnative.dev/)
- [Expo Documentation](https://docs.expo.dev/)
- [TypeScript in React Native](https://reactnative.dev/docs/typescript)
- [Bun Documentation](https://bun.sh/)
- [Mongoose Documentation](https://mongoosejs.com/)

### 🛠️ Tools & Services:
- [Expo Go App](https://expo.dev/client) - Zum Testen auf dem Handy
- [MongoDB Atlas](https://www.mongodb.com/atlas) - Cloud Database
- [Postman](https://www.postman.com/) - API Testing
- [React Native Directory](https://reactnative.directory/) - Package Library

### 🎯 Nächste Schritte:
1. ✅ Expo Go App auf dem Handy installieren
2. ✅ Erstes React Native Projekt erstellen
3. ✅ Fullstack Todo App entwickeln
4. ✅ App für Android/iOS builden
5. ✅ In App Stores veröffentlichen

---

**Viel Spaß beim Entwickeln! 🚀📱**

