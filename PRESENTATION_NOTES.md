# SHIPGUARD AI: Hackathon Presentation & Pitch Notes

## 1. Problem Statement
Commercial ships, naval vessels, and offshore platforms operate in harsh saline marine environments. They require continuous, rigorous structural health inspection to detect:
* **Corrosion & Oxidation**: Metal loss leading to hull breaches and environmental disaster.
* **Structural Fatigue Cracks**: Catastrophic failure risks under dynamic sea loads.
* **Surface Pitting & Deformation**: Hydrodynamic drag increase and localized structural weakness.

---

## 2. Existing Limitations of Current Maritime Inspection
* **Manual & Dangerous**: Requires human surveyors in dry-docks or suspended on scaffolding/ropes in hazardous, confined spaces (ballast tanks, double bottoms).
* **High Downtime & Cost**: Dry-docking a vessel costs \$20,000 to \$100,000+ per day.
* **Subjective & Inconsistent**: Human visual checks suffer from inspector fatigue and qualitative scoring disparities.
* **No Real-time Digital Trace**: Inspection logs are often fragmented paper binders or manual spreadsheets without spatial defect coordinates.

---

## 3. Our Solution: SHIPGUARD AI
**SHIPGUARD AI** is an indigenous contactless AI-powered ship inspection and structural health monitoring prototype.
* **Contactless Visual Screening**: Accepts drone, crawler, or handheld camera inspection imagery.
* **Real AI Computer Vision Engine**: Performs genuine object detection with bounding box localization and confidence scores using YOLOv8.
* **Explainable Severity Assessment**: Categorizes defects into `LOW`, `MEDIUM`, `HIGH`, `CRITICAL` with human-auditable engineering rationale.
* **Inspection Prioritization Risk Score (0-100)**: Formulates operational risk and actionable maintenance protocols (Routine, Scheduled, Priority, Immediate).
* **Local Persistent Registry**: SQLite database logging all historical inspections.
* **Automated PDF Inspection Reports**: One-click generation of statutory-grade reports with embedded imagery and spatial coordinates.

---

## 4. How the AI Works
1. **Input Normalization**: Image is converted to standard RGB and scaled to $640 \times 640$ with aspect-ratio letterbox padding.
2. **Deep Learning Backbone**: Passes through YOLOv8 convolutional and cross-stage partial (CSP) feature extraction layers.
3. **Multi-Scale Feature Pyramid**: Detects fine surface micro-cracks alongside expansive corrosion patches.
4. **Bounding Box Regression & Class Scoring**: Generates localized pixel coordinates $[x_1, y_1, x_2, y_2]$, defect classes (`corrosion`, `severe-corrosion`, `crack`, `iron rust`), and confidence values.
5. **Severity & Risk Engine**: Calculates relative defect footprint $\frac{\text{Area}_{\text{defect}}}{\text{Area}_{\text{frame}}}$, evaluates compounding hazard risks, and computes the 0-100 Prioritization Risk score.

---

## 5. Dataset Provenance & Integrity
* In strict adherence to our **No Fake Data Policy**, we do NOT generate fake synthetic defects.
* **Roboflow Marine & Metal Corrosion Dataset** (`rust-detection-38s6e` / `Francesco/corrosion-bi3q3`): 1,842 real industrial and marine images.
* **OpenSistemas Crack Dataset** (`YOLOv8-crack-seg`): 11,298 real structural surface crack images.
* **Maritime Hull Archive**: Authentic ship hull photographs from Wikimedia Commons and marine engineering documentation.

---

## 6. System Architecture
```
[ Drone / Camera Optical Imagery ]
               ↓
    [ Image Preprocessing ]
               ↓
[ YOLOv8 Neural Detection Engine ]
               ↓
 [ Defect Localization & Classes ]
               ↓
   [ Explainable Severity Engine ]
               ↓
 [ Inspection Prioritization Risk (0-100) ]
               ↓
[ SQLite Inspection Database ] ───→ [ Interactive Dashboard ]
                                          ↓
                             [ Automated PDF Inspection Report ]
```

---

## 7. Core Innovation & Competitive Positioning
* **What we DO claim**: 
  > *"Existing research and industry solutions demonstrate AI-assisted inspection. SHIPGUARD AI focuses on integrating defect detection, localization, severity assessment, inspection prioritization, history tracking, and reporting into a lightweight unified contactless inspection workflow suitable for rapid deployment on portside tablets and edge drone docks."*
* **What we DO NOT claim**: 
  > *"We do NOT claim to be the first AI ship inspection system, nor do we claim our risk score replaces statutory classification society certification."*

---

## 8. Industrial & Social Impact
* **Maritime Safety**: Prevents at-sea structural fractures and oil spills.
* **Surveyor Safety**: Reduces human exposure to confined, oxygen-depleted ballast tanks.
* **Economic Efficiency**: Decreases vessel dry-dock downtime by pre-triaging suspect hull plates before docking.
* **Indigenous Capability**: Developed as an open, sovereign inspection framework adaptable for domestic naval and commercial fleets.

---

## 9. Scalability
* **Edge Deployment**: Lightweight YOLOv8 nano model runs in $<150\text{ ms}$ on standard CPUs, making it drone-edge or tablet deployable without expensive cloud GPUs.
* **Fleet Fleetwide Aggregation**: Local SQLite databases can sync periodically to central maritime cloud registries.

---

## 10. Future Scope (Multi-Modal Sensor Fusion)
* **3D LiDAR**: Millimeter-accurate dent depth profiling and hull deformation mapping.
* **Thermal Infrared (IR)**: Subsurface delamination and insulation moisture entrapment.
* **Acoustic / EMAT Resonance**: Contactless plate thickness thinning analysis.
* **Autonomous Drones & Crawlers**: Autonomous GPS-denied inspection inside cargo holds.

---

## 11. Known Limitations (Honest Disclosure)
* **Camera-only MVP**: Multi-spectral (thermal, acoustic, LiDAR) sensors are designed as future architecture.
* **Surface-Only Visuals**: Visual cameras cannot measure interior metal thickness without ultrasonic sensors.
* **Pre-trained Weights**: Models use verified pre-trained weights on public datasets; dry-dock specific fine-tuning is supported via `model/best.pt`.

---

## 12. Two-Minute Live Pitch & Demo Script

### [0:00 - 0:30] The Hook & Problem
> *"Judges, maritime transport carries 90% of global trade. Yet, inspecting massive ship hulls for rust and structural cracks still relies on human surveyors climbing scaffolding inside hazardous, dark ballast tanks. One undetected fatigue crack can lead to catastrophic hull failure, sinkings, and devastating oil spills."*

### [0:30 - 1:00] The Solution: SHIPGUARD AI
> *"This is SHIPGUARD AI: an indigenous contactless AI-powered ship inspection and structural health monitoring system. Instead of manual checks, an inspector or drone captures hull photographs. SHIPGUARD AI instantly detects defects, localizes them, calculates severity, determines prioritization risk, and produces a complete inspection record in seconds."*

### [1:00 - 1:30] Live System Walkthrough
> *(Click 'Choose from Verified Marine Demo Images' -> Select 'Demo Hull Crack Inspection 2' -> Click 'Analyze Inspection')*  
> *"Watch our real neural network in action: Within 150 milliseconds on a standard CPU, our YOLOv8 model localizes 7 structural cracks and corrosion patches with authentic bounding boxes and confidence percentages.*  
> *Notice our transparent severity and risk engine: It calculates an Inspection Prioritization Risk of 78/100, explaining exactly why: high defect density, compounding hazard, and structural crack presence. It immediately outputs the operational maintenance protocol: Priority inspection within 7 days."*

### [1:30 - 2:00] Persistence & Reporting
> *(Click 'Inspection History' tab, then 'Report Generator' -> Download PDF)*  
> *"Every inspection is automatically recorded to our local SQLite database. With a single click, we generate a statutory-grade PDF Inspection Report complete with embedded annotated imagery, spatial bounding box coordinates, and engineering disclaimers.*  
> *SHIPGUARD AI turns slow, hazardous manual surveys into a real-time, explainable, digital inspection workflow. Thank you!"*
