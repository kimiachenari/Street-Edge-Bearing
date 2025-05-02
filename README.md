# 🛣️ **Street Edge Bearing Visualization Using OSMnx** 🛣️

This project visualizes the **edge bearings** of the street network in **Mashhad, Iran** using the **OSMnx** library. Edge bearings represent the orientation of the street segments in the network and are useful for understanding the geometric layout of streets in urban areas. This project creates both a histogram and a polar plot of street orientations.

For more information about **OSMnx**, visit [OSMnx GitHub](https://github.com/gboeing/osmnx).

---

## 🚀 **Key Features**

- **Edge Bearing Calculation**: Uses the **OSMnx** library to calculate the bearings (angles) of street edges.
- **Histogram Plot**: Visualizes the distribution of edge bearings using a histogram.
- **Polar Plot**: Provides a **polar plot** to visually represent the distribution of street orientations in the network.
- **Data from OpenStreetMap**: Extracts data from **OpenStreetMap** for **Mashhad, Iran**, providing real-world urban network information.
- **Custom Visualization**: Offers custom plotting with **Matplotlib** and **NumPy**, showcasing the edge orientations in a street network.

---

## 🧑‍🔬 **Getting Started**

### 1. **Install Required Libraries**

Ensure that you have the following libraries installed:

```bash
pip install osmnx pandas matplotlib numpy
```

### 2. **Run the Script**

1. **Set the Region**: The script is currently set to analyze **District 1, Mashhad, Iran**. You can modify the `graph_from_place()` function to analyze different areas.
2. **Execute the Script**: Run the script to calculate the **edge bearings** and generate visualizations for the street network.

---

## 🔧 **How It Works**

### 1. **Import Libraries**

The script imports the required libraries such as **OSMnx**, **Pandas**, **Matplotlib**, and **NumPy** for data processing and visualization:

```python
import csv 
import osmnx as ox
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
```

### 2. **Fetch Street Network Data**

The street network for **District 1, Mashhad, Iran** is fetched from **OpenStreetMap** using the **OSMnx** library. The edge bearings are added to the graph using the `add_edge_bearings()` function:

```python
ox.config(use_cache=True, log_console=True)
G = ox.graph_from_place('District 1, Mashhad, Iran', network_type='drive')
G = ox.add_edge_bearings(G)
```

### 3. **Convert Graph to GeoDataFrame**

The graph is converted to **GeoDataFrames** for easier manipulation, and the data is stored in a **Pandas DataFrame** for further analysis:

```python
gdf_edges = ox.graph_to_gdfs(G, nodes=True)
df = pd.DataFrame(gdf_edges)
```

### 4. **Visualize Edge Bearings with a Histogram**

A **histogram** is created to visualize the distribution of the edge bearings in the network. The bins are set to show the frequencies of the bearings:

```python
bearings = df['bearing']
ax = bearings.hist(bins=30, zorder=2, alpha=0.8)
xlim = ax.set_xlim(0, 360)
ax.set_title('Network Edge Bearings of (District1, Mashhad, Iran)')
plt.show()
```

### 5. **Polar Plot of Edge Bearings**

A **polar plot** is generated to display the edge bearings in a circular format. This gives a more intuitive view of the orientation of streets in the network:

```python
n = 30
count, division = np.histogram(bearings, bins=[ang*360/n for ang in range(0,n+1)])
division = division[0:-1]
width =  2 * np.pi/n
ax = plt.subplot(111, projection='polar')
ax.set_theta_zero_location('N')
ax.set_theta_direction('clockwise')
bars = ax.bar(division * np.pi/180 - width * 0.5 , count, width=width, bottom=0.0)
ax.set_title('Network Edge Bearings of (District1, Mashhad, Iran)', y=1.1 )
plt.show()
```

### 6. **Output and Display**

Both the **histogram** and **polar plot** are displayed using **Matplotlib**'s plotting functions. These visualizations help understand the distribution and orientation of streets in the urban network.

---

## 📊 **Outputs**

- **Histogram Plot**: Displays the distribution of street edge bearings in **District 1, Mashhad**, represented by a histogram.
- **Polar Plot**: A **polar plot** showing the frequency of street orientations, giving an intuitive understanding of the street network's directional distribution.

---
![download2222](https://github.com/user-attachments/assets/2a1c5b7f-525c-4112-85f4-c837abfe6475)
![download (2)](https://github.com/user-attachments/assets/7e314cf0-aa56-4563-9c88-d6c1e673a7cc)

## 📈 **Future Enhancements**

- **Interactive Plots**: Add **interactive visualization** using libraries like **Plotly** or **Bokeh** to explore the street orientations interactively.
- **Detailed Analysis**: Incorporate other **network centrality measures** and visualize them along with edge bearings to gain more insights into the street network's efficiency.
- **Comparative Analysis**: Extend the analysis to multiple regions or cities to compare street orientations and their relation to urban layouts.

---

