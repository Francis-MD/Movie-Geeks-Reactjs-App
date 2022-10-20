# Movie-Geeks-Reactjs-App

## Description
Using React.js I built an application to find our favorite movies using The OMDb API.

## The Application
The following video is an example of the App functionality.

![Movie Geeks React App Giphy](https://user-images.githubusercontent.com/107253828/196825666-a09052a2-46d8-42e5-a55b-b4299dfa14ad.gif)

## The Code
```import { useState, useEffect } from 'react';

import MovieCard from './MovieCard';

import './App.css';
import SearchIcon from './search.svg';

const API_URL = 'http://www.omdbapi.com?apikey=9ad99d03';

const movie1 = {
  "Title": "Amaizing Spiderman Syndrome",
  "Year": "2012",
  "imdbID": "tt2586634",
  "Type": "movie",
  "Poster": "N/A"
}

const App = () => {

  const [movies, setMovies] = useState([]);
  const [searchTerm, setSearchTerm] = useState('');

  const searchMovies = async (tittle) => {
    const response = await fetch(`${API_URL}&s=${tittle}`)
    const data = await response.json();

    setMovies(data.Search);
  }

  useEffect(() => {
    searchMovies('Spiderman');

  }, []);

  return (
    <div className="app">
      <h1>Movie Geeks</h1>

      <div className='search'>
        <input
          placeholder="Search for movies"
          value={searchTerm}
          onChange={(e) => setSearchTerm(e.target.value)}
        />
        <img
          src={SearchIcon}
          alt="search"
          onClick={() => searchMovies(searchTerm)}
        />
      </div>

      {movies?.length > 0
        ? (
          <div className='container'>
            {movies.map((movie) => (<MovieCard movie={movie} />))}
          </div>
        ) : (
          <div className='empty'>
            <h2>No movies found</h2>
          </div>
        )}
    </div>
  );
}

export default App;
