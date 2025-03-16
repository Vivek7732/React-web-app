# React-web-app
application
Features Implemented
✅ Home Page with Introduction & Navigation
✅ Event Listing Page with Filtering & Adding Events
✅ React Router Navigation
✅ Minimal Styling & Responsive UI
Step 1: Install Dependencies
First, set up your React project and install required packages:
npx create-react-app communion-hub-app
cd communion-hub-app
npm install react-router-dom
Step 2: Set Up Routing
Modify src/App.js to handle navigation between pages.
import React from "react";
import { BrowserRouter as Router, Routes, Route, Link } from "react-router-dom";
import Home from "./pages/Home";
import Events from "./pages/Events";

function App() {
  return (
    <Router>
      <nav style={{ padding: "10px", background: "#f4f4f4" }}>
        <Link to="/" style={{ marginRight: "10px" }}>Home</Link>
        <Link to="/events">Events</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/events" element={<Events />} />
      </Routes>
    </Router>
  );
}
Step 3: Create the Home Page
import React from "react";
import { useNavigate } from "react-router-dom";

function Home() {
  const navigate = useNavigate();

  return (
    <div style={{ textAlign: "center", padding: "20px" }}>
      <h1>Welcome to CommunionHub</h1>
      <p>Connecting people of all faiths through events and community support.</p>
      <button onClick={() => navigate("/events")} style={{ padding: "10px 20px", marginTop: "10px", cursor: "pointer" }}>
        Explore Events
      </button>
    </div>
  );
}
Step 4: Create the Event Listing Page
import React, { useState } from "react";

function Events() {
  const [events, setEvents] = useState([
    { id: 1, title: "Charity Drive", date: "2025-03-20", category: "Charity", location: "NYC" },
    { id: 2, title: "Faith Gathering", date: "2025-04-10", category: "Religious", location: "LA" },
  ]);

  const [filter, setFilter] = useState("");
  const [newEvent, setNewEvent] = useState({ title: "", date: "", category: "", location: "" });

  const handleAddEvent = () => {
    if (!newEvent.title || !newEvent.date || !newEvent.category || !newEvent.location) return;
    setEvents([...events, { id: events.length + 1, ...newEvent }]);
    setNewEvent({ title: "", date: "", category: "", location: "" });
  };

  return (
    <div style={{ padding: "20px" }}>
      <h2>Event Listing</h2>

      <label>Filter by Category: </label>
      <select onChange={(e) => setFilter(e.target.value)}>
        <option value="">All</option>
        <option value="Religious">Religious</option>
        <option value="Social">Social</option>
        <option value="Charity">Charity</option>
      </select>

      <ul>
        {events
          .filter((event) => (filter ? event.category === filter : true))
          .map((event) => (
            <li key={event.id}>
              <strong>{event.title}</strong> - {event.date} ({event.category}) @ {event.location}
            </li>
          ))}
      </ul>

      <h3>Add New Event</h3>
      <input type="text" placeholder="Title" value={newEvent.title} onChange={(e) => setNewEvent({ ...newEvent, title: e.target.value })} />
      <input type="date" value={newEvent.date} onChange={(e) => setNewEvent({ ...newEvent, date: e.target.value })} />
      <input type="text" placeholder="Category" value={newEvent.category} onChange={(e) => setNewEvent({ ...newEvent, category: e.target.value })} />
      <input type="text" placeholder="Location" value={newEvent.location} onChange={(e) => setNewEvent({ ...newEvent, location: e.target.value })} />
      <button onClick={handleAddEvent}>Add Event</button>
    </div>
  );
}

export default Events;

