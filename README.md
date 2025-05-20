import React, { useState } from 'react';

const App = () => {
  const [activeFilter, setActiveFilter] = useState('All');
  const [searchTerm, setSearchTerm] = useState('');
  const [darkMode, setDarkMode] = useState(false);
  const [selectedProject, setSelectedProject] = useState(null);

  // Mock project data
  const projects = [
    {
      title: "E-Commerce Store",
      category: "Web Development",
      description: "A full-stack e-commerce platform with shopping cart and checkout system.",
      image: "https://picsum.photos/id/1012/300/200 "
    },
    {
      title: "Weather App",
      category: "Mobile Development",
      description: "An Android app that provides real-time weather updates using OpenWeather API.",
      image: "https://picsum.photos/id/1013/300/200 "
    },
    // ... other projects ...
  ];

  // Filter logic
  const filteredProjects = projects.filter(project => {
    const matchesFilter = activeFilter === 'All' || project.category === activeFilter;
    const matchesSearch = project.title.toLowerCase().includes(searchTerm.toLowerCase()) ||
                          project.description.toLowerCase().includes(searchTerm.toLowerCase());
    return matchesFilter && matchesSearch;
  });

  return (
    <div className={`min-h-screen transition-colors duration-300 ${darkMode ? 'bg-gray-900 text-white' : 'bg-gray-50 text-gray-900'}`}>
      {/* Header */}
      <header className={`${darkMode ? 'bg-gray-800' : 'bg-white'} shadow-sm transition-colors duration-300`}>
        <div className="container mx-auto px-4 py-6 flex justify-between items-center">
          <div>
            <h1 className="text-3xl font-bold text-indigo-600">Internship Portfolio Showcase</h1>
            <p className={`mt-2 ${darkMode ? 'text-gray-300' : 'text-gray-600'}`}>Explore amazing projects created by our talented interns</p>
          </div>

          {/* Dark Mode Toggle */}
          <button
            onClick={() => setDarkMode(!darkMode)}
            className={`p-2 rounded-full focus:outline-none transition-colors ${
              darkMode ? 'bg-gray-700 text-yellow-300' : 'bg-gray-200 text-gray-700'
            }`}
            aria-label="Toggle dark mode"
          >
            {darkMode ? (
              // Sun Icon
              <svg xmlns="http://www.w3.org/2000/svg" className="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
              </svg>
            ) : (
              // Moon Icon
              <svg xmlns="http://www.w3.org/2000/svg" className="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
              </svg>
            )}
          </button>
        </div>
      </header>

      {/* Projects Grid */}
      <main className="container mx-auto px-4 py-8">
        {filteredProjects.length > 0 ? (
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            {filteredProjects.map((project, index) => (
              <div 
                key={index} 
                className={`bg-white dark:bg-gray-800 rounded-lg overflow-hidden shadow-md hover:shadow-xl transition-shadow duration-300 ${
                  darkMode ? 'bg-gray-800' : 'bg-white'
                }`}
              >
                <img 
                  src={project.image} 
                  alt={project.title} 
                  className="w-full h-48 object-cover"
                />
                <div className="p-5">
                  <span className={`inline-block px-3 py-1 rounded-full text-xs font-semibold mb-2 ${
                    darkMode 
                      ? 'bg-indigo-900 text-indigo-200' 
                      : 'bg-indigo-100 text-indigo-800'
                  }`}>
                    {project.category}
                  </span>
                  <h2 className="text-xl font-bold mb-2">{project.title}</h2>
                  <p className={`text-gray-600 mb-4 ${darkMode ? 'text-gray-300' : ''}`}>{project.description}</p>
                  <button 
                    onClick={() => setSelectedProject(project)}
                    className="mt-2 px-4 py-2 bg-indigo-600 text-white rounded hover:bg-indigo-700 transition-colors"
                  >
                    View Details
                  </button>
                </div>
              </div>
            ))}
          </div>
        ) : (
          <div className="text-center py-16">
            <svg className={`mx-auto h-12 w-12 ${darkMode ? 'text-gray-500' : 'text-gray-400'}`} fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M9.172 16.172a4 4 0 015.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
            <h3 className={`mt-2 text-lg font-medium ${darkMode ? 'text-gray-300' : 'text-gray-900'}`}>No projects found</h3>
            <p className={`mt-1 ${darkMode ? 'text-gray-400' : 'text-gray-500'}`}>Try changing your filter or search terms.</p>
          </div>
        )}
      </main>
    </div>
  );
};

export default App;
