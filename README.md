# 🎫 AI-Powered Support Ticket Router

An intelligent system that automatically classifies and routes customer support tickets to the appropriate department or agent using Natural Language Processing (NLP) and Machine Learning.

## 🚀 Features

- **Automatic Classification** – Categorizes incoming tickets by type (billing, technical, general, etc.)
- **Smart Routing** – Assigns tickets to the right team or agent based on content and priority
- **NLP-Powered** – Uses state-of-the-art language models to understand ticket intent
- **Priority Detection** – Identifies urgency level (low, medium, high, critical)
- **REST API** – Easy integration with existing helpdesk systems

## 🏗️ Project Structure

```
aI-powered-support-ticket-router/
├── data/               # Datasets for training and evaluation
├── models/             # Trained model artifacts
├── src/                # Source code
│   ├── classifier/     # Ticket classification logic
│   ├── router/         # Routing engine
│   └── api/            # REST API layer
├── tests/              # Unit and integration tests
├── notebooks/          # Jupyter notebooks for experiments
├── requirements.txt    # Python dependencies
└── README.md           # Project documentation
```

## 🛠️ Tech Stack

- **Language**: Python 3.10+
- **ML Framework**: scikit-learn / Hugging Face Transformers
- **API**: FastAPI
- **Testing**: pytest

## ⚙️ Setup & Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/your-username/aI-powered-support-ticket-router.git
   cd aI-powered-support-ticket-router
   ```

2. **Create a virtual environment**

   ```bash
   python -m venv venv
   source venv/bin/activate   # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application**
   ```bash
   uvicorn src.api.main:app --reload
   ```

## 🧪 Running Tests

```bash
pytest tests/
```

## 📄 License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Please open an issue or submit a pull request.
