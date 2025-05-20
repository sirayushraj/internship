import streamlit as st
from streamlit_modal import Modal
import pandas as pd

# Page config
st.set_page_config(page_title="Internship Portfolio", layout="centered")

# Custom CSS for dark/light mode toggle
st.markdown("""
<style>
    .project-card {
        border: 1px solid #ccc;
        border-radius: 8px;
        padding: 10px;
        margin-bottom: 15px;
        transition: box-shadow 0.3s ease;
    }
    .project-card:hover {
        box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    .chip {
        background-color: #e0e0e0;
        color: #333;
        padding: 4px 8px;
        border-radius: 12px;
        font-size: 12px;
        display: inline-block;
        margin-bottom: 8px;
    }
    .dark .chip {
        background-color: #444;
        color: #ddd;
    }
</style>
""", unsafe_allow_html=True)

# Mock data
projects = [
    {
        "title": "E-Commerce Store",
        "category": "Web Development",
        "description": "A full-stack e-commerce platform with shopping cart and checkout system.",
        "image": "https://picsum.photos/id/1012/300/200 "
    },
    {
        "title": "Weather App",
        "category": "Mobile Development",
        "description": "An Android app that provides real-time weather updates using OpenWeather API.",
        "image": "https://picsum.photos/id/1013/300/200 "
    },
    {
        "title": "Data Dashboard",
        "category": "Data Science",
        "description": "Interactive dashboard for visualizing sales data with Plotly and Dash.",
        "image": "https://picsum.photos/id/1015/300/200 "
    },
    {
        "title": "Portfolio Website",
        "category": "Web Development",
        "description": "Personal portfolio site built with React and Tailwind CSS.",
        "image": "https://picsum.photos/id/1016/300/200 "
    },
    {
        "title": "Sentiment Analyzer",
        "category": "Machine Learning",
        "description": "Text analysis tool that detects sentiment in user input using NLP techniques.",
        "image": "https://picsum.photos/id/1018/300/200 "
    },
    {
        "title": "Task Management App",
        "category": "Mobile Development",
        "description": "Cross-platform task manager with local storage and reminders.",
        "image": "https://picsum.photos/id/1019/300/200 "
    }
]

# Unique categories
categories = ["All"] + sorted(set(p["category"] for p in projects))

# Session state for filter, search, and theme
if 'filter_category' not in st.session_state:
    st.session_state.filter_category = "All"
if 'search_term' not in st.session_state:
    st.session_state.search_term = ""
if 'dark_mode' not in st.session_state:
    st.session_state.dark_mode = False

# Modal setup
modal = Modal("Project Details", key="modal_key")

# Header
st.title("🎓 Internship Portfolio Showcase")
st.markdown("Explore amazing projects created by our talented interns.")

# Search bar
search_term = st.text_input("🔍 Search Projects...", value=st.session_state.search_term)
st.session_state.search_term = search_term

# Filter dropdown
filter_category = st.selectbox("📁 Filter by Category", options=categories, index=categories.index(st.session_state.filter_category))
st.session_state.filter_category = filter_category

# Dark Mode Toggle
dark_mode = st.checkbox("🌙 Dark Mode", value=st.session_state.dark_mode)
st.session_state.dark_mode = dark_mode

# Apply dark mode styling
if st.session_state.dark_mode:
    st.markdown('<style class="dark"></style>', unsafe_allow_html=True)

# Filter logic
def filter_projects():
    filtered = []
    for p in projects:
        matches_category = st.session_state.filter_category == "All" or p["category"] == st.session_state.filter_category
        matches_search = st.session_state.search_term.lower() in p["title"].lower() or st.session_state.search_term.lower() in p["description"].lower()
        if matches_category and matches_search:
            filtered.append(p)
    return filtered

# Display cards
for project in filter_projects():
    with st.container():
        col1, col2 = st.columns([1, 3])
        with col1:
            st.image(project["image"], width=150)
        with col2:
            st.markdown(f"<div class='chip'>{project['category']}</div>", unsafe_allow_html=True)
            st.subheader(project["title"])
            st.caption(project["description"])
            if st.button("View Details", key=f"btn_{project['title']}"):
                modal.open()

        st.markdown("---")

# Modal content
if modal.is_open():
    with modal.container():
        for p in projects:
            if f"btn_{p['title']}" in st.session_state and st.session_state[f"btn_{p['title']}"]:
                st.image(p["image"], use_column_width=True)
                st.subheader(p["title"])
                st.markdown(f"**Category:** {p['category']}")
                st.write(p["description"])
                break

# Footer
st.markdown("<hr><p style='text-align:center;'>© 2025 Internship Portfolio Showcase | Created with Streamlit</p>", unsafe_allow_html=True)
