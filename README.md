<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Internship Portfolio Showcase</title>
  <style>
    body {
      margin: 0;
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      background-color: #f9fafb;
      color: #111827;
      transition: background-color 0.3s ease, color 0.3s ease;
    }

    .dark {
      background-color: #111827;
      color: #f3f4f6;
    }

    header {
      background: white;
      padding: 1rem 2rem;
      box-shadow: 0 1px 3px rgba(0,0,0,0.1);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    header h1 {
      margin: 0;
      font-size: 1.5rem;
      color: #4f46e5;
    }

    nav {
      background: white;
      padding: 0.5rem 2rem;
      overflow-x: auto;
      white-space: nowrap;
    }

    nav button {
      margin-right: 0.5rem;
      padding: 0.5rem 1rem;
      border-radius: 9999px;
      border: none;
      cursor: pointer;
      background-color: #e5e7eb;
      color: #111827;
    }

    nav button.active {
      background-color: #4f46e5;
      color: white;
    }

    main {
      padding: 2rem;
      max-width: 1200px;
      margin: 0 auto;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 1.5rem;
    }

    .card {
      background: white;
      border-radius: 0.5rem;
      box-shadow: 0 1px 3px rgba(0,0,0,0.1);
      overflow: hidden;
      transition: transform 0.2s ease, box-shadow 0.2s ease;
    }

    .card:hover {
      transform: translateY(-4px);
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }

    .chip {
      background-color: #dbeafe;
      color: #1e40af;
      padding: 0.25rem 0.5rem;
      border-radius: 9999px;
      font-size: 0.75rem;
      display: inline-block;
      margin-bottom: 0.5rem;
    }

    .card img {
      width: 100%;
      height: 160px;
      object-fit: cover;
    }

    .card-body {
      padding: 1rem;
    }

    .card-body h2 {
      font-size: 1.25rem;
      margin: 0 0 0.5rem 0;
    }

    .card-body p {
      font-size: 0.875rem;
      color: #4b5563;
    }

    .card-body button {
      margin-top: 0.5rem;
      padding: 0.5rem 1rem;
      background-color: #4f46e5;
      color: white;
      border: none;
      border-radius: 0.375rem;
      cursor: pointer;
    }

    footer {
      text-align: center;
      padding: 2rem;
      font-size: 0.875rem;
      color: #6b7280;
    }

    .modal {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0,0,0,0.6);
      display: none;
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }

    .modal.show {
      display: flex;
    }

    .modal-content {
      background: white;
      border-radius: 0.5rem;
      padding: 2rem;
      max-width: 600px;
      width: 90%;
      position: relative;
    }

    .modal-content img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      border-radius: 0.5rem;
      margin-bottom: 1rem;
    }

    .close-btn {
      position: absolute;
      top: 1rem;
      right: 1rem;
      font-size: 1.25rem;
      cursor: pointer;
    }

    .search-bar {
      max-width: 400px;
      margin: 0 auto 1rem auto;
    }

    .search-bar input {
      width: 100%;
      padding: 0.5rem 1rem;
      border-radius: 9999px;
      border: 1px solid #d1d5db;
    }

    .dark .search-bar input {
      background: #1f2937;
      color: #f3f4f6;
      border-color: #4b5563;
    }

    .dark .card {
      background: #1f2937;
    }

    .dark .chip {
      background-color: #374151;
      color: #d1d5db;
    }

    .dark .card-body p {
      color: #d1d5db;
    }

    .dark .card-body button {
      background-color: #6366f1;
    }
  </style>
</head>
<body>
  <header class="dark:bg-gray-800">
    <div>
      <h1>🎓 Internship Portfolio Showcase</h1>
      <p>Explore amazing projects created by our talented interns</p>
    </div>
    <button id="theme-toggle" style="font-size: 1.25rem;">🌙</button>
  </header>

  <nav id="filters"></nav>

  <main>
    <div class="search-bar">
      <input type="text" id="search" placeholder="Search projects..." />
    </div>

    <div class="grid" id="project-grid"></div>
  </main>

  <footer>
    © 2025 Internship Portfolio Showcase | Created with HTML/CSS/JS
  </footer>

  <!-- Modal -->
  <div class="modal" id="project-modal">
    <div class="modal-content">
      <span class="close-btn" onclick="hideModal()">&times;</span>
      <img id="modal-image" src="" alt="">
      <h2 id="modal-title"></h2>
      <p><strong>Category:</strong> <span id="modal-category"></span></p>
      <p id="modal-description"></p>
    </div>
  </div>

  <script>
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

    const categories = ['All', ...new Set(projects.map(p => p.category))];

    const filterNav = document.getElementById('filters');
    const projectGrid = document.getElementById('project-grid');
    const modal = document.getElementById('project-modal');
    const searchInput = document.getElementById('search');

    let activeFilter = 'All';
    let darkMode = false;

    function renderFilters() {
      filterNav.innerHTML = '';
      categories.forEach(cat => {
        const btn = document.createElement('button');
        btn.textContent = cat;
        if (cat === activeFilter) btn.classList.add('active');
        btn.onclick = () => {
          activeFilter = cat;
          renderFilters();
          renderProjects();
        };
        filterNav.appendChild(btn);
      });
    }

    function renderProjects() {
      const term = searchInput.value.toLowerCase();
      projectGrid.innerHTML = '';

      projects.filter(p => {
        return (activeFilter === 'All' || p.category === activeFilter) &&
               (p.title.toLowerCase().includes(term) || p.description.toLowerCase().includes(term));
      }).forEach(project => {
        const card = document.createElement('div');
        card.className = 'card';

        card.innerHTML = `
          <img src="${project.image}" alt="${project.title}">
          <div class="card-body">
            <div class="chip">${project.category}</div>
            <h2>${project.title}</h2>
            <p>${project.description}</p>
            <button onclick="showModal('${project.title}', '${project.category}', '${project.description}', '${project.image}')">View Details</button>
          </div>
        `;
        projectGrid.appendChild(card);
      });
    }

    function showModal(title, category, description, image) {
      document.getElementById('modal-title').textContent = title;
      document.getElementById('modal-category').textContent = category;
      document.getElementById('modal-description').textContent = description;
      document.getElementById('modal-image').src = image;
      modal.classList.add('show');
    }

    function hideModal() {
      modal.classList.remove('show');
    }

    searchInput.addEventListener('input', renderProjects);

    document.getElementById('theme-toggle').addEventListener('click', () => {
      darkMode = !darkMode;
      document.body.classList.toggle('dark');
      document.getElementById('theme-toggle').textContent = darkMode ? '☀️' : '🌙';
    });

    // Init
    renderFilters();
    renderProjects();
  </script>
</body>
</html>
