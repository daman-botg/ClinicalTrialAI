#  Clinical Trial Outcome Predictor

An AI-powered tool(Local Website) that predicts clinical trial outcomes using fine-tuned BioBERT and provides natural language explanations via Gemini AI.

##  Overview

This project uses machine learning to predict whether clinical trials will succeed or fail based on their protocol descriptions. The system was trained on 472 completed clinical trials and achieves 84.5% accuracy.

**Key Features:**
-  BioBERT model fine-tuned on clinical trial data
-  AI-powered explanations using Google Gemini
-  Interactive web interface built with Gradio
-  Detailed risk factor analysis
-  Real-time predictions in seconds

##  Model Performance

| Metric | Score |
|--------|-------|
| Accuracy | 84.5% |
| Precision | 86.3% |
| Recall | 97.5% |
| F1 Score | 91.6% |
| ROC-AUC | 0.596 |

**Note:** The model is highly sensitive (97.5% recall) but conservative in predicting failures (86.3% precision).

##  Quick Start

### Prerequisites

- Python 3.8+
- CUDA-capable GPU (optional, but recommended)
- Google Gemini API key (free tier available)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/clinical-trial-predictor.git
cd clinical-trial-predictor
```

2. **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Set up API key**
Create a `.env` file:
```
GEMINI_API_KEY=your_api_key_here
```

Get your free API key at: https://makersuite.google.com/app/apikey

5. **Download the model**

The trained BioBERT model is too large for GitHub. Download it from:
[Google Drive Link] or [Hugging Face Link]

Extract to `models/biobert-clinical-trial/`

### Running the Application
```bash
python app.py
```

The web interface will open automatically at `http://localhost:7860`

##  Usage

### Web Interface

1. **Enter trial information:**
   - Trial title (e.g., "Phase 3 Study of Drug X")
   - Detailed description (150+ words recommended)
   - Eligibility criteria (optional)

2. **Get prediction:**
   - Success/failure prediction
   - Confidence score
   - Risk factors
   - AI explanation

3. **Ask follow-up questions:**
   - "Why this prediction?"
   - "How to improve chances?"
   - Custom questions

### Programmatic Usage
```python
from src.model import ClinicalTrialPredictor

# Initialize predictor
predictor = ClinicalTrialPredictor('models/biobert-clinical-trial')

# Make prediction
result = predictor.predict(
    title="Phase 3 Study of Drug X",
    description="Randomized, double-blind...",
    eligibility="Age ≥18 years..."
)

print(result['prediction'])  # SUCCESS or FAILURE
print(result['success_probability'])  # 87.3
```

##  Documentation

- [Installation Guide](docs/installation.md)
- [Usage Guide](docs/usage.md)
- [Model Training](notebooks/02_model_training.ipynb)
- [API Reference](docs/api.md)

##  Methodology

### Data Collection
- **Source:** ClinicalTrials.gov API
- **Size:** 472 completed trials (Phase 2 & 3)
- **Labels:** Success (completed) vs Failure (terminated for scientific reasons)
- **Conditions:** Cancer, diabetes, cardiovascular, neurological, respiratory

### Model Architecture
- **Base Model:** BioBERT v1.1 (110M parameters)
- **Fine-tuning:** 8 epochs with class-weighted loss
- **Input:** Trial title + description + eligibility (max 512 tokens)
- **Output:** Binary classification (success/failure)

### Explainability
- **LLM Integration:** Google Gemini 2.5 Flash
- **Purpose:** Generate human-readable explanations
- **Context:** Includes prediction, confidence, and risk factors

##  Dataset

Due to size and privacy considerations, the dataset is not included in this repository. 

**To recreate the dataset:**
```bash
python scripts/download_data.py
```

This will download trials from ClinicalTrials.gov API (requires no authentication).

##  Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

##  License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

##  Disclaimer

**This tool is for research and educational purposes only.** 

- Predictions should NOT be the sole basis for clinical trial decisions
- Always consult with clinical trial experts, statisticians, and regulatory specialists
- The model's predictions are based on historical patterns and may not apply to novel trial designs
- No warranty is provided regarding accuracy or reliability

##  Acknowledgments

- **BioBERT** by DMIS Lab (Korea University)
- **ClinicalTrials.gov** for public trial data
- **Google Gemini** for AI explanations
- **Gradio** for the web interface
- Built for Yale NLP Medical Research Program application

##  Contact

Guhan Venkat - guhan.venkatachalapathi@gmail.com

##  Citation

If you use this work in your research, please cite:
```bibtex
@software{ClinicalTrialAI,
  author = {Guhan Venkat},
  title = {Clinical Trial Outcome Predictor(ClinicalTrialAI): AI-Powered Analysis Using BioBERT},
  year = {2026},
  url = {https://github.com/daman-botg/ClinicalTrialAI}
}
```

##  Related Work

- [BioBERT Paper](https://arxiv.org/abs/1901.08746)
- [Clinical Trial Success Rates](https://pubmed.ncbi.nlm.nih.gov/30503307/)
- [NLP in Clinical Research](https://www.nature.com/articles/s41591-020-0965-x)