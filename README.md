// src/component/EducationPage.tsx
import React, { useState, useEffect } from 'react';
import './EducationPage.css';

type Resource = {
  id: number;
  title: string;
  species: string;
  topic: string;
  content: string;
  imageUrl: string;
  videoUrl: string;
};

const initialResources: Resource[] = [
  {
    id: 1,
    title: 'Proper Dog Nutrition',
    species: 'Dog',
    topic: 'Nutrition',
    content: 'Dogs require a balanced diet including protein, carbs, fats, and fiber.',
    imageUrl: 'https://cdn.pixabay.com/photo/2017/09/25/13/12/dog-2785074_960_720.jpg',
    videoUrl: 'https://www.youtube.com/embed/FP2dJgxqH3g',
  },
  {
    id: 2,
    title: 'Feline Hygiene Tips',
    species: 'Cat',
    topic: 'Hygiene',
    content: 'Cats groom themselves but also need regular ear and nail checks.',
    imageUrl: 'https://cdn.pixabay.com/photo/2015/03/27/13/16/cat-694730_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/6RZ9ZClDq6c',
  },
  {
    id: 3,
    title: 'Dog First Aid Basics',
    species: 'Dog',
    topic: 'First Aid',
    content: 'Learn how to handle cuts, injuries, and CPR for dogs.',
    imageUrl: 'https://cdn.pixabay.com/photo/2018/05/07/22/04/dog-3389729_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/nr5NxjcuX5Q',
  },
];

const EducationPage: React.FC = () => {
  const [search, setSearch] = useState('');
  const [species, setSpecies] = useState('');
  const [topic, setTopic] = useState('');
  const [favorites, setFavorites] = useState<number[]>([]);

  useEffect(() => {
    const saved = localStorage.getItem('edu-favorites');
    if (saved) setFavorites(JSON.parse(saved));
  }, []);

  useEffect(() => {
    localStorage.setItem('edu-favorites', JSON.stringify(favorites));
  }, [favorites]);

  const toggleFavorite = (id: number) => {
    setFavorites(prev =>
      prev.includes(id) ? prev.filter(f => f !== id) : [...prev, id]
    );
  };

  const filteredResources = initialResources.filter(resource =>
    resource.title.toLowerCase().includes(search.toLowerCase()) &&
    (species ? resource.species === species : true) &&
    (topic ? resource.topic === topic : true)
  );

  return (
    <div className="education-page">
      <h1>Animal Healthcare Education</h1>

      <div className="filters">
        <input
          type="text"
          placeholder="Search resources..."
          value={search}
          onChange={e => setSearch(e.target.value)}
        />

        <select value={species} onChange={e => setSpecies(e.target.value)}>
          <option value="">All Species</option>
          <option value="Dog">Dog</option>
          <option value="Cat">Cat</option>
        </select>

        <select value={topic} onChange={e => setTopic(e.target.value)}>
          <option value="">All Topics</option>
          <option value="Nutrition">Nutrition</option>
          <option value="Hygiene">Hygiene</option>
          <option value="First Aid">First Aid</option>
        </select>
      </div>

      <div className="resources">
        {filteredResources.map(resource => (
          <div key={resource.id} className="resource-card">
            <img src={resource.imageUrl} alt={resource.title} />
            <h2>{resource.title}</h2>
            <p><strong>Species:</strong> {resource.species} | <strong>Topic:</strong> {resource.topic}</p>
            <p>{resource.content}</p>
            <iframe
              width="100%"
              height="215"
              src={resource.videoUrl}
              title="Instructional Video"
              frameBorder="0"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
              allowFullScreen
            />
            <button onClick={() => toggleFavorite(resource.id)}>
              {favorites.includes(resource.id) ? '★ Saved' : '☆ Save to Favorites'}
            </button>
          </div>
        ))}
      </div>
    </div>
  );
};

export default EducationPage;