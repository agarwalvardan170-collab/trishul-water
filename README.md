import React, { useState } from "react";

// IndiaTravel_AllInOne_App.jsx
// Single-file React app (Tailwind-ready) — MVP scaffold for an All-in-One India Travel site
// How to use:
// 1) Create a new React project (Vite / Create React App / Replit React template)
// 2) Add Tailwind CSS (recommended) or remove classNames and use your own CSS
// 3) Drop this file in src/App.jsx and run

const SAMPLE_CITIES = [
  {
    id: "jaipur",
    name: "Jaipur",
    cover:
      "https://images.unsplash.com/photo-1549893078-5aa5d1b6c5d2?q=80&w=1600&auto=format&fit=crop&ixlib=rb-4.0.3&s=5a8f3d1d6a3f3a0a7a6f66fd5b0d9f50",
    tagline: "Pink City — forts, palaces & food",
  },
  {
    id: "goa",
    name: "Goa",
    cover:
      "https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?q=80&w=1600&auto=format&fit=crop&ixlib=rb-4.0.3&s=6b4f6a1f7c1b9c6b9f9b9a3a2c1d2e11",
    tagline: "Beaches, nightlife & seafood",
  },
  {
    id: "varanasi",
    name: "Varanasi",
    cover:
      "https://images.unsplash.com/photo-1504328344995-4f5bde0e4a9d?q=80&w=1600&auto=format&fit=crop&ixlib=rb-4.0.3&s=2a0baf0d8f6a6c6d7e8f9b0a1c2d3e4f",
    tagline: "Ghats, spirituality & riverside life",
  },
];

const SAMPLE_HOTELS = [
  {
    id: "h1",
    city: "jaipur",
    name: "Royal Heritage Hotel",
    price: 3200,
    rating: 4.5,
    img: "https://images.unsplash.com/photo-1501117716987-c8e5f2ff5a33?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=6b82b93b0a3d6b3f6b4d2a9a2c8b7b6c",
  },
  {
    id: "h2",
    city: "goa",
    name: "Beachside Resort",
    price: 4500,
    rating: 4.3,
    img: "https://images.unsplash.com/photo-1501117716987-c8e5f2ff5a33?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=6b82b93b0a3d6b3f6b4d2a9a2c8b7b6c",
  },
];

const SAMPLE_GUIDES = [
  {
    id: "g1",
    city: "jaipur",
    name: "Amit Sharma",
    languages: ["Hindi", "English"],
    pricePerDay: 1200,
    rating: 4.8,
    verified: true,
    bio: "Local historian & storyteller — 8 years guiding experience.",
    img: "https://randomuser.me/api/portraits/men/32.jpg",
  },
  {
    id: "g2",
    city: "goa",
    name: "Leena Fernandes",
    languages: ["English", "Portuguese", "Hindi"],
    pricePerDay: 1500,
    rating: 4.6,
    verified: true,
    bio: "Food & culture specialist, leads sunrise market tours.",
    img: "https://randomuser.me/api/portraits/women/44.jpg",
  },
];

const SAMPLE_PLACES = [
  {
    id: "p1",
    city: "jaipur",
    name: "Amber Fort",
    hours: "9:00 - 17:00",
    fee: "Entry ₹100-550",
    short: "Hilltop fort with panoramic views and light shows.",
    img: "https://images.unsplash.com/photo-1549511488-6a0b3d1b7d2a?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d",
  },
  {
    id: "p2",
    city: "goa",
    name: "Baga Beach",
    hours: "24 hrs",
    fee: "Free",
    short: "Popular beach, water sports and sunset views.",
    img: "https://images.unsplash.com/photo-1507525428034-b723cf961d3e?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e",
  },
];

function Header({ onSearch }) {
  const [query, setQuery] = useState("");
  const [city, setCity] = useState("");

  function submit(e) {
    e.preventDefault();
    onSearch({ query, city });
  }

  return (
    <header className="bg-white/80 backdrop-blur-md shadow sticky top-0 z-20">
      <div className="max-w-6xl mx-auto px-4 py-4 flex items-center justify-between">
        <div className="flex items-center gap-3">
          <div className="w-10 h-10 rounded-full bg-gradient-to-tr from-indigo-500 to-pink-500 flex items-center justify-center text-white font-bold">YT</div>
          <div>
            <h1 className="text-lg font-semibold">EkSafar</h1>
            <p className="text-xs text-gray-500">One-stop travel for India</p>
          </div>
        </div>

        <form onSubmit={submit} className="flex gap-2 items-center">
          <input
            value={query}
            onChange={(e) => setQuery(e.target.value)}
            placeholder="Search places, hotels, experiences"
            className="px-3 py-2 border rounded-md w-72"
          />
          <select value={city} onChange={(e) => setCity(e.target.value)} className="px-3 py-2 border rounded-md">
            <option value="">Any city</option>
            {SAMPLE_CITIES.map((c) => (
              <option key={c.id} value={c.id}>
                {c.name}
              </option>
            ))}
          </select>
          <button className="px-4 py-2 bg-indigo-600 text-white rounded-md">Search</button>
        </form>
      </div>
    </header>
  );
}

function CityCards({ onSelect }) {
  return (
    <section className="max-w-6xl mx-auto px-4 py-8">
      <h2 className="text-2xl font-semibold mb-4">Top cities</h2>
      <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
        {SAMPLE_CITIES.map((c) => (
          <div key={c.id} className="rounded-xl shadow overflow-hidden">
            <img src={c.cover} alt={c.name} className="w-full h-40 object-cover" />
            <div className="p-4">
              <h3 className="text-lg font-semibold">{c.name}</h3>
              <p className="text-sm text-gray-500">{c.tagline}</p>
              <div className="mt-3 flex justify-between items-center">
                <button onClick={() => onSelect(c.id)} className="px-3 py-2 bg-indigo-600 text-white rounded-md">Explore</button>
                <a href="#" className="text-sm text-indigo-600">3-day plan</a>
              </div>
            </div>
          </div>
        ))}
      </div>
    </section>
  );
}

function HotelsList({ city }) {
  const hotels = SAMPLE_HOTELS.filter((h) => (!city ? true : h.city === city));
  return (
    <section className="max-w-6xl mx-auto px-4 py-8">
      <h2 className="text-2xl font-semibold mb-4">Hotels</h2>
      <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
        {hotels.map((h) => (
          <div key={h.id} className="flex gap-4 items-center p-4 border rounded-md">
            <img src={h.img} alt={h.name} className="w-32 h-20 object-cover rounded-md" />
            <div className="flex-1">
              <h3 className="font-semibold">{h.name}</h3>
              <p className="text-sm text-gray-500">₹{h.price} / night • {h.rating} ★</p>
              <div className="mt-2 flex gap-2">
                <button className="px-3 py-1 border rounded">View</button>
                <button className="px-3 py-1 bg-green-600 text-white rounded">Book</button>
              </div>
            </div>
          </div>
        ))}
      </div>
    </section>
  );
}

function GuidesList({ city, onHire }) {
  const guides = SAMPLE_GUIDES.filter((g) => (!city ? true : g.city === city));
  return (
    <section className="max-w-6xl mx-auto px-4 py-8">
      <h2 className="text-2xl font-semibold mb-4">Verified Guides</h2>
      <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
        {guides.map((g) => (
          <div key={g.id} className="p-4 border rounded-md flex gap-4 items-center">
            <img src={g.img} alt={g.name} className="w-20 h-20 rounded-full object-cover" />
            <div className="flex-1">
              <div className="flex items-center justify-between gap-2">
                <div>
                  <h3 className="font-semibold">{g.name} {g.verified && <span className="ml-2 text-xs bg-indigo-100 text-indigo-700 px-2 py-1 rounded">Verified</span>}</h3>
                  <p className="text-sm text-gray-500">{g.languages.join(", ")}</p>
                </div>
                <div className="text-right">
                  <div className="font-semibold">₹{g.pricePerDay}/day</div>
                  <div className="text-sm text-gray-500">{g.rating} ★</div>
                </div>
              </div>
              <p className="text-sm mt-2">{g.bio}</p>
              <div className="mt-3">
                <button onClick={() => onHire(g)} className="px-3 py-2 bg-indigo-600 text-white rounded-md">Hire Guide</button>
              </div>
            </div>
          </div>
        ))}
      </div>
    </section>
  );
}

function PlacesList({ city }) {
  const places = SAMPLE_PLACES.filter((p) => (!city ? true : p.city === city));
  return (
    <section className="max-w-6xl mx-auto px-4 py-8">
      <h2 className="text-2xl font-semibold mb-4">Top Places</h2>
      <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
        {places.map((p) => (
          <div key={p.id} className="rounded-md border overflow-hidden">
            <img src={p.img} alt={p.name} className="w-full h-36 object-cover" />
            <div className="p-3">
              <h3 className="font-semibold">{p.name}</h3>
              <p className="text-sm text-gray-500">{p.short}</p>
              <p className="text-xs mt-2">Hours: {p.hours} • {p.fee}</p>
            </div>
          </div>
        ))}
      </div>
    </section>
  );
}

function MiniItinerary({ itinerary, onRemove }) {
  return (
    <div className="mt-4">
      <h3 className="font-semibold">Your Itinerary</h3>
      <ul className="mt-2 space-y-2">
        {itinerary.map((it, idx) => (
          <li key={idx} className="p-2 border rounded flex justify-between items-center">
            <div>
              <div className="font-medium">Day {idx + 1}: {it.title}</div>
              <div className="text-sm text-gray-500">{it.notes}</div>
            </div>
            <div>
              <button onClick={() => onRemove(idx)} className="px-2 py-1 text-sm border rounded">Remove</button>
            </div>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default function App() {
  const [selectedCity, setSelectedCity] = useState("");
  const [searchResult, setSearchResult] = useState(null);
  const [itinerary, setItinerary] = useState([]);
  const [hiredGuide, setHiredGuide] = useState(null);

  function handleSearch(payload) {
    setSelectedCity(payload.city || "");
    setSearchResult(payload);
  }

  function addDay() {
    setItinerary((s) => [...s, { title: "Sightseeing & local food", notes: "Morning: major monument, Afternoon: local markets" }]);
  }

  function removeDay(idx) {
    setItinerary((s) => s.filter((_, i) => i !== idx));
  }

  function hireGuide(guide) {
    // Mock booking flow
    setHiredGuide(guide);
    alert(`Guide ${guide.name} hired! We sent a booking request to the guide.`);
  }

  function mockBookHotel(hotel) {
    alert(`Booked ${hotel.name} for ₹${hotel.price} / night (mock).`);
  }

  return (
    <div className="min-h-screen bg-gradient-to-b from-white to-slate-50 text-slate-800">
      <Header onSearch={handleSearch} />

      <main className="pt-6 pb-20">
        <CityCards onSelect={(id) => setSelectedCity(id)} />

        <div className="max-w-6xl mx-auto px-4">
          <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <div className="lg:col-span-2">
              <HotelsList city={selectedCity} />
              <PlacesList city={selectedCity} />
              <GuidesList city={selectedCity} onHire={hireGuide} />
            </div>

            <aside className="p-4 bg-white border rounded-md shadow">
              <h2 className="text-xl font-semibold">Planner & Safety</h2>

              <div className="mt-3">
                <p className="text-sm text-gray-600">Selected city: <strong>{selectedCity || "Any"}</strong></p>
                <div className="mt-3 flex gap-2">
                  <button onClick={addDay} className="px-3 py-2 bg-indigo-600 text-white rounded-md">Add Day</button>
                  <button onClick={() => {navigator.clipboard?.writeText(JSON.stringify({ selectedCity, itinerary }))}} className="px-3 py-2 border rounded-md">Save Plan</button>
                </div>

                <MiniItinerary itinerary={itinerary} onRemove={removeDay} />

                <div className="mt-4 border-t pt-4 text-sm">
                  <h4 className="font-semibold">Safety</h4>
                  <p className="text-gray-500 mt-2">Emergency: Local police numbers, nearest hospital, embassy details (mock).</p>
                  <div className="mt-2 flex gap-2">
                    <button className="px-3 py-2 bg-red-600 text-white rounded-md">SOS</button>
                    <button className="px-3 py-2 border rounded-md">Local Help</button>
                  </div>
                </div>

                <div className="mt-4 border-t pt-4 text-sm">
                  <h4 className="font-semibold">Hired Guide</h4>
                  {hiredGuide ? (
                    <div>
                      <p className="font-medium">{hiredGuide.name}</p>
                      <p className="text-sm text-gray-500">{hiredGuide.bio}</p>
                    </div>
                  ) : (
                    <p className="text-gray-500">No guide hired yet.</p>
                  )}
                </div>

              </div>
            </aside>
          </div>
        </div>

      </main>

      <footer className="bg-white border-t mt-8">
        <div className="max-w-6xl mx-auto px-4 py-6 text-sm text-gray-600 flex justify-between">
          <div>© {new Date().getFullYear()} EkSafar — Built with ❤️ (MVP)</div>
          <div>Made for pilots: Jaipur, Goa, Varanasi</div>
        </div>
      </footer>
    </div>
  );
}
