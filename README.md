# flask-cicd-demo

A Python Flask web application with a fully automated CI/CD pipeline using GitHub Actions and AWS Elastic Beanstalk.

Every push to the `main` branch automatically runs tests and deploys the application to AWS — no manual steps required.

---

## Tech Stack

- **Python / Flask** — web application
- **pytest** — unit testing
- **GitHub Actions** — CI/CD pipeline automation
- **AWS Elastic Beanstalk** — application hosting
- **AWS IAM** — secure credentials and access management
- **AWS S3** — deployment package storage (managed by Elastic Beanstalk)

---

## How the Pipeline Works

1. Code is pushed to the `main` branch on GitHub
2. GitHub Actions automatically triggers the pipeline
3. Dependencies are installed from `requirements.txt`
4. Unit tests are run with pytest — if any test fails, the pipeline stops and no deployment occurs
5. The application is zipped and deployed to AWS Elastic Beanstalk
6. The live application is updated at the Elastic Beanstalk URL

---

## Project Structure

```
flask-cicd-demo/
├── .github/
│   └── workflows/
│       └── deploy.yml      # Pipeline definition
├── tests/
│   └── test_app.py         # Unit tests
├── application.py          # Flask application
├── requirements.txt        # Python dependencies
├── conftest.py             # pytest configuration
└── .gitignore
```

---

## Local Setup

1. Clone the repository
```bash
git clone https://github.com/yourusername/flask-cicd-demo.git
cd flask-cicd-demo
```

2. Create and activate a virtual environment
```bash
python -m venv venv
# Windows
.\venv\Scripts\Activate.ps1
# Mac/Linux
source venv/bin/activate
```

3. Install dependencies
```bash
pip install -r requirements.txt
```

4. Run the app locally
```bash
python application.py
```

Visit `http://127.0.0.1:5000` in your browser.

5. Run tests
```bash
pytest tests/
```

---

## AWS Configuration

The pipeline requires the following GitHub Secrets to be set in the repository settings:

| Secret | Description |
|--------|-------------|
| `AWS_ACCESS_KEY_ID` | IAM user access key |
| `AWS_SECRET_ACCESS_KEY` | IAM user secret key |
| `AWS_REGION` | AWS region (e.g. us-east-2) |

The IAM user is configured with least-privilege permissions, limited to Elastic Beanstalk and S3 actions only.