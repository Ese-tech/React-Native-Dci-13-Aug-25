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

# Dependencies installieren
bun add express cors dotenv
bun add mongoose jsonwebtoken bcrypt
bun add -d @types/express @types/cors @types/jsonwebtoken @types/bcrypt typescript tsx

# TypeScript Config erstellen
bunx tsc --init
```

#### 📋 Backend package.json:
```json
{
  "name": "todo-backend",
  "version": "1.0.0",
  "scripts": {
    "dev": "tsx --watch src/index.ts",
    "build": "tsc",
    "start": "node dist/index.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^8.0.0",
    "jsonwebtoken": "^9.0.2",
    "bcrypt": "^5.1.1",
    "cors": "^2.8.5",
    "dotenv": "^16.3.1"
  },
  "devDependencies": {
    "@types/express": "^4.17.21",
    "@types/jsonwebtoken": "^9.0.5",
    "@types/bcrypt": "^5.0.2",
    "@types/cors": "^2.8.17",
    "typescript": "^5.2.2",
    "tsx": "^4.6.0"
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

# Zusätzliche Dependencies
bun add @react-navigation/native @react-navigation/native-stack
bun add react-native-screens react-native-safe-area-context
bun add axios react-hook-form
bun add @expo/vector-icons
```

#### 📋 Frontend package.json:
```json
{
  "name": "todo-frontend",
  "version": "1.0.0",
  "scripts": {
    "start": "expo start",
    "android": "expo start --android",
    "ios": "expo start --ios",
    "web": "expo start --web"
  },
  "dependencies": {
    "expo": "~50.0.0",
    "react": "18.2.0",
    "react-native": "0.73.0",
    "@react-navigation/native": "^6.1.9",
    "@react-navigation/native-stack": "^6.9.17",
    "axios": "^1.6.0",
    "react-hook-form": "^7.48.0"
  },
  "devDependencies": {
    "@types/react": "~18.2.45",
    "typescript": "^5.1.3"
  }
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

# Build Commands
expo build:android           # Android APK
expo build:ios              # iOS IPA (nur Mac)
expo publish                # App zu Expo veröffentlichen

# Projekt Management
expo install                 # Kompatible Packages installieren
expo doctor                  # Projekt auf Probleme prüfen
expo logout / expo login     # Account Management
```

---

## 9️⃣ Beispiel Code-Struktur

### 🔹 Backend Models (Mongoose):
```typescript
// backend/src/models/User.ts
import mongoose from 'mongoose';
import bcrypt from 'bcrypt';

interface IUser {
  email: string;
  password: string;
  name: string;
  comparePassword(password: string): Promise<boolean>;
}

const userSchema = new mongoose.Schema<IUser>({
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  name: { type: String, required: true }
});

userSchema.pre('save', async function(next) {
  if (!this.isModified('password')) return next();
  this.password = await bcrypt.hash(this.password, 10);
  next();
});

userSchema.methods.comparePassword = async function(password: string) {
  return bcrypt.compare(password, this.password);
};

export default mongoose.model<IUser>('User', userSchema);
```

### 🔹 Frontend Auth Service:
```typescript
// frontend/src/services/auth.ts
import axios from 'axios';

const API_URL = 'http://localhost:3000/api';

export const authService = {
  login: async (email: string, password: string) => {
    const response = await axios.post(`${API_URL}/auth/login`, {
      email,
      password
    });
    return response.data;
  },

  register: async (name: string, email: string, password: string) => {
    const response = await axios.post(`${API_URL}/auth/register`, {
      name,
      email,
      password
    });
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

