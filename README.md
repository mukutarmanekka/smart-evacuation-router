# Smart Evacuation Router 🚨

A sophisticated web application that helps plan optimal evacuation routes during emergency situations. The system uses real-world road network data and advanced pathfinding algorithms to find safe evacuation paths while avoiding obstacles like water bodies and following road constraints.

## Features

### 🗺️ Interactive Map Interface
- Real-time interactive map powered by Folium
- Multiple map tile layers (OpenStreetMap, Light, Dark themes)
- Visual representation of disaster zones, people locations, and evacuation routes

### 🚨 Disaster Zone Management
- Click-to-place disaster markers with customizable impact radius
- Visual representation of danger zones with colored circles
- Support for multiple disaster scenarios

### 👥 Person Management
- Add people at specific coordinates
- Automatic classification of people as "safe" or "in danger zone"
- Real-time status updates based on disaster zone proximity

### 🛣️ Smart Routing Algorithm
- Custom A* pathfinding algorithm optimized for emergency evacuation
- **Key Constraints:**
  - Routes must lead from person's location to outside the disaster zone
  - Must follow existing road networks (uses OpenStreetMap data)
  - Completely avoids water bodies (rivers, lakes, coastlines)
  - Finds shortest safe path to exit the danger zone
  - Prioritizes major roads when available

### 🌍 Global Support
- Custom coordinate input for any global location
- Real-time road network data fetching using OSMnx

## Installation

### Prerequisites
- Python 3.8 or higher
- Internet connection (required for fetching map data)

### Setup Instructions

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd smart-evacuation-router
   ```

2. **Create a virtual environment (recommended):**
   ```bash
   python -m venv evacuation_env
   evacuation_env\Scripts\activate.bat  
   ```

3. **Install required dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application:**
   ```bash
   streamlit run app.py
   ```

5. **Access the application:**
   Open your web browser and navigate to `http://localhost:8501`

## Usage Guide

### Getting Started
1. **Set Disaster Zone:** Use the form to place a disaster marker with specified radius
2. **Add People:** Place people markers at various locations
3. **View Routes:** The system automatically calculates and displays evacuation routes for people in danger zones

### Interface Components

#### Sidebar Controls
- **Location Selection:** Dropdown for major cities or custom coordinate input
- **Disaster Settings:** Adjustable impact radius (100m - 5000m)
- **Reset Options:** Clear disaster zones, people, or all data

#### Main Interface
- **Disaster Zone Form:** Input coordinates to place disaster markers
- **Person Addition Form:** Add people at specific locations
- **Interactive Map:** Visual representation of all elements and routes

#### Route Information
- **Statistics Dashboard:** Shows total people, those in danger, and safe individuals
- **Route Details:** Information about evacuation paths including distance estimates

## Technical Architecture

### Core Components

#### 1. Main Application (`app.py`)
- Streamlit web interface
- Session state management
- User interaction handling
- Map rendering and updates

#### 2. Evacuation Algorithm (`evacuation_algorithm.py`)
- Custom A* pathfinding implementation
- Heuristic functions optimized for emergency scenarios
- Water avoidance and road network following
- Exit node identification and prioritization

#### 3. Data Processing (`data_processing.py`)
- OpenStreetMap data integration
- Coordinate system conversions
- Distance calculations using Haversine formula
- Road network filtering and processing

#### 4. Map Utilities (`map_utils.py`)
- Folium map creation and styling
- Marker placement and customization
- Route visualization with directional arrows
- Interactive map elements

### Algorithm Details

The evacuation routing uses a modified A* algorithm with these key features:

1. **Heuristic Function:** Prioritizes movement toward disaster zone exits
2. **Cost Function:** Heavily penalizes water crossings (10,000x penalty)
3. **Constraint Satisfaction:** Ensures routes follow road networks
4. **Exit Node Detection:** Identifies optimal exit points just outside danger zones
5. **Multi-objective Optimization:** Balances shortest path with safety constraints

### Data Sources
- **Road Networks:** OpenStreetMap via OSMnx library
- **Geographic Data:** Real-time fetching of street networks
- **Coordinate Systems:** WGS84 (latitude/longitude)

## Configuration

### Customizable Parameters
- **Disaster Radius:** 100m to 5000m (adjustable in sidebar)
- **Buffer Distance:** 100m around disaster zone for exit node detection
- **Maximum Exit Nodes:** Up to 10 exit points considered per disaster zone
- **Route Colors:** Predefined color palette for route visualization

### Performance Settings
- **Network Distance:** Automatically adjusts based on disaster radius
- **Node Filtering:** Removes water-based nodes for better performance
- **Caching:** Session state preserves data during user session

## Dependencies

```
streamlit          # Web application framework
folium            # Interactive map visualization
networkx          # Graph algorithms and network analysis
numpy             # Numerical computations
matplotlib        # Plotting and visualization
osmnx             # OpenStreetMap data processing
streamlit-folium  # Folium integration with Streamlit
```

## File Structure

```
smart-evacuation-router/
│
├── app.py                    # Main Streamlit application
├── evacuation_algorithm.py   # A* pathfinding implementation
├── data_processing.py        # Data handling and processing
├── map_utils.py             # Map visualization utilities
├── requirements.txt         # Python dependencies
├── README.md               # Project documentation
└── Untitled.ipynb         # Development notebook
```

## Use Cases

### Emergency Planning
- **Emergency Services:** Route planning for evacuation procedures
- **Urban Planning:** Infrastructure assessment for emergency preparedness
- **Educational:** Teaching pathfinding algorithms and emergency management

### Research Applications
- **Algorithm Development:** Testing pathfinding algorithms in real scenarios
- **Network Analysis:** Studying road network connectivity and resilience
- **Disaster Preparedness:** Analyzing evacuation capacity and bottlenecks

## Limitations and Considerations

### Current Limitations
- **Real-time Data:** Uses static road network data (not live traffic)
- **Disaster Types:** Generic circular disaster zones (not hazard-specific)
- **Capacity Planning:** Doesn't account for road capacity or congestion
- **Dynamic Obstacles:** No real-time obstacle detection

### Performance Notes
- **Initial Load:** First map load may take 30-60 seconds for data fetching
- **Network Dependency:** Requires internet connection for OpenStreetMap data
- **Memory Usage:** Large road networks may require significant RAM

## Contributing

### Development Setup
1. Fork the repository
2. Create a feature branch
3. Make changes and test thoroughly
4. Submit a pull request with detailed description

### Areas for Improvement
- **Real-time Data Integration:** Live traffic and road closure data
- **Advanced Disaster Modeling:** Specific hazard types and spread patterns
- **Multi-modal Transportation:** Support for pedestrian, bicycle, and public transit
- **Optimization Algorithms:** Additional routing algorithms and comparisons
- **Mobile Responsiveness:** Enhanced mobile device support

## License

This project is open source and available under the MIT License.

## Support

For issues, questions, or contributions, please:
1. Check existing documentation
2. Search for similar issues
3. Create detailed bug reports or feature requests
4. Include system information and steps to reproduce

## Acknowledgments

- **OpenStreetMap:** For providing comprehensive global map data
- **OSMnx Library:** For excellent OpenStreetMap integration
- **Streamlit:** For the user-friendly web framework
- **Folium:** For interactive map visualization capabilities

---

**Note:** This application is designed for educational and planning purposes. In real emergency situations, always follow official evacuation procedures and emergency services guidance.
