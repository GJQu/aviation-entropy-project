## Core Learning Roadmap: Airborne Entropy

---

## 🗺️ Geospatial (GIS) Concepts

This project demands proficiency in transitioning between data types and understanding how location impacts analysis.

### 1. Data Models and Geometry
* **Vector Data:** Understanding the difference between **Points** (aircraft position), **LineStrings** (flight paths/trajectories), and **Polygons** (airspace boundaries, country outlines).
    * *Tools:* $\text{Shapely}$ and $\text{GeoPandas}$ for creating and manipulating these geometries.
* **Raster Data:** Working with grid-based data, specifically for **Weather Layers** (e.g., a grid of wind speed or precipitation).
    * *Tools:* $\text{Rasterio}$ for reading/writing and $\text{GDAL}$ (often underlying $\text{Rasterio}$) for transformation.
* **Geometry Creation from Coordinates:** Converting raw $(\text{latitude}, \text{longitude})$ pairs from the OpenSky API into $\text{Shapely}$ geometry objects for spatial analysis.

### 2. Coordinate Reference Systems (CRS) and Projections
* **WGS 84 (EPSG:4326):** The standard unprojected CRS for GPS coordinates (latitude and longitude). All raw flight data will be in this format.
* **Web Mercator (EPSG:3857):** The projection used by most web mapping services ($\text{Contextily}$, $\text{Folium}$, $\text{Deck.gl}$). Essential for visualization.
* **Reprojection:** The process of converting data from one CRS to another (e.g., $4326 \to 3857$) using the $\text{GeoPandas}$.$\text{to}\_\text{crs}()$ method. This is critical for accurate measurements and visual display.

### 3. Spatial Analysis Techniques
* **Spatial Joins:** The ability to merge two datasets based on their geographic location rather than a common attribute.
    * *Example:* Identifying which flights (LineStrings) fall within a specific airspace (Polygon).
* **Buffering:** Creating a polygon boundary around a point or line at a specified distance.
    * *Example:* Defining a region of interest around a major airport.
* **Point-in-Polygon Analysis:** Determining which points (aircraft) fall inside a defined polygon (congested airspace).
* **Raster Extraction:** Sampling a raster dataset (weather) at specific vector locations (flight path points) to assign weather attributes to the flight.

---

## 📈 Statistics and Entropy

These concepts are central to quantifying the project's core narrative: "Airborne Entropy."

### 1. Entropy (Disorder Quantification)
* **Shannon Entropy ($H$):** The core metric for this project. It measures the average level of "surprise" or uncertainty in a probability distribution.
    $$H = -\sum_{i=1}^{N} P_i \log_2 P_i$$
    * *Application:* Quantifying the disorder in the $3\text{D}$ airspace grid bins. A low value of $H$ indicates high order (flights following predictable paths); a high value indicates chaos (flights spread out unexpectedly).
* **Probability Distribution ($P_i$):** Calculating the proportion of time that a flight occupies a specific 3D grid cell.

### 2. Spatial Statistics
* **Binning and Gridding:** Dividing the continuous space (latitude, longitude, altitude) into discrete, manageable cells (the $3\text{D}$ grid) for analysis.
* **Correlation:** Measuring the statistical relationship between the calculated entropy index ($H$) and external factors like FAA delay counts, weather indices, or cancellation rates.

---

## 🤖 Machine Learning and Network Analysis

Your existing data science background will be applied here to validate and deepen the entropy metric.

### 1. Clustering (Unsupervised Learning)
* **DBSCAN (Density-Based Spatial Clustering of Applications with Noise):** An algorithm used to group points based on density.
    * *Application:* Identifying distinct, highly-trafficked flight **lanes** or **patterns** in $3\text{D}$ space.
* **HDBSCAN (Hierarchical DBSCAN):** A more robust version that doesn't require pre-setting the number of clusters.
    * *Validation:* When the system is "ordered" (low entropy), $\text{HDBSCAN}$ should find clear, strong clusters (the lanes). When it's "chaotic" (high entropy), these clusters will break down or merge, validating your entropy metric.

### 2. Network Analysis
* **Graph Theory:** Modeling the global aviation system as a **directed graph**.
    * *Nodes:* Airports ($\text{IATA}/\text{ICAO}$ codes).
    * *Edges:* Flights connecting the airports (weighted by volume, delay, or average flight time).
* **Network Metrics (using NetworkX):**
    * **Betweenness Centrality:** Identifying which airports (nodes) or routes (edges) serve as critical bridges in the network.
    * **Clustering Coefficient:** Measuring the tendency of nodes to cluster together (how interconnected a set of neighboring airports is).
    * **Degree Distribution:** Analyzing the number of connections each airport has to understand hub vs. spoke dynamics.

---

## 🎨 Visualization and Deployment

These skills turn your analysis into a compelling, professional story.

* **Interactive Web Mapping:** Using **$\text{Folium}$** for quick interactive $2\text{D}$ maps and **$\text{Deck.gl}$** (via Python wrappers) for the high-impact $3\text{D}$ visualization of flight paths and density fields.
* **Data App Frameworks:** Deploying the entire project using **$\text{Streamlit}$** to create an interactive, shareable dashboard that integrates your $2\text{D}$ maps, $3\text{D}$ visualizations, and the animated entropy timeline.
