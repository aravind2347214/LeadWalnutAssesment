# Pokémon Explorer

A responsive web application built with Next.js that allows users to browse, search, and view detailed information about Pokémon.

## Features

- Browse Pokémon with pagination
- Search Pokémon by name
- Filter Pokémon by type
- View detailed information for each Pokémon
- Fully responsive design

## Setup Instructions

1. **Prerequisites**
   - Node.js (v14 or higher)
   - npm or yarn

2. **Installation**
   ```bash
   # Clone the repository
   git clone <repository-url>

   # Navigate to the project directory
   cd pokemon-explorer

   # Install dependencies
   pnpm install
   # or
   yarn install
   # or
   npm install
   ```

3. **Running the Application**
   ```bash
   # Start the development server
   npm run dev
   # or
   yarn dev
   ```

   The application will be available at `http://localhost:3000`

## Technical Approach

### Architecture
- Built with Next.js 13+ using the App Router
- Implemented as a Client Component using the 'use client' directive
- Utilizes React hooks for state management (useState, useEffect)
- Styling done with Tailwind CSS for responsive design

### Key Implementation Details
1. **Data Fetching**
   - Uses the PokeAPI (https://pokeapi.co/)
   - Implements pagination using `limit` and `offset` query parameters
   - Fetches detailed information for each Pokémon in parallel using `Promise.all`

2. **State Management**
   ```javascript
   const [pokemon, setPokemon] = useState([]);
   const [loading, setLoading] = useState(false);
   const [error, setError] = useState(null);
   const [searchTerm, setSearchTerm] = useState('');
   const [currentPage, setCurrentPage] = useState(1);
   const [totalPages, setTotalPages] = useState(0);
   const [selectedPokemon, setSelectedPokemon] = useState(null);
   const [typeFilter, setTypeFilter] = useState('all');
   ```

3. **Filtering Logic**
   ```javascript
   const filteredPokemon = pokemon.filter(p => {
     const matchesSearch = p.name.toLowerCase().includes(searchTerm.toLowerCase());
     const matchesType = typeFilter === 'all' || p.types.some(t => t.type.name === typeFilter);
     return matchesSearch && matchesType;
   });
   ```

## Challenges and Trade-offs

   - **Challenge**: Next.js 13+ uses Server Components by default, but we needed client-side state and effects
   - **Solution**: Used the 'use client' directive to enable client-side features
   - **Trade-off**: Lost some benefits of Server Components like reduced client-side JavaScript
---
   - **Challenge**: Needed to balance between fetching enough data and performance
   - **Solution**: Implemented pagination and fetched detailed data only for visible Pokémon
   - **Trade-off**: Multiple API calls needed, but better initial load time
---
   - **Challenge**: Creating a layout that works well across all device sizes
   - **Solution**: Used Tailwind CSS with responsive breakpoints
   ```jsx
   <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
   ```
   ---
   - **Challenge**: Providing good UX during data fetching
   - **Solution**: Implemented a custom loader component
   - **Trade-off**: Added complexity, but better user experience

## Potential Improvements

1. Implement caching of Pokémon data to reduce API calls
2. Add error boundaries for more robust error handling
3. Implement keyboard navigation for better accessibility
4. Add unit tests for critical components and functions

## Dependencies

- Next.js
- React
- Tailwind CSS

## Browser Support

Tested and working on:
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
