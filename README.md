// ProServi Web App (Versión básica MVP) // Framework: React con Tailwind CSS // Backend: Firebase (Auth + Firestore)

// Estructura de archivos: // src/ // ├── App.jsx // ├── main.jsx // ├── components/ // │   ├── Navbar.jsx // │   ├── ServiceList.jsx // │   ├── ProfessionalProfile.jsx // │   ├── RequestForm.jsx // │   └── RegisterForm.jsx // ├── pages/ // │   ├── Home.jsx // │   ├── Register.jsx // │   ├── ProfessionalDashboard.jsx // └── firebase.js

// ===== tailwind.config.js ===== module.exports = { content: [ "./index.html", "./src/**/*.{js,ts,jsx,tsx}", ], theme: { extend: {}, }, plugins: [], };

// ===== postcss.config.js ===== module.exports = { plugins: { tailwindcss: {}, autoprefixer: {}, }, };

// ===== package.json ===== { "name": "proservi", "version": "1.0.0", "private": true, "scripts": { "dev": "vite", "build": "vite build", "preview": "vite preview" }, "dependencies": { "firebase": "^10.7.0", "react": "^18.2.0", "react-dom": "^18.2.0", "react-router-dom": "^6.14.2" }, "devDependencies": { "autoprefixer": "^10.4.14", "postcss": "^8.4.21", "tailwindcss": "^3.3.2", "vite": "^4.4.9" } }

// ===== index.css ===== @tailwind base; @tailwind components; @tailwind utilities;

// ===== firebase.js ===== import { initializeApp } from "firebase/app"; import { getFirestore } from "firebase/firestore"; import { getAuth } from "firebase/auth";

const firebaseConfig = { apiKey: import.meta.env.VITE_API_KEY, authDomain: import.meta.env.VITE_AUTH_DOMAIN, projectId: import.meta.env.VITE_PROJECT_ID, storageBucket: import.meta.env.VITE_STORAGE_BUCKET, messagingSenderId: import.meta.env.VITE_MESSAGING_SENDER_ID, appId: import.meta.env.VITE_APP_ID };

const app = initializeApp(firebaseConfig); export const db = getFirestore(app); export const auth = getAuth(app);

// ===== App.jsx ===== import { BrowserRouter as Router, Routes, Route } from 'react-router-dom'; import Home from './pages/Home'; import Register from './pages/Register'; import ProfessionalDashboard from './pages/ProfessionalDashboard'; import Navbar from './components/Navbar';

function App() { return ( <Router> <Navbar /> <Routes> <Route path="/" element={<Home />} /> <Route path="/registro" element={<Register />} /> <Route path="/dashboard" element={<ProfessionalDashboard />} /> </Routes> </Router> ); }

export default App;

// ===== Home.jsx ===== import ServiceList from '../components/ServiceList';

export default function Home() { return ( <div className="p-4"> <h1 className="text-xl font-bold">Buscar servicios locales</h1> <ServiceList /> </div> ); }

// ===== ServiceList.jsx (resumido) ===== const services = ["Plomería", "Electricidad", "Diseño", "Fotografía"]; export default function ServiceList() { return ( <div className="grid grid-cols-2 gap-2 mt-4"> {services.map(s => <button key={s} className="p-2 bg-teal-600 text-white rounded-xl">{s}</button>)} </div> ); }

// (otros componentes como RegisterForm, ProfessionalProfile, etc., seguirán esta lógica con Firebase)

// ===== main.jsx ===== import React from 'react'; import ReactDOM from 'react-dom/client'; import App from './App'; import './index.css';

ReactDOM.createRoot(document.getElementById('root')).render( <React.StrictMode> <App /> </React.StrictMode> );

