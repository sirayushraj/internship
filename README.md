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
    {
      title: "Data Dashboard",
      category: "Data Science",
      description: "Interactive dashboard for visualizing sales data with Plotly and Dash.",
      image: "https://picsum.photos/id/1015/300/200 "
    },
    {
      title: "Portfolio Website",
      category: "Web Development",
      description: "Personal portfolio site built with React and Tailwind CSS.",
      image: "https://picsum.photos/id/1016/300/200 "
    },
    {
      title: "Sentiment Analyzer",
      category: "Machine Learning",
      description: "Text analysis tool that detects sentiment in user input using NLP techniques.",
      image: "https://picsum.photos/id/1018/300/200 "
    },
    {
      title: "Task Management App",
      category: "Mobile Development",
      description: "Cross-platform task manager with local storage and reminders.",
      image: "https://picsum.photos/id/1019/300/200 "
    }
  ];

  // Get unique categories for filtering
  const categories = ['All', ...new Set(projects.map(project => project.category))];

  // Filter and search logic
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

        {/* Search Bar */}
        <div className="container mx-auto px-4 pb-6 max-w-md">
          <input
            type="text"
            placeholder="Search projects..."
            value={searchTerm}
            onChange={(e) => setSearchTerm(e.target.value)}
            className={`w-full px-4 py-2 rounded-lg border focus:outline-none focus:ring-2 focus:ring-indigo-500 transition-colors ${
              darkMode 
                ? 'bg-gray-700 border-gray-600 text-white focus:ring-yellow-400' 
                : 'bg-white border-gray-300 text-gray-900 focus:ring-indigo-500'
            }`}
          />
        </div>
      </header>

      {/* Filters */}
      <nav className={`${darkMode ? 'bg-gray-800' : 'bg-white'} py-4 shadow-sm sticky top-0 z-10 transition-colors duration-300`}>
        <div className="container mx-auto px-4 overflow-x-auto">
          <div className="flex space-x-2">
            {categories.map((category) => (
              <button
                key={category}
                onClick={() => setActiveFilter(category)}
                className={`px-4 py-2 rounded-full transition-all duration-300 ${
                  activeFilter === category 
                    ? 'bg-indigo-600 text-white' 
                    : darkMode
                      ? 'bg-gray-700 text-gray-200 hover:bg-gray-600'
                      : 'bg-gray-200 text-gray-700 hover:bg-gray-300'
                }`}
              >
                {category}
              </button>
            ))}
          </div>
        </div>
      </nav>

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

      {/* Modal */}
      {selectedProject && (
        <div className="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50 p-4 transition-opacity duration-300">
          <div className={`bg-white dark:bg-gray-800 rounded-lg p-6 w-full max-w-3xl max-h-screen overflow-y-auto transition-colors duration-300 ${
            darkMode ? 'bg-gray-800 text-white' : 'bg-white text-gray-900'
          }`}>
            <img src={selectedProject.image} alt={selectedProject.title} className="w-full h-64 object-cover rounded mb-4" />
            <h2 className="text-3xl font-bold mb-2">{selectedProject.title}</h2>
            <p className={`text-sm mb-4 ${darkMode ? 'text-gray-300' : 'text-gray-600'}`}>
              Category: <strong>{selectedProject.category}</strong>
            </p>
            <p className="mb-6">{selectedProject.description}</p>
            <button 
              onClick={() => setSelectedProject(null)}
              className="px-4 py-2 bg-indigo-600 text-white rounded hover:bg-indigo-700 transition-colors"
            >
              Close
            </button>
          </div>
        </div>
      )}

      {/* Footer */}
      <footer className={`${darkMode ? 'bg-gray-800 border-gray-700 text-gray-300' : 'bg-white border-gray-200 text-gray-600'} border-t mt-auto transition-colors duration-300`}>
        <div className="container mx-auto px-4 py-6">
          <p className="text-center">
            © 2025 Internship Portfolio Showcase | Created with React & Tailwind CSS
          </p>
        </div>
      </footer>
    </div>
  );
};

export default App;
