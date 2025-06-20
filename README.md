// CRM ระบบพื้นฐานด้วย React + Tailwind + Firebase (v9 modular)
// ไฟล์นี้เป็นตัวอย่างโค้ดหลักที่สามารถนำไปแยกเป็น Component ได้ภายหลัง
// ต้องติดตั้ง Firebase และตั้งค่าก่อนใช้งานจริง

import { useState, useEffect } from "react";
import { initializeApp } from "firebase/app";
import {
  getAuth,
  createUserWithEmailAndPassword,
  signInWithEmailAndPassword,
  onAuthStateChanged,
} from "firebase/auth";
import {
  getFirestore,
  collection,
  addDoc,
  query,
  where,
  getDocs,
} from "firebase/firestore";

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_STORAGE_BUCKET",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID",
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

export default function CRMApp() {
  const [user, setUser] = useState(null);
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [caseData, setCaseData] = useState({
    trackingNumber: "",
    courier: "",
    topic: "ประสานงาน 1",
    detail: "",
    status: "รอติดตาม",
  });
  const [cases, setCases] = useState([]);

  useEffect(() => {
    onAuthStateChanged(auth, (currentUser) => {
      setUser(currentUser);
      if (currentUser) loadCases(currentUser.email);
    });
  }, []);

  const register = async () => {
    await createUserWithEmailAndPassword(auth, email, password);
  };

  const login = async () => {
    await signInWithEmailAndPassword(auth, email, password);
  };

  const handleSubmit = async () => {
    const doc = {
      admin: user.email,
      timestamp: new Date(),
      ...caseData,
    };
    await addDoc(collection(db, "cases"), doc);
    setCaseData({ trackingNumber: "", courier: "", topic: "ประสานงาน 1", detail: "", status: "รอติดตาม" });
    loadCases(user.email);
  };

  const loadCases = async (adminEmail) => {
    const q = query(collection(db, "cases"), where("admin", "==", adminEmail));
    const snapshot = await getDocs(q);
    const data = snapshot.docs.map((doc) => ({ id: doc.id, ...doc.data() }));
    setCases(data);
  };

  if (!user) {
    return (
      <div className="p-4 max-w-md mx-auto">
        <h1 className="text-xl font-bold mb-4">Login / Register</h1>
        <input
          type="email"
          className="border p-2 w-full mb-2"
          placeholder="Email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
        />
        <input
          type="password"
          className="border p-2 w-full mb-2"
          placeholder="Password"
          value={password}
          onChange={(e) => setPassword(e.target.value)}
        />
        <div className="flex gap-2">
          <button className="bg-blue-500 text-white px-4 py-2" onClick={login}>Login</button>
          <button className="bg-green-500 text-white px-4 py-2" onClick={register}>Register</button>
        </div>
      </div>
    );
  }

  return (
    <div className="p-4 max-w-3xl mx-auto">
      <h1 className="text-2xl font-bold mb-4">ระบบแจ้งเคส</h1>
      <div className="mb-4">
        <input
          type="text"
          className="border p-2 w-full mb-2"
          placeholder="เลขพัสดุ"
          value={caseData.trackingNumber}
          onChange={(e) => setCaseData({ ...caseData, trackingNumber: e.target.value })}
        />
        <input
          type="text"
          className="border p-2 w-full mb-2"
          placeholder="บริษัทขนส่ง"
          value={caseData.courier}
          onChange={(e) => setCaseData({ ...caseData, courier: e.target.value })}
        />
        <select
          className="border p-2 w-full mb-2"
          value={caseData.topic}
          onChange={(e) => setCaseData({ ...caseData, topic: e.target.value })}
        >
          <option>ประสานงาน 1</option>
          <option>ประสานงาน 2</option>
          <option>ประสานงาน 3</option>
        </select>
        <textarea
          className="border p-2 w-full mb-2"
          placeholder="รายละเอียด"
          value={caseData.detail}
          onChange={(e) => setCaseData({ ...caseData, detail: e.target.value })}
        ></textarea>
        <select
          className="border p-2 w-full mb-2"
          value={caseData.status}
          onChange={(e) => setCaseData({ ...caseData, status: e.target.value })}
        >
          <option>รอติดตาม</option>
          <option>ติดตามซ้ำ</option>
          <option>เสร็จแล้ว</option>
        </select>
        <button className="bg-blue-600 text-white px-4 py-2" onClick={handleSubmit}>บันทึก</button>
      </div>

      <h2 className="text-lg font-semibold mb-2">รายการเคสของคุณ</h2>
      <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
        {['รอติดตาม', 'ติดตามซ้ำ', 'เสร็จแล้ว'].map((status) => (
          <div key={status} className="border p-3 rounded">
            <h3 className="font-bold text-center mb-2">{status}</h3>
            {cases.filter(c => c.status === status).map((c) => (
              <div key={c.id} className="mb-2 text-sm">
                <div><b>พัสดุ:</b> {c.trackingNumber}</div>
                <div><b>หัวข้อ:</b> {c.topic}</div>
                <div><b>เวลา:</b> {new Date(c.timestamp.seconds * 1000).toLocaleString()}</div>
                <div><b>รายละเอียด:</b> {c.detail}</div>
              </div>
            ))}
          </div>
        ))}
      </div>
    </div>
  );
}

