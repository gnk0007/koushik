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
    content: 'Dogs need a protein-rich diet with balanced carbs and fats. Avoid chocolate and onions.',
    imageUrl: 'https://cdn.pixabay.com/photo/2017/09/25/13/12/dog-2785074_960_720.jpg',
    videoUrl: 'https://www.youtube.com/embed/FP2dJgxqH3g',
  },
  {
    id: 2,
    title: 'Feline Hygiene Tips',
    species: 'Cat',
    topic: 'Hygiene',
    content: 'Cats clean themselves, but check ears, nails and litter hygiene regularly.',
    imageUrl: 'https://cdn.pixabay.com/photo/2015/03/27/13/16/cat-694730_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/6RZ9ZClDq6c',
  },
  {
    id: 3,
    title: 'Rabbit Grooming & Diet',
    species: 'Rabbit',
    topic: 'Grooming',
    content: 'Brush your rabbit’s coat and provide plenty of hay and leafy greens.',
    imageUrl: 'https://cdn.pixabay.com/photo/2018/04/01/20/12/easter-3281583_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/98LOsaVG0xA',
  },
  {
    id: 4,
    title: 'Guinea-Pig First Aid',
    species: 'Guinea Pig',
    topic: 'First Aid',
    content: 'Clean wounds gently, isolate sick pigs, and visit a vet for respiratory issues.',
    imageUrl: 'https://cdn.pixabay.com/photo/2017/07/30/20/37/guinea-pig-2551308_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/98nEGyyYAm4',
  },
  {
    id: 5,
    title: 'Training a Parrot to Talk',
    species: 'Parrot',
    topic: 'Training',
    content: 'Use repetition and positive reinforcement to teach parrots simple phrases.',
    imageUrl: 'https://cdn.pixabay.com/photo/2021/05/20/16/39/parrot-6268524_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/SRijXBCQ0CM',
  },
  {
    id: 6,
    title: 'Cleaning Your Fish Tank',
    species: 'Fish',
    topic: 'Hygiene',
    content: 'Change 25 % of the water weekly. Monitor pH, nitrate, and temperature.',
    imageUrl: 'https://cdn.pixabay.com/photo/2016/10/12/20/12/fish-1736486_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/_5uV2tG6rjA',
  },
  {
    id: 7,
    title: 'Turtle Habitat Setup',
    species: 'Turtle',
    topic: 'Habitat',
    content: 'Turtles need a basking spot, clean water, and UVB lighting in their tank.',
    imageUrl: 'https://cdn.pixabay.com/photo/2016/10/12/20/13/turtle-1736489_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/TGpD0xhVgyY',
  },
  {
    id: 8,
    title: 'Hamster Wheel Safety',
    species: 'Hamster',
    topic: 'Exercise',
    content: 'Use solid wheels to avoid foot injuries. Let them explore daily.',
    imageUrl: 'https://cdn.pixabay.com/photo/2018/07/26/16/31/hamster-3561454_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/KUu0iY2uuy4',
  },
  {
    id: 9,
    title: 'Ferret Vaccination Schedule',
    species: 'Ferret',
    topic: 'Vaccination',
    content: 'Vaccinate against canine distemper annually and rabies if required.',
    imageUrl: 'https://cdn.pixabay.com/photo/2015/04/19/08/32/ferret-729932_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/NrZd5hNrc-c',
  },
  {
    id: 10,
    title: 'Horse Hoof Care Basics',
    species: 'Horse',
    topic: 'Grooming',
    content: 'Clean hooves daily and trim regularly to prevent lameness.',
    imageUrl: 'https://cdn.pixabay.com/photo/2017/01/20/00/30/horse-1999117_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/xZoYZyGXr1w',
  },
  {
    id: 11,
    title: 'Budgie Mental Stimulation',
    species: 'Budgie',
    topic: 'Enrichment',
    content: 'Rotate toys weekly, provide foraging puzzles and daily interaction.',
    imageUrl: 'https://cdn.pixabay.com/photo/2022/03/06/17/11/budgie-7050457_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/D8nN5dAOm4Q',
  },
  {
    id: 12,
    title: 'Reptile Heating & Lighting',
    species: 'Lizard',
    topic: 'Habitat',
    content: 'Use basking lamps and UVB lights. Keep a temperature gradient.',
    imageUrl: 'https://cdn.pixabay.com/photo/2016/06/19/07/38/chameleon-1465586_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/kCC_OO9hP1c',
  },
  {
    id: 13,
    title: 'Canary Singing & Health',
    species: 'Canary',
    topic: 'Behavior',
    content: 'Healthy canaries sing often. Silence can be a sign of illness or stress.',
    imageUrl: 'https://cdn.pixabay.com/photo/2021/03/02/13/33/canary-6062893_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/A2yAZEpZ4dc',
  },
  {
    id: 14,
    title: 'Gerbil Housing Tips',
    species: 'Gerbil',
    topic: 'Habitat',
    content: 'Gerbils need deep bedding, tunnels, and chewing toys to stay happy.',
    imageUrl: 'https://cdn.pixabay.com/photo/2018/04/07/19/39/gerbil-3297338_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/AN4dYVZXZcY',
  },
  {
    id: 15,
    title: 'Lovebird Bonding Tips',
    species: 'Lovebird',
    topic: 'Training',
    content: 'Use treats and consistent handling. Avoid forcing interaction.',
    imageUrl: 'https://cdn.pixabay.com/photo/2019/09/15/17/53/birds-4477796_1280.jpg',
    videoUrl: 'https://www.youtube.com/embed/FU9-T_pEmPM',
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

  const filteredResources = initialResources.filter(res =>
    res.title.toLowerCase().includes(search.toLowerCase()) &&
    (species ? res.species === species : true) &&
    (topic ? res.topic === topic : true)
  );

  return (
    <div className="education-page">
      <h1>Animal Healthcare Resources</h1>

      <div className="filters">
        <input
          type="text"
          placeholder="Search resources..."
          value={search}
          onChange={e => setSearch(e.target.value)}
        />

        <select value={species} onChange={e => setSpecies(e.target.value)}>
          <option value="">All Species</option>
          {Array.from(new Set(initialResources.map(r => r.species))).map(s => (
            <option key={s} value={s}>{s}</option>
          ))}
        </select>

        <select value={topic} onChange={e => setTopic(e.target.value)}>
          <option value="">All Topics</option>
          {Array.from(new Set(initialResources.map(r => r.topic))).map(t => (
            <option key={t} value={t}>{t}</option>
          ))}
        </select>
      </div>

      <div className="resources">
        {filteredResources.map(r => (
          <div key={r.id} className="resource-card">
            <img src={r.imageUrl} alt={r.title} />
            <h2>{r.title}</h2>
            <p>
              <strong>Species:</strong> {r.species} |
              <strong> Topic:</strong> {r.topic}
            </p>
            <p>{r.content}</p>
            <iframe
              width="100%"
              height="215"
              src={r.videoUrl}
              title="Instructional Video"
              frameBorder="0"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
              allowFullScreen
            />
            <button onClick={() => toggleFavorite(r.id)}>
              {favorites.includes(r.id) ? '★ Saved' : '☆ Save to Favorites'}
            </button>
          </div>
        ))}
      </div>
    </div>
  );
};

export default EducationPage;