# Metis DICOM Viewer

A professional, web-based medical imaging viewer with AI-powered brain tumor segmentation capabilities. Built for clinical use, this application provides advanced visualization tools for NIfTI MRI files with integrated deep learning segmentation models.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Python](https://img.shields.io/badge/python-3.13-blue.svg)
![TypeScript](https://img.shields.io/badge/typescript-5.9-blue.svg)
![React](https://img.shields.io/badge/react-19.1-blue.svg)

## 🎯 Overview

Metis DICOM Viewer is a full-stack medical imaging application designed for radiologists and medical professionals. It combines a modern, intuitive web interface with powerful backend processing capabilities to provide:

- **Multi-viewport DICOM/NIfTI visualization** with axial, coronal, sagittal, and 3D volume rendering
- **AI-powered brain tumor segmentation** using deep learning models (PSPNet and U-Net)
- **Professional annotation and measurement tools** for clinical documentation
- **Cloud-based storage** with AWS S3 integration
- **Comprehensive keyboard shortcuts** for efficient workflow

## ✨ Features

### 🖼️ Image Viewing
- **Multi-viewport support**: Up to 4 simultaneous viewports with independent controls
- **Multiple viewing planes**: Axial, Coronal, Sagittal, and 3D Volume rendering
- **Advanced windowing**: Adjustable window/level (brightness) and window width (contrast)
- **Zoom and pan**: Precise image manipulation with mouse and keyboard controls
- **Slice navigation**: Quick navigation through image stacks with arrow keys

### 🤖 AI Segmentation
- **Dual model support**: PSPNet and U-Net architectures for brain tumor segmentation
- **Multi-modal processing**: Automatic detection and processing of FLAIR, T1, T1CE, and T2 sequences
- **Real-time overlay**: Toggle segmentation masks over original images
- **Detailed statistics**: Voxel counts for background, necrotic core, edema, and enhancing tumor regions

### 📏 Measurement & Annotation Tools
- **Linear measurements**: Measure distances between points on images
- **Point annotations**: Add text annotations with color-coded markers
- **Eraser tool**: Remove measurements and annotations
- **Persistent overlays**: Annotations persist across slice navigation

### ⌨️ Keyboard Shortcuts
Comprehensive keyboard shortcut system for efficient workflow:
- **Navigation**: Arrow keys for slice navigation, `+/-` for zoom
- **Viewport selection**: `1-4` to switch between viewports
- **View switching**: `X` (Axial), `Y` (Coronal), `G` (Sagittal), `V` (3D)
- **Tools**: `S` (Scroll), `Z` (Zoom), `P` (Pan), `B` (Brightness), `C` (Contrast)
- **Annotations**: `M` (Measure), `A` (Annotate), `E` (Erase)
- **AI**: `Ctrl/Cmd + Enter` (Run segmentation), `O` (Toggle overlay)
- **Help**: `?` or `H` to toggle keyboard shortcuts reference

Press `?` or `H` in the viewer to see the complete keyboard shortcuts legend.

### 🎨 User Interface
- **Dark mode optimized**: Professional dark theme designed for extended viewing sessions
- **Responsive design**: Works on various screen sizes and resolutions
- **Intuitive controls**: Collapsible sidebar with organized tool sections
- **Visual feedback**: Clear indicators for active tools and modes

## 🏗️ Architecture

### Frontend
- **Framework**: React 19.1 with TypeScript
- **Build Tool**: Vite 7.1
- **Routing**: React Router DOM 7.9
- **Styling**: TailwindCSS 4.1 with custom CSS
- **Medical Imaging Libraries**:
  - `@niivue/niivue`: Advanced 3D medical image rendering
  - `nifti-reader-js`: NIfTI file parsing and reading
  - `cornerstone-core`: DICOM image rendering foundation

### Backend
- **Framework**: FastAPI with Python 3.13
- **Database**: PostgreSQL with psycopg2
- **Cloud Storage**: AWS S3 via boto3
- **Medical Imaging**: nibabel for NIfTI processing
- **Deep Learning**: PyTorch with segmentation-models-pytorch

### Segmentation Models
- **PSPNet**: Pyramid Scene Parsing Network for semantic segmentation
- **U-Net**: Custom improved U-Net architecture
- **Training Data**: BraTS 2016 dataset (requires separate download)

## 📋 Prerequisites

### Required Software
- **Node.js** 18+ and npm
- **Python** 3.13+
- **PostgreSQL** 12+ (running locally or remotely)
- **AWS Account** with S3 bucket configured

### Required Data
- **BraTS 2016 Dataset**: For training segmentation models
  - Download from: [https://www.med.upenn.edu/sbia/brats2016.html](https://www.med.upenn.edu/sbia/brats2016.html)
  - Place in `Segmentation_Models/data/` directory

## 🚀 Installation

### 1. Clone the Repository
```bash
git clone <repository-url>
cd Metis_DICOM_Viewer
```

### 2. Backend Setup

```bash
cd Projects/Metis_Capstone/Backend

# Create virtual environment
python3 -m venv venv

# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Backend Environment Configuration

Create a `.env` file in `Projects/Metis_Capstone/Backend/`:

```env
# PostgreSQL Configuration
DB_HOST=localhost
DB_NAME=dicom_db
DB_USER=your_username
DB_PASSWORD=your_password
DB_PORT=5432

# AWS S3 Configuration
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
AWS_REGION=us-east-1
S3_BUCKET=your-s3-bucket-name

# Model Configuration (optional - for segmentation)
MODEL_CHECKPOINT_PATH=s3://your-bucket/path/to/model.pth
UNET_MODEL_PATH=s3://your-bucket/path/to/unet_model.pth
```

### 4. Frontend Setup

```bash
cd Projects/Metis_Capstone/frontend

# Install dependencies
npm install
```

### 5. Segmentation Models Setup (Optional)

If you plan to train or use segmentation models:

```bash
cd Projects/Metis_Capstone/Segmentation_Models

# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate  # macOS/Linux
# or
venv\Scripts\activate  # Windows

# Install dependencies
pip install -r requirements.txt

# Download and place BraTS 2016 dataset in data/ directory
```

## 🏃 Running the Application

### Start the Backend Server

```bash
cd Projects/Metis_Capstone/Backend
source venv/bin/activate  # Activate venv if not already active
python main.py
```

The backend will start on `http://localhost:8000`

### Start the Frontend Development Server

```bash
cd Projects/Metis_Capstone/frontend
npm run dev
```

The frontend will start on `http://localhost:3000` (or the next available port)

### Access the Application

Open your browser and navigate to:
- **Frontend**: `http://localhost:3000`
- **Backend API Docs**: `http://localhost:8000/docs` (FastAPI automatic documentation)

## 📖 Usage Guide

### Uploading Images

1. From the landing page, click "Upload File" or drag and drop a NIfTI file (`.nii` or `.nii.gz`)
2. The file will be automatically uploaded to the backend and stored in S3
3. You'll be redirected to the viewer with your image loaded

### Viewing Images

- **Navigate slices**: Use arrow keys (`↑`/`↓`) or the scroll tool
- **Zoom**: Use `+`/`-` keys or the zoom tool
- **Pan**: Activate pan mode (`P`) and drag the image
- **Adjust brightness/contrast**: Activate brightness (`B`) or contrast (`C`) mode and drag vertically

### Using Multiple Viewports

1. Click "New Viewer Window" in the 3D Options section
2. Select a viewport using `1-4` keys
3. Each viewport can have independent views, slices, and settings
4. Maximum of 4 viewports supported

### Running AI Segmentation

1. Upload all 4 modalities (FLAIR, T1, T1CE, T2) with consistent naming:
   - Format: `PatientID_modality.nii` (e.g., `BraTS20_Validation_001_flair.nii`)
2. Select the model type (PSPNet or U-Net) from the dropdown
3. Press `Ctrl/Cmd + Enter` or click "Run Segmentation"
4. Wait for processing (progress will be displayed)
5. Toggle overlay with `O` key or the overlay button

### Making Measurements

1. Activate measure tool (`M` key)
2. Click and drag on the image to create a measurement line
3. Distance is displayed in pixels
4. Use erase tool (`E`) to remove measurements

### Adding Annotations

1. Activate annotate tool (`A` key)
2. Click on the image where you want to place an annotation
3. Enter text in the modal dialog
4. Annotations appear as colored markers with tooltips on hover

## 🔌 API Documentation

### MRI Endpoints

#### Upload MRI File
```http
POST /mri
Content-Type: multipart/form-data

Body: file (NIfTI file)
Response: { message, mri_id, file_path }
```

#### Get All MRI Metadata
```http
GET /mri
Response: List[MRIResponse]
```

#### Get MRI by ID
```http
GET /mri/{mri_id}
Response: MRIResponse
```

#### Download MRI File
```http
GET /mri/{mri_id}/data
Response: Binary file stream
```

#### Detect Modality
```http
POST /mri/{mri_id}/detect
Response: { mri_id, file_name, detected_modality, sibling_files }
```

### Segmentation Endpoints

#### Run Segmentation
```http
POST /mri/{mri_id}/segment?model_type=pspnet
Response: { mri_id, segmentation_id, message, segmentation_path, summary }
```

#### Get Segmentation
```http
GET /mri/{mri_id}/segmentation
Response: { segmentation_id, segmentation_path, date_created, summary }
```

#### Download Segmentation
```http
GET /mri/{mri_id}/segmentation/data
Response: Binary file stream
```

Full API documentation available at `http://localhost:8000/docs` when the backend is running.

## 🗂️ Project Structure

```
Metis_DICOM_Viewer/
├── Projects/
│   └── Metis_Capstone/
│       ├── Backend/
│       │   ├── main.py              # FastAPI application
│       │   ├── inference.py        # Segmentation model inference
│       │   ├── unet_model.py       # Custom U-Net architecture
│       │   ├── requirements.txt     # Python dependencies
│       │   └── .env                 # Environment variables (create this)
│       │
│       ├── frontend/
│       │   ├── src/
│       │   │   ├── components/
│       │   │   │   └── DicomViewer.tsx  # Main viewer component
│       │   │   ├── pages/
│       │   │   │   ├── Landing.tsx      # Landing page
│       │   │   │   └── About.tsx        # About page
│       │   │   └── main.tsx             # Entry point
│       │   ├── public/                  # Static assets
│       │   ├── package.json             # Node dependencies
│       │   └── vite.config.ts            # Vite configuration
│       │
│       └── Segmentation_Models/
│           ├── PSPNet/
│           │   ├── PSPmodel.py      # PSPNet model definition
│           │   ├── DataPREP.py      # Data preprocessing
│           │   └── config.py        # Model configuration
│           ├── Model_Combiners/
│           │   └── MetaLearner_viewcombiner.py
│           └── requirements.txt     # Python dependencies
│
└── README.md
```

## 🧪 Development

### Frontend Development
```bash
cd Projects/Metis_Capstone/frontend
npm run dev      # Start dev server
npm run build    # Build for production
npm run lint     # Run ESLint
```

### Backend Development
```bash
cd Projects/Metis_Capstone/Backend
source venv/bin/activate
python main.py  # Run with uvicorn (development)
# Or use uvicorn directly:
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### Training Segmentation Models
```bash
cd Projects/Metis_Capstone/Segmentation_Models
source venv/bin/activate
# Follow model-specific training scripts in PSPNet/ directory
```

## 🧑‍💻 Team

**Metis Team** - Southeastern Louisiana University Capstone Project

- **Erick** - Team Leader, Backend Developer
- **Brooks** - Data Science & Analytics
- **John** - IT Infrastructure & Security
- **Jackson** - Full-Stack Development
- **Tyler** - Frontend Development

## 📝 License

This project is part of a capstone project at Southeastern Louisiana University.

## 🤝 Contributing

This is a capstone project. For questions or contributions, please contact the team.

## ⚠️ Important Notes

### Data Privacy
- This application is designed for educational and research purposes
- Ensure compliance with HIPAA and other medical data regulations if handling real patient data
- The demo files included are from the BraTS 2016 public dataset

### Model Requirements
- Segmentation models must be trained separately using the BraTS dataset
- Pre-trained model checkpoints should be stored in S3 or locally
- Model paths must be configured in the `.env` file

### Database Setup
- PostgreSQL database must be created and accessible
- Tables are automatically created on first run
- Ensure proper backup procedures for production use

## 🐛 Troubleshooting

### Backend Issues

**Database Connection Error**
- Verify PostgreSQL is running
- Check `.env` file credentials
- Ensure database exists and user has proper permissions

**S3 Connection Error**
- Verify AWS credentials in `.env`
- Check S3 bucket exists and is accessible
- Verify IAM permissions for S3 access

**Model Loading Error**
- Ensure model checkpoint path is correct in `.env`
- Verify model file exists in S3 or local path
- Check model architecture matches code expectations

### Frontend Issues

**Port Already in Use**
- Change port in `vite.config.ts` or use `npm run dev -- --port 3001`

**Module Not Found**
- Run `npm install` to ensure all dependencies are installed
- Clear `node_modules` and reinstall if issues persist

**CORS Errors**
- Ensure backend CORS middleware is configured correctly
- Verify backend is running on expected port

## 📚 Additional Resources

- [NIfTI Format Documentation](https://nifti.nimh.nih.gov/)
- [BraTS Challenge](https://www.med.upenn.edu/sbia/brats2016.html)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [React Documentation](https://react.dev/)
- [Niivue Documentation](https://github.com/niivue/niivue)

## 🔮 Future Enhancements

- [ ] DICOM file support (currently NIfTI only)
- [ ] User authentication and session management
- [ ] Export annotations and measurements to reports
- [ ] Additional segmentation models
- [ ] Real-time collaboration features
- [ ] Mobile-responsive design improvements
- [ ] Advanced 3D rendering options

---

**Built with ❤️ by the Metis Team at Southeastern Louisiana University**
