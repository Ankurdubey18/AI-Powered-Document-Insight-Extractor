# AI-Powered Document Insight Extractor

An intelligent document analysis application that extracts structured insights from retail media documents (PDF/DOCX) using AI-powered natural language processing. The application uses transformer models to summarize documents, classify document types, and extract key information like deadlines, KPIs, technical specifications, and action items.

- Project Video Explanation: https://drive.google.com/file/d/11_T_IGaWlPG041uA_O7IMRkdhUR5Ugg8/view?usp=drive_link

- Live Project Demo: https://frontend-ruby-pi-tz28sfllbr.vercel.app/

## 🎯 Features

### Document Processing
- **Multi-format Support**: Parse PDF and DOCX files
- **File Validation**: Automatic validation of file type and size (max 10MB)
- **Error Handling**: Comprehensive error handling for corrupted or invalid files

### AI-Powered Extraction
- **Text Summarization**: Uses T5-Small model to generate concise 2-3 sentence summaries
- **Document Classification**: Identifies document types (Creative Brief, Campaign Brief, etc.)
- **Structured Data Extraction**:
  - Technical specifications (dimensions, formats, file sizes)
  - Deadlines and important dates
  - KPIs (CTR, CPC, conversion rates, etc.)
  - Brand guidelines (colors, fonts, tone)
  - Action items and tasks
  - Compliance warnings

### User Interface
- **Drag & Drop Upload**: Easy file upload with drag-and-drop support
- **Real-time Processing**: Visual feedback during document processing
- **Structured Results Display**: Organized presentation of extracted insights
- **JSON Export**: Download results as JSON file
- **Connection Monitoring**: Real-time backend connection status indicator

## 🏗️ Architecture

This is a full-stack application with:
- **Backend**: FastAPI (Python) with AI/ML models
- **Frontend**: React + TypeScript with Vite
- **AI Models**: Hugging Face Transformers (T5-Small, DistilBERT)

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Python 3.8+** (for backend)
- **Node.js 18+** and **npm** (for frontend)
- **Internet connection** (for downloading AI models on first run)

## 🚀 Quick Start

### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd AI-Powered-Document-Insight-Extractor
```

### Step 2: Set Up Backend

```bash
# Navigate to backend directory
cd backend

# Create virtual environment (recommended)
python -m venv venv

# Activate virtual environment
# On Windows:
.\venv\Scripts\activate
# On Mac/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Step 3: Start Backend Server

```bash
# Make sure you're in the backend directory with venv activated
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

**Expected Output:**
```
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Started reloader process
INFO:     Started server process
INFO:     Application startup complete.
```

The backend API will be available at **http://localhost:8000**

> **Note**: On first run, AI models will be downloaded automatically (may take 1-2 minutes). Models are cached for subsequent runs.

### Step 4: Set Up Frontend

Open a **new terminal window**:

```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

**Expected Output:**
```
  VITE v7.x.x  ready in xxx ms

  ➜  Local:   http://localhost:5173/
```

The frontend application will be available at **http://localhost:5173**

### Step 5: Use the Application

1. Open your browser and navigate to `http://localhost:5173`
2. Verify the "Backend Connected" badge appears (green)
3. Upload a PDF or DOCX file:
   - Drag and drop a file onto the upload area, OR
   - Click the upload area to browse for a file
4. Click "Extract Insights" button
5. Wait for processing (you'll see a loading spinner)
6. View the extracted insights in the results panel
7. Download results as JSON if needed

## 📁 Project Structure

```
AI-Powered-Document-Insight-Extractor/
├── backend/
│   ├── main.py                 # FastAPI application entry point
│   ├── config.py               # Configuration settings
│   ├── requirements.txt        # Python dependencies
│   ├── services/               # Core services
│   │   ├── document_parser.py  # PDF/DOCX parsing
│   │   ├── ai_extractor.py     # AI-powered extraction
│   │   └── model_loader.py     # ML model loading
│   ├── utils/                  # Utility functions
│   │   ├── helpers.py
│   │   ├── pattern_matcher.py
│   │   ├── structured_extractor.py
│   │   └── summary_simplifier.py
│   ├── models/                 # Model definitions
│   ├── temp_uploads/           # Temporary file storage
│   └── test_documents/         # Sample test documents
├── frontend/
│   ├── src/
│   │   ├── api/                # Backend API integration
│   │   ├── components/         # React components
│   │   ├── pages/              # Page components
│   │   └── utils/              # Helper functions
│   ├── package.json
│   └── vite.config.ts
└── README.md                   # This file
```

## ⚙️ Configuration

### Backend Configuration

Create a `.env` file in the `backend/` directory (optional):

```env
# AI Model Configuration
T5_MODEL_NAME=t5-small
DISTILBERT_MODEL_NAME=distilbert-base-uncased
DEVICE=cpu  # or 'cuda' for GPU support

# API Configuration
API_HOST=0.0.0.0
API_PORT=8000

# CORS Configuration
ALLOWED_ORIGINS=http://localhost:5173,http://localhost:3000
```

### Frontend Configuration

Create a `.env` file in the `frontend/` directory (optional):

```env
VITE_API_URL=http://localhost:8000
```

> **Note**: If you don't create `.env` files, the application will use default values.

## 🔌 API Endpoints

### Health Check
- `GET /` - Root endpoint with API information
- `GET /health` - Basic health check
- `GET /api/health` - Detailed API health check

### Document Processing
- `POST /api/parse-document` - Parse document and extract raw text
- `POST /api/analyze` - Analyze document and return extracted text
- `POST /api/extract-insights` - Extract AI-powered structured insights

### API Documentation

Once the backend is running, visit:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

## 🧪 Testing

### Test Backend

```bash
cd backend

# Test document parser
python test_parser.py

# Test AI extraction
python test_ai_extraction.py

# Test model loader
python test_model_loader.py

# Test API endpoints
python test_endpoints.py
```

### Test Frontend

1. Start both backend and frontend servers
2. Open browser to `http://localhost:5173`
3. Upload a test document from `backend/test_documents/`
4. Verify all features work correctly

### Manual API Testing with curl

```bash
# Health check
curl http://localhost:8000/api/health

# Extract insights
curl -X POST "http://localhost:8000/api/extract-insights" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@path/to/document.pdf"
```

## 🐛 Troubleshooting

### Backend Issues

#### Port Already in Use
If port 8000 is already in use:
```bash
uvicorn main:app --reload --port 8001
```
Then update frontend `.env` to use port 8001.

#### Model Loading Issues
**Symptoms**: Slow startup or model loading errors

**Solutions**:
- Models download automatically on first use (may take 1-2 minutes)
- Ensure internet connection is available
- Models are cached in `~/.cache/huggingface/` after first download
- Check backend logs for specific error messages

#### Memory Issues
**Symptoms**: Out of memory errors

**Solutions**:
- Use CPU mode: Set `DEVICE=cpu` in `.env`
- Process smaller files
- Increase system RAM if possible

#### File Upload Errors
**Symptoms**: File upload fails

**Solutions**:
- Check file size (must be under 10MB)
- Check file type (only PDF and DOCX supported)
- Verify `temp_uploads/` directory exists and is writable
- Check backend terminal for detailed error messages

### Frontend Issues

#### Backend Not Connecting
**Symptoms**: Red "Backend Disconnected" badge

**Solutions**:
1. Verify backend is running on port 8000
2. Check `VITE_API_URL` in frontend `.env` file
3. Verify CORS is configured in backend `main.py`
4. Check browser console for specific errors

#### CORS Errors
**Symptoms**: Console shows CORS errors

**Solutions**:
1. Verify backend CORS allows `http://localhost:5173`
2. Check `ALLOWED_ORIGINS` in backend configuration
3. Restart backend server after CORS changes

#### File Upload Fails
**Symptoms**: Error message after clicking "Extract Insights"

**Solutions**:
1. Check file size (must be under 10MB)
2. Check file type (only PDF and DOCX supported)
3. Check browser console for errors
4. Verify backend is running and accessible

## 📦 Dependencies

### Backend Dependencies
- `fastapi` - Web framework
- `uvicorn` - ASGI server
- `python-multipart` - File upload support
- `pdfplumber` - PDF parsing
- `python-docx` - DOCX parsing
- `transformers` - Hugging Face transformers
- `torch` - PyTorch for ML models
- `python-dotenv` - Environment variable management

See `backend/requirements.txt` for complete list.

### Frontend Dependencies
- `react` - UI library
- `react-dom` - React DOM renderer
- `tailwindcss` - CSS framework
- `typescript` - Type safety
- `vite` - Build tool

See `frontend/package.json` for complete list.

## 🚀 Production Deployment

### Backend Deployment

1. **Set Environment Variables**:
   ```env
   DEVICE=cpu
   API_HOST=0.0.0.0
   API_PORT=8000
   ALLOWED_ORIGINS=https://your-frontend-domain.com
   ```

2. **Use Production Server**:
   ```bash
   uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
   ```

3. **Set Up Reverse Proxy**: Use nginx or similar for production deployment

### Frontend Deployment

1. **Set Environment Variables**:
   ```env
   VITE_API_URL=https://your-backend-api.com
   ```

2. **Build for Production**:
   ```bash
   cd frontend
   npm run build
   ```

3. **Deploy**: The `dist/` folder can be deployed to:
   - Vercel
   - Netlify
   - GitHub Pages
   - Any static file hosting service

## 📊 Performance

### Model Loading
- Models load on first request (~10-30 seconds)
- Models are cached after first load
- Subsequent requests are faster

### Processing Time
- Small files (< 1MB): ~5-10 seconds
- Medium files (1-5MB): ~10-30 seconds
- Large files (5-10MB): ~30-60 seconds

### Optimization Tips
1. Use GPU if available (`DEVICE=cuda`)
2. Process files in batches
3. Models are automatically cached after first load

## 🔒 Security Considerations

- File type validation prevents malicious uploads
- File size limits prevent DoS attacks
- Temporary files are automatically cleaned up
- CORS configured for specific origins
- Environment variables for sensitive configuration

## 📝 API Response Format

Example response from `/api/extract-insights`:

```json
{
  "success": true,
  "message": "Insights extracted successfully",
  "summary": {
    "goal": "Campaign goal description",
    "dates": ["2024-01-15", "2024-02-01"],
    "channels": ["Social Media", "Display"],
    "primary_kpis": ["CTR", "Conversion Rate"],
    "key_constraints": ["Budget limit", "Brand guidelines"]
  },
  "document_type": {
    "type": "Creative Brief",
    "confidence": 0.95
  },
  "creative_requirements": {
    "must_have": ["Logo", "Brand colors"],
    "optional": ["Animation", "Video"]
  },
  "technical_specs": [
    {
      "type": "dimension",
      "value": "1080x1080"
    }
  ],
  "guidelines": {
    "copy_rules": ["Use brand voice"],
    "design_rules": ["Follow brand colors"],
    "accessibility_rules": ["Alt text required"],
    "legal_rules": ["Include disclaimer"]
  },
  "action_items": [
    {
      "task": "Review creative assets",
      "priority": "high"
    }
  ],
  "file_metadata": {
    "filename": "document.pdf",
    "file_size": "2.5 MB",
    "file_type": ".pdf",
    "text_length": 5000,
    "word_count": 800
  }
}
```

## ✅ Verification Checklist

When everything is working correctly:
- ✅ Backend server running on port 8000
- ✅ Frontend server running on port 5173
- ✅ Can upload PDF files
- ✅ Can upload DOCX files
- ✅ Processing indicator shows during upload
- ✅ Results display correctly in all sections
- ✅ Can download JSON results
- ✅ No console errors in browser
- ✅ No errors in backend terminal

## 📚 Additional Resources

- **Backend API Docs**: http://localhost:8000/docs (when backend is running)
- **Hugging Face Models**: 
  - [T5-Small](https://huggingface.co/t5-small)
  - [DistilBERT](https://huggingface.co/distilbert-base-uncased)

## 🤝 Contributing

This project is ready for use. If you encounter any issues or have suggestions:
1. Check the troubleshooting section
2. Review backend/frontend logs
3. Verify all prerequisites are met

## 📄 License

[Add your license information here]

---

**Version**: 1.0.0  
**Status**: ✅ Complete and ready for use

All features implemented and tested:
- ✅ Document parsing (PDF/DOCX)
- ✅ AI-powered extraction
- ✅ Pattern matching for structured data
- ✅ Error handling
- ✅ API endpoints
- ✅ Frontend UI
- ✅ CORS configuration

