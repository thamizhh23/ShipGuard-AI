# SHIPGUARD AI
### Indigenous Contactless AI-Powered Ship Inspection and Structural Health Monitoring System

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Framework: Streamlit](https://img.shields.io/badge/framework-Streamlit-red.svg)](https://streamlit.io/)
[![YOLOv8](https://img.shields.io/badge/model-YOLOv8-green.svg)](https://github.com/ultralytics/ultralytics)
[![Database: SQLite](https://img.shields.io/badge/database-SQLite-lightgrey.svg)](https://www.sqlite.org/)
[![No Fake Data Policy](https://img.shields.io/badge/policy-Zero%20Fake%20Data-brightgreen.svg)]()

---

## 1. Problem Statement
Commercial cargo ships, naval vessels, and offshore structures operate continuously under aggressive marine environments characterized by saltwater immersion, wave slap, and mechanical vibration. Regular inspection is critical to identify:
* **Structural Damage**: Plate deformation, buckled stiffeners, and weld fissures.
* **Corrosion & Scaling**: Severe metal loss compromising hull watertight integrity.
* **Fatigue Cracks**: Sub-critical fissures that propagate rapidly into catastrophic hull fractures.

Current inspection workflows heavily rely on manual checks, requiring inspectors to enter dark, hazardous confined spaces (double bottoms, ballast tanks) or erect dangerous staging along dry-dock hulls. This is time-consuming, expensive (\$20k-\$100k/day dry-dock downtime), and prone to human oversight.

---

## 2. Solution Overview
**SHIPGUARD AI** is an indigenous, contactless visual inspection system. By leveraging remote imagery from handheld cameras, crawlers, or autonomous inspection drones, SHIPGUARD AI executes an automated computer vision pipeline:

```
Real Ship Inspection Photo
           ↓
Image Preprocessing & Normalization
           ↓
Real AI Computer Vision Model (YOLOv8)
           ↓
Defect Detection & Spatial Bounding Box
           ↓
Confidence Scoring & Area Calculation
           ↓
Explainable Severity Assessment (LOW / MED / HIGH / CRITICAL)
           ↓
Inspection Prioritization Risk Score (0-100)
           ↓
Operational Maintenance Recommendation
           ↓
Persistent SQLite Inspection Registry
           ↓
Interactive Dashboard & Automated PDF Inspection Report
```

---

## 3. Key Features
* **Real Computer Vision Defect Detection**: Runs actual PyTorch neural network inference with Ultralytics YOLOv8. No hardcoded or fake predictions.
* **Multi-Defect Localization**: Localizes corrosion, iron rust, copper corrosion, severe degradation, and structural cracks with bounding boxes and confidence scores.
* **Transparent Severity Engine**: Categorizes defects into `LOW`, `MEDIUM`, `HIGH`, `CRITICAL` with explainable engineering rationales.
* **Inspection Prioritization Risk Score (0-100)**: Decomposes overall risk mathematically across defect count, confidence, surface area %, and defect hazard classes.
* **Actionable Maintenance Recommendations**: Maps risk scores directly to operational timeframes (Routine, 30-Day Scheduled, 7-Day Priority, Immediate Expert Survey).
* **Local SQLite Inspection History**: Persistent audit trail with search, filter, and CSV export.
* **Automated PDF Report Generation**: One-click generation of statutory-grade reports via ReportLab with embedded annotated imagery and localized defect tables.
* **Zero Fake Data Policy**: Honest metrics, real models, and authentic public maritime datasets.

---

## 4. Technology Stack
* **Language**: Python 3.10+
* **Computer Vision**: Ultralytics YOLOv8, OpenCV (`opencv-python`), Pillow (`PIL`)
* **Deep Learning Runtime**: PyTorch, Torchvision
* **Dashboard / UI**: Streamlit
* **Database**: SQLite3 (Native Python interface)
* **Data Processing**: Pandas, NumPy
* **Report Generation**: ReportLab PDF Engine
* **Plotting**: Matplotlib

---

## 5. Dataset Specifications & Provenance
In accordance with our strict No Fake Data Policy, SHIPGUARD AI uses real, publicly accessible computer vision datasets:
* **Roboflow Marine Rust & Corrosion Dataset** (`rust-detection-38s6e` / `Francesco/corrosion-bi3q3`): 1,842 real industrial and marine images annotated for surface corrosion and oxidation.
* **OpenSistemas Crack Dataset** (`YOLOv8-crack-seg`): 11,298 structural surface crack inspection images.
* **Wikimedia Commons Marine Archive**: Authentic public domain maritime hull photographs.
* Detailed information, license terms, and split breakdowns are documented in [`dataset/README.md`](dataset/README.md).

---

## 6. Installation

Clone the repository and install dependencies:

```bash
# Clone the repository
git clone https://github.com/your-username/ShipGuardAI.git
cd ShipGuardAI

# Create and activate a virtual environment
python -m venv .venv

# On Windows (PowerShell):
.venv\Scripts\Activate.ps1

# On Linux / macOS:
source .venv/bin/activate

# Install required packages
pip install -r requirements.txt
```

---

## 7. Running the Application

Launch the Streamlit dashboard:

```bash
streamlit run app.py
```

The application will launch in your browser at `http://localhost:8501`.

---

## 8. Running Automated Tests

Run the full automated verification test suite:

```bash
python -m unittest discover -s tests -p "test_*.py" -v
```

All 22 unit tests validate model loading, bounding-box validity, rule determinism, risk mathematical bounds, database persistence, and PDF report creation.

---

## 9. System Architecture

```
Current Operational Architecture (Camera / Vision MVP):
┌────────────────────────────────────────────────────────┐
│                   OPTICAL INPUT LAYER                  │
│       Camera / Drone Imagery / Historical JPEGs        │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
              Image Preprocessing & Resizing
                            │
                            ▼
           YOLOv8 Neural Network (model/best.pt)
                            │
             ┌──────────────┴──────────────┐
             ▼                             ▼
   Corrosion & Rust Detections     Crack Localizations
             └──────────────┬──────────────┘
                            │
                            ▼
            Explainable Rule Severity Engine
                            │
                            ▼
             Risk Prioritization Score (0-100)
                            │
             ┌──────────────┴──────────────┐
             ▼                             ▼
    Local SQLite Database          Streamlit UI Dashboard
             │                             │
             └──────────────┬──────────────┘
                            ▼
             Automated ReportLab PDF Report
```

### Future Multi-Sensor Fusion Architecture (FUTURE WORK):
```
    Camera           3D LiDAR         Thermal IR       Acoustic / EMAT
  (Visual BBox)   (Dent Depth)    (Sub-surface Heat)   (Wall Thickness)
        │                │                 │                   │
        └────────────────┼─────────────────┴───────────────────┘
                         ▼
             Multi-Sensor Fusion Engine
                         ▼
        Integrated Hull Digital Twin Platform
```
*Note: Sensors beyond optical cameras are designed as future architecture and are not simulated or faked in this prototype.*

---

## 10. Limitations (Honest Disclosure)
* **Camera-based MVP**: Remote optical sensing only; does not include physical ultrasonic or thermal hardware in this prototype.
* **Surface-Visible Only**: Cannot measure interior metal plate thickness thinning without non-destructive ultrasound testing (UTM).
* **AI-Assisted Prioritization**: Severity and Risk scores are heuristic decision-support metrics; they do **not** replace certified marine surveyor clearance or statutory classification society surveys.

---

## 11. Future Scope
* **Autonomous Drone Integration**: Real-time video streaming from GPS-denied inspection drones inside cargo holds.
* **3D LiDAR Deformation Mapping**: Millimeter-accuracy dent, deflection, and curvature mapping.
* **Thermal Infrared Imaging**: Detection of sub-surface delamination and void formation.
* **Acoustic / EMAT Testing**: Contactless wall thinning and interior micro-fissure profiling.
* **3D Ship Digital Twin**: Interactive 3D vessel model mapping defect coordinates across hull frames.
* **Cloud Fleet Telemetry**: Fleetwide dashboard for shipping operators and port authorities.

---

## 12. Deployment Instructions (Streamlit Community Cloud)
1. Push this repository to GitHub:
   ```bash
   git init
   git add .
   git commit -m "Initial release of SHIPGUARD AI MVP"
   git branch -M main
   git remote add origin https://github.com/your-username/ShipGuardAI.git
   git push -u origin main
   ```
2. Navigate to [share.streamlit.io](https://share.streamlit.io/).
3. Connect your GitHub account and select this repository.
4. Set the main file path to `app.py`.
5. Click **Deploy**. The application will read `requirements.txt` and deploy automatically.
