# MWG-Website-
Maurice Wardana Global, Logistic and Distribution 
import React, { useState } from 'react'; import { motion } from 'framer-motion'; import { Truck, Search, Phone, Mail } from 'lucide-react';

// MauriceWardanaGlobal.jsx // Single-file React component for an interactive landing page. // Requirements: Tailwind CSS, framer-motion, lucide-react, and shadcn/ui (optional). // How to use: drop this file into your React app (e.g. src/components/MauriceWardanaGlobal.jsx) // and import it from App.jsx: import MauriceWardanaGlobal from './components/MauriceWardanaGlobal'

export default function MauriceWardanaGlobal() { // Mock tracking dataset (replace with real API in production) const mockShipments = [ { id: 'MWG123456', status: 'In Transit', eta: '2025-10-24', origin: 'Jakarta, ID', destination: 'Surabaya, ID' }, { id: 'MWG987654', status: 'Delivered', eta: '2025-10-18', origin: 'Bandung, ID', destination: 'Bali, ID' }, ];

const [trackingId, setTrackingId] = useState(''); const [trackingResult, setTrackingResult] = useState(null);

const [weight, setWeight] = useState(10); const [distance, setDistance] = useState(100); const [service, setService] = useState('regular'); const [estimate, setEstimate] = useState(null);

const [contact, setContact] = useState({ name: '', email: '', message: '' }); const [toast, setToast] = useState(null);

function handleTrack(e) { e.preventDefault(); const found = mockShipments.find(s => s.id.toLowerCase() === trackingId.trim().toLowerCase()); if (found) { setTrackingResult(found); setToast({ type: 'success', msg: Status ditemukan: ${found.status} }); } else { setTrackingResult({ id: trackingId, status: 'Not Found' }); setToast({ type: 'error', msg: 'Pengiriman tidak ditemukan. Periksa nomor pelacakan.' }); } setTimeout(() => setToast(null), 3500); }

function calcEstimate(e) { e.preventDefault(); // Simple pricing algorithm: base + weight factor + distance factor + service multiplier const base = 50; // base price const weightFactor = Math.max(1, weight / 5) * 10; const distanceFactor = Math.max(1, distance / 50) * 5; const serviceMultiplier = service === 'express' ? 1.6 : service === 'priority' ? 1.3 : 1.0; const price = Math.round((base + weightFactor + distanceFactor) * serviceMultiplier); setEstimate({ price, currency: 'IDR', breakdown: { base, weightFactor, distanceFactor, serviceMultiplier } }); }

function submitContact(e) { e.preventDefault(); // In real app: POST to backend. Here we show a fake success toast and clear form. setToast({ type: 'success', msg: 'Pesan terkirim — tim kami akan menghubungi Anda.' }); setContact({ name: '', email: '', message: '' }); setTimeout(() => setToast(null), 3500); }

return ( <div className="min-h-screen bg-gradient-to-b from-white to-slate-50 text-slate-900"> {/* Navbar */} <nav className="max-w-6xl mx-auto px-6 py-6 flex items-center justify-between"> <div className="flex items-center gap-3"> <div className="w-10 h-10 bg-slate-800 rounded-full flex items-center justify-center text-white font-bold">MW</div> <div> <div className="font-semibold">Maurice Wardana Global</div> <div className="text-xs text-slate-500">Logistik & Distribusi</div> </div> </div> <div className="flex items-center gap-6"> <a className="text-sm hover:underline" href="#services">Layanan</a> <a className="text-sm hover:underline" href="#tracking">Lacak</a> <a className="text-sm hover:underline" href="#estimate">Estimasi</a> <a className="text-sm hover:underline" href="#contact">Hubungi</a> </div> </nav>

{/* Hero */}
  <header className="max-w-6xl mx-auto px-6 py-12 grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
    <motion.div initial={{ opacity: 0, x: -30 }} animate={{ opacity: 1, x: 0 }} transition={{ duration: 0.6 }}>
      <h1 className="text-4xl md:text-5xl font-extrabold leading-tight">
        Maurice Wardana Global
        <span className="block text-indigo-600">Logistik & Distribusi — cepat, aman, dapat dipercaya</span>
      </h1>
      <p className="mt-6 text-slate-600">Solusi pengiriman darat, laut, dan udara untuk bisnis skala kecil hingga enterprise. Pelacakan real-time, estimasi tarif, dan dukungan pelanggan 24/7.</p>

      <div className="mt-6 flex gap-3">
        <a href="#estimate" className="px-5 py-3 bg-indigo-600 text-white rounded-lg shadow hover:opacity-95">Dapatkan Estimasi</a>
        <a href="#contact" className="px-5 py-3 border border-slate-200 rounded-lg">Hubungi Sales</a>
      </div>

      <div className="mt-8 grid grid-cols-3 gap-4 text-sm text-slate-600">
        <div className="p-4 bg-white rounded-lg shadow-sm">
          <div className="font-semibold">Area</div>
          <div>Indonesia & ASEAN</div>
        </div>
        <div className="p-4 bg-white rounded-lg shadow-sm">
          <div className="font-semibold">Layanan</div>
          <div>Dar, Laut, Udara</div>
        </div>
        <div className="p-4 bg-white rounded-lg shadow-sm">
          <div className="font-semibold">Support</div>
          <div>24/7</div>
        </div>
      </div>
    </motion.div>

    <motion.div className="relative" initial={{ opacity: 0, x: 30 }} animate={{ opacity: 1, x: 0 }} transition={{ duration: 0.6 }}>
      <div className="bg-gradient-to-tr from-indigo-50 to-white p-6 rounded-2xl shadow-lg">
        <div className="flex items-center gap-4">
          <Truck />
          <div>
            <div className="text-sm font-medium">Pelacakan Sekarang</div>
            <div className="text-xs text-slate-500">Masukkan nomor AWB untuk melihat status</div>
          </div>
        </div>

        <form onSubmit={handleTrack} className="mt-4 flex gap-3">
          <input value={trackingId} onChange={e => setTrackingId(e.target.value)} placeholder="Contoh: MWG123456" className="flex-1 px-4 py-2 border rounded-lg" />
          <button className="px-4 py-2 bg-indigo-600 text-white rounded-lg">Lacak</button>
        </form>

        {trackingResult && (
          <div className="mt-4 bg-white p-4 rounded-lg border">
            <div className="font-semibold">Nomor: {trackingResult.id}</div>
            <div className="text-sm">Status: <span className="font-medium">{trackingResult.status}</span></div>
            {trackingResult.eta && <div className="text-sm">ETA: {trackingResult.eta}</div>}
            {trackingResult.origin && <div className="text-sm">Asal: {trackingResult.origin}</div>}
            {trackingResult.destination && <div className="text-sm">Tujuan: {trackingResult.destination}</div>}
          </div>
        )}

        <div className="mt-4 text-xs text-slate-500">Catatan: ini adalah demo pelacakan. Hubungkan API pihak ketiga untuk data real-time.</div>
      </div>

      {/* Decorative map / card */}
      <div className="mt-6 p-6 bg-white rounded-2xl shadow-inner text-slate-500 text-sm">
        <div className="font-semibold">Keunggulan Kami</div>
        <ul className="mt-2 list-disc list-inside">
          <li>Rute optimal & integrasi TMS</li>
          <li>Asuransi kargo opsional</li>
          <li>Pelaporan & dashboard kinerja</li>
        </ul>
      </div>
    </motion.div>
  </header>

  {/* Services */}
  <section id="services" className="max-w-6xl mx-auto px-6 py-12">
    <h2 className="text-2xl font-bold">Layanan Kami</h2>
    <div className="mt-6 grid grid-cols-1 md:grid-cols-3 gap-6">
      <ServiceCard title="Pengiriman Darat" desc="Jaringan trucking nasional untuk pengiriman cepat dan aman." />
      <ServiceCard title="Pengiriman Laut" desc="Solusi FCL/LCL untuk muatan besar dan rute internasional." />
      <ServiceCard title="Pengiriman Udara" desc="Express & priority untuk kebutuhan waktu sensitif." />
    </div>
  </section>

  {/* Estimate Calculator */}
  <section id="estimate" className="max-w-6xl mx-auto px-6 py-12">
    <h2 className="text-2xl font-bold">Kalkulator Estimasi Tarif</h2>
    <p className="text-slate-600 mt-2">Masukkan berat paket, jarak, dan tipe layanan untuk melihat estimasi harga.</p>

    <div className="mt-6 grid grid-cols-1 md:grid-cols-2 gap-6">
      <form onSubmit={calcEstimate} className="bg-white p-6 rounded-lg shadow">
        <label className="block text-sm">Berat (kg)</label>
        <input type="number" value={weight} onChange={e => setWeight(Number(e.target.value))} className="w-full px-3 py-2 border rounded mt-2" />

        <label className="block text-sm mt-4">Jarak (km)</label>
        <input type="number" value={distance} onChange={e => setDistance(Number(e.target.value))} className="w-full px-3 py-2 border rounded mt-2" />

        <label className="block text-sm mt-4">Tipe Layanan</label>
        <select value={service} onChange={e => setService(e.target.value)} className="w-full px-3 py-2 border rounded mt-2">
          <option value="regular">Regular</option>
          <option value="priority">Priority</option>
          <option value="express">Express</option>
        </select>

        <div className="mt-6 flex gap-3">
          <button className="px-4 py-2 bg-indigo-600 text-white rounded">Hitung</button>
          <button type="button" className="px-4 py-2 border rounded" onClick={() => { setWeight(10); setDistance(100); setService('regular'); setEstimate(null); }}>Reset</button>
        </div>
      </form>

      <div className="bg-white p-6 rounded-lg shadow">
        <h3 className="font-semibold">Hasil Estimasi</h3>
        {!estimate ? (
          <p className="mt-3 text-slate-500">Belum ada perhitungan. Isi form di samping dan tekan "Hitung".</p>
        ) : (
          <div className="mt-3">
            <div className="text-3xl font-bold">{estimate.price.toLocaleString()} {estimate.currency}</div>
            <div className="mt-2 text-sm text-slate-600">Rincian:</div>
            <ul className="mt-2 list-disc list-inside text-sm text-slate-600">
              <li>Base: {estimate.breakdown.base}</li>
              <li>Weight factor: {Math.round(estimate.breakdown.weightFactor)}</li>
              <li>Distance factor: {Math.round(estimate.breakdown.distanceFactor)}</li>
              <li>Service multiplier: {estimate.breakdown.serviceMultiplier}x</li>
            </ul>

            <div className="mt-4">
              <a href="#contact" className="inline-block px-4 py-2 bg-indigo-600 text-white rounded">Request Quote</a>
            </div>
          </div>
        )}
      </div>
    </div>
  </section>

  {/* CTA + Contact */}
  <section id="contact" className="max-w-6xl mx-auto px-6 py-12">
    <div className="grid grid-cols-1 md:grid-cols-2 gap-6 items-start">
      <div className="bg-indigo-600 text-white p-8 rounded-lg">
        <h3 className="text-2xl font-bold">Butuh solusi logistik yang custom?</h3>
        <p className="mt-4 text-slate-100">Tim operasional kami siap membantu rencana pengiriman dan integrasi sistem.</p>

        <div className="mt-6">
          <div className="flex items-center gap-3"><Phone /> <span>+62 21 555 0123</span></div>
          <div className="flex items-center gap-3 mt-2"><Mail /> <span>sales@mauricewardana.global</span></div>
        </div>
      </div>

      <form onSubmit={submitContact} className="bg-white p-6 rounded-lg shadow">
        <h3 className="font-semibold">Kirim Pesan</h3>
        <label className="block text-sm mt-4">Nama</label>
        <input value={contact.name} onChange={e => setContact({ ...contact, name: e.target.value })} className="w-full px-3 py-2 border rounded mt-2" />

        <label className="block text-sm mt-4">Email</label>
        <input value={contact.email} onChange={e => setContact({ ...contact, email: e.target.value })} className="w-full px-3 py-2 border rounded mt-2" />

        <label className="block text-sm mt-4">Pesan</label>
        <textarea value={contact.message} onChange={e => setContact({ ...contact, message: e.target.value })} rows={4} className="w-full px-3 py-2 border rounded mt-2" />

        <div className="mt-4">
          <button className="px-4 py-2 bg-indigo-600 text-white rounded">Kirim</button>
        </div>
      </form>
    </div>
  </section>

  {/* Footer */}
  <footer className="bg-white border-t py-8">
    <div className="max-w-6xl mx-auto px-6 flex flex-col md:flex-row justify-between items-center gap-4">
      <div>
        <div className="font-semibold">Maurice Wardana Global</div>
        <div className="text-sm text-slate-500">© {new Date().getFullYear()} Maurice Wardana Global. Semua hak dilindungi.</div>
      </div>
      <div className="text-sm text-slate-500">Privacy · Terms · Sitemap</div>
    </div>
  </footer>

  {/* Toast */}
  {toast && (
    <div className={`fixed right-6 bottom-6 p-4 rounded-lg shadow-lg ${toast.type === 'success' ? 'bg-green-600 text-white' : 'bg-red-600 text-white'}`}>
      {toast.msg}
    </div>
  )}
</div>

); }

function ServiceCard({ title, desc }) { return ( <motion.div whileHover={{ y: -6 }} className="bg-white p-6 rounded-lg shadow cursor-pointer"> <div className="text-indigo-600 mb-3"><Truck /></div> <div className="font-semibold">{title}</div> <div className="mt-2 text-sm text-slate-600">{desc}</div> <div className="mt-4"> <a href="#contact" className="text-sm font-medium underline">Pelajari Lebih Lanjut</a> </div> </motion.div> ); }
