.education-page {
  max-width: 1000px;
  margin: 40px auto;
  padding: 30px;
  background: #fffdf8;
  font-family: 'Segoe UI', sans-serif;
  border-radius: 16px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.08);
}

.education-page h1 {
  text-align: center;
  font-size: 2.5rem;
  color: #ff7a00;
  margin-bottom: 30px;
}

.filters {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  margin-bottom: 25px;
  justify-content: center;
}

.filters input,
.filters select {
  padding: 10px;
  font-size: 1rem;
  border: 1px solid #ddd;
  border-radius: 6px;
  min-width: 200px;
}

.resources {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
}

.resource-card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.06);
  padding: 20px;
  transition: 0.2s ease-in-out;
}

.resource-card:hover {
  transform: translateY(-3px);
}

.resource-card img {
  width: 100%;
  border-radius: 10px;
  margin-bottom: 10px;
}

.resource-card h2 {
  color: #ff7300;
  font-size: 1.3rem;
  margin: 10px 0 5px;
}

.resource-card p {
  font-size: 0.95rem;
  margin-bottom: 10px;
  color: #444;
}

.resource-card button {
  background-color: #ff7300;
  color: white;
  padding: 8px 14px;
  font-size: 0.95rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

.resource-card button:hover {
  background-color: #e06200;
}