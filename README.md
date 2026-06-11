# Wildlife Conservation Using Drones — GIS & AI Research

A research presentation examining how GIS spatial analysis and UAV drones can be used to predict and prevent elephant poaching. The project studies 156 known poaching incidents in the Tsavo region of Kenya (8,150 sq miles) and models how drone surveillance, risk mapping, and strategic ranger deployment can protect at-risk wildlife.

The analysis is based on the The Pennsylvania State University research paper "Predicting and Preventing Elephant Poaching Incidents through Statistical Analysis, GIS-Based Risk Analysis, and Aerial Surveillance Flight Path Modeling" (Shaffer & Bishop). The team applied ESRI ArcGIS with the Spatial Analyst Extension, R-STAT for point pattern analysis, and GeoDa for spatial autocorrelation. The pipeline constructs a GIS risk map by correlating 156 poaching incident locations with physical features (roads, water sources, land cover types), models drone flight paths from camera FOV and battery constraints using ArduPilot Mega Planner, and calculates optimal ranger station placement via travel-cost surfaces.

**[Live Demo →](https://halkhoori2000.github.io/Wildlife-Conservation-Using-Drones/)**

---

## Use Cases
- Anti-poaching operations: the same GIS risk-mapping approach (correlating incident locations with terrain features) is used by conservation organisations in Africa and Asia to direct ranger patrols toward statistically high-risk zones
- Wildlife reserve management: drone flight path modelling from camera FOV and battery limits applies directly to planning systematic aerial surveys for wildlife census or habitat monitoring
- Disaster response and search-and-rescue: the travel-cost surface method for optimising ranger station placement is the same technique used in emergency services for ambulance depot siting and SAR team positioning
- Environmental policy and land use: GIS spatial autocorrelation analysis (used here to identify poaching clustering patterns) is a standard tool in environmental impact assessment and conservation planning

## Challenges
- **Stochastic vs. deterministic process validation**: before any predictive model can be built from the 156 poaching incident points, it must be confirmed that the distribution is not random — 100 Monte Carlo simulations were run to rule out a stochastic process; only a deterministic pattern permits predictive risk modelling
- **Multi-layer GIS correlation**: roads, water sources, and land cover each contribute independently to poaching risk — combining them into a single composite risk surface requires assigning defensible weights to each factor, and the weighting choices directly affect which areas are flagged as high-risk
- **Drone coverage vs. battery constraint trade-off**: the flight path model must balance camera FOV (wider angle = more area per pass but lower resolution) against cruising altitude, speed, and battery life — optimising for coverage area while maintaining enough image quality to detect poachers
- **Travel-cost surface accuracy**: ranger response time depends on terrain — roads are fast, dense forest and rivers are slow; accurately parameterising the resistance of each land cover type is critical for the station placement model to produce realistic deployment recommendations

---

## Methodology

```
156 Poaching Incidents (Tsavo, Kenya)
        │
        ▼
 Point Pattern Analysis  ←  R-STAT + GeoDa
 (100 Monte Carlo simulations — confirm non-random distribution)
        │
        ▼
 GIS Risk Map  ←  ArcGIS + Spatial Analyst
 (roads × water sources × land cover → composite risk surface)
        │
        ├─ Drone Flight Paths  ←  ArduPilot Mega Planner
        │  (camera FOV × altitude × battery → coverage area per pass)
        │
        └─ Ranger Station Placement  ←  ArcGIS Travel-Cost Surface
           (terrain resistance → optimal guard post locations)
```

---

## Tech Stack

| Item | Detail |
|---|---|
| GIS Platform | ESRI ArcGIS with Spatial Analyst Extension |
| Statistical Analysis | R-STAT (point pattern analysis), GeoDa (spatial autocorrelation) |
| Drone Path Planning | ArduPilot Mega Planner |
| Study Area | Tsavo region, southwest Kenya — 8,150 sq miles |
| Incident Data | 156 elephant poaching locations (provided by Kenyan conservation group) |

---

## Course

CMPSC/DS 442 — Artificial Intelligence  
The Pennsylvania State University · 2022
