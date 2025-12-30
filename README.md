# 🎯 Agentic Job Hunter

An intelligent multi-agent system that revolutionizes job applications by automatically tailoring resumes and preparing interview materials using AI agents powered by CrewAI.

![Python](https://img.shields.io/badge/python-3.11+-blue.svg)
![CrewAI](https://img.shields.io/badge/CrewAI-latest-green.svg)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4--Turbo-orange.svg)

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [How It Works](#how-it-works)
- [Installation](#installation)
- [Configuration](#configuration)
- [Agents & Their Roles](#agents--their-roles)
- [Project Structure](#project-structure)
- [Best Practices](#best-practices)

## 🎯 Overview

**Agentic Job Hunter** is an AI-powered job application assistant that uses four specialized AI agents working in harmony to:

- 🔍 **Analyze** job postings to extract key requirements
- 👤 **Profile** candidates using their GitHub and personal information
- 📄 **Tailor** resumes to perfectly match job requirements
- 💼 **Prepare** comprehensive interview materials and talking points


## ✨ Features

### 🤖 Four Specialized AI Agents

1. **Tech Job Researcher** - Extracts and analyzes job requirements
2. **Personal Profiler** - Creates comprehensive candidate profiles
3. **Resume Strategist** - Tailors resumes to match specific roles
4. **Interview Preparer** - Generates interview questions and talking points

### 🛠️ Advanced Capabilities

- ✅ **PDF Resume Analysis** - Semantic search through your CV
- ✅ **Web Scraping** - Extracts data from job postings and GitHub
- ✅ **Async Execution** - Parallel processing for faster results
- ✅ **Context-Aware Tasks** - Agents build on each other's work
- ✅ **File Output** - Generates ready-to-use markdown files
- ✅ **ATS Optimization** - Ensures resumes pass Applicant Tracking Systems

## 🏗️ Architecture

```mermaid
graph TB
    subgraph "Input Sources"
        A[Job Posting URL]
        B[Your Resume PDF]
        C[GitHub Profile]
        D[Personal Writeup]
    end
    
    subgraph "AI Agent Crew"
        E[Tech Job Researcher]
        F[Personal Profiler]
        G[Resume Strategist]
        H[Interview Preparer]
    end
    
    subgraph "Tools & APIs"
        I[SerperDev Search]
        J[Web Scraper]
        K[PDF Search Tool]
        L[File Reader]
    end
    
    subgraph "Outputs"
        M[Tailored Resume]
        N[Interview Materials]
    end
    
    A --> E
    B --> F
    C --> F
    D --> F
    
    E --> I
    E --> J
    F --> J
    F --> K
    F --> L
    
    E --> G
    F --> G
    G --> M
    
    E --> H
    F --> H
    G --> H
    H --> N
    
    style E fill:#4CAF50
    style F fill:#2196F3
    style G fill:#FF9800
    style H fill:#9C27B0
    style M fill:#F44336
    style N fill:#F44336
```

## 🔄 How It Works

### Workflow Sequence

```mermaid
sequenceDiagram
    participant User
    participant Researcher
    participant Profiler
    participant Strategist
    participant Preparer
    participant Output
    
    User->>Researcher: Job Posting URL
    User->>Profiler: Resume + GitHub + Writeup
    
    par Parallel Execution
        Researcher->>Researcher: Extract Requirements
        Profiler->>Profiler: Build Profile
    end
    
    Researcher-->>Strategist: Job Requirements
    Profiler-->>Strategist: Candidate Profile
    
    Strategist->>Strategist: Tailor Resume
    Strategist-->>Output: tailored_resume.md
    
    Strategist-->>Preparer: Tailored Resume
    Researcher-->>Preparer: Job Requirements
    Profiler-->>Preparer: Candidate Profile
    
    Preparer->>Preparer: Create Interview Materials
    Preparer-->>Output: interview_materials.md
    
    Output-->>User: Complete Application Package
```

### Task Dependencies

```mermaid
graph LR
    A[Research Task] --> C[Resume Strategy]
    B[Profile Task] --> C
    C --> D[Interview Prep]
    A --> D
    B --> D
    
    style A fill:#4CAF50
    style B fill:#2196F3
    style C fill:#FF9800
    style D fill:#9C27B0
```

## 🚀 Installation

### Prerequisites

- Python 3.11 or higher
- OpenAI API key
- Serper API key (for web search)
- Your resume in PDF format

### Step-by-Step Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/iitsh/Agentic-Job-Hunter.git
   cd Agentic-Job-Hunter
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install crewai crewai-tools python-dotenv jupyter
   ```

4. **Set up your API keys**
   ```bash
   cp .env.example .env
   # Edit .env and add your API keys
   ```

5. **Add your resume**
   ```bash
   # Place your CV as YOUR_CV.pdf in the root directory
   ```

## ⚙️ Configuration

### Environment Variables

Create a `.env` file with your API keys:

```env
OPENAI_API_KEY=your_openai_api_key_here
SERPER_API_KEY=your_serper_api_key_here
```

### Get Your API Keys

- **OpenAI API Key**: [platform.openai.com](https://platform.openai.com/api-keys)
- **Serper API Key**: [serper.dev](https://serper.dev/)

## 📖 Usage

### Running the Jupyter Notebook

```bash
jupyter notebook L7_job_application_crew.ipynb
```

### Programmatic Usage

```python
from crewai import Agent, Task, Crew
from utils import get_openai_api_key, get_serper_api_key
import os

# Set up environment
openai_api_key = get_openai_api_key()
os.environ["OPENAI_MODEL_NAME"] = 'gpt-4-turbo'
os.environ["SERPER_API_KEY"] = get_serper_api_key()

# Define your inputs
job_application_inputs = {
    'job_posting_url': 'https://example.com/job-posting',
    'github_url': 'https://github.com/yourusername',
    'personal_writeup': '''
        I am a passionate software engineer with 5 years of experience
        in full-stack development, specializing in Python and React...
    '''
}

# Run the crew
result = job_application_crew.kickoff(inputs=job_application_inputs)
```

### Input Parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| `job_posting_url` | URL of the job posting | `https://company.com/careers/123` |
| `github_url` | Your GitHub profile URL | `https://github.com/yourusername` |
| `personal_writeup` | Brief description of yourself | Your career summary and goals |

### Output Files

After execution, you'll find two files:

1. **`tailored_resume.md`** - Your customized resume
2. **`interview_materials.md`** - Interview prep materials

## 👥 Agents & Their Roles

### 1. 🔍 Tech Job Researcher

**Role**: Analyzes job postings to extract requirements

**Capabilities**:
- Scrapes job posting websites
- Extracts key skills and qualifications
- Categorizes requirements by importance
- Identifies technical and soft skills needed

**Tools Used**:
- Web Scraper
- Serper Search

---

### 2. 👤 Personal Profiler

**Role**: Creates comprehensive candidate profiles

**Capabilities**:
- Analyzes GitHub repositories and contributions
- Extracts skills from resume
- Synthesizes personal writeup
- Identifies key strengths and experiences

**Tools Used**:
- Web Scraper
- Serper Search
- PDF Search Tool
- File Reader

---

### 3. 📄 Resume Strategist

**Role**: Tailors resumes to match job requirements

**Capabilities**:
- Updates summary to highlight relevant experience
- Rephrases work experience to match job keywords
- Emphasizes relevant skills
- Optimizes for ATS systems
- **Never fabricates information**

**Tools Used**:
- Web Scraper
- Serper Search
- PDF Search Tool
- File Reader

---

### 4. 💼 Interview Preparer

**Role**: Generates interview materials

**Capabilities**:
- Creates potential interview questions
- Develops talking points for key experiences
- Suggests how to discuss skills and projects
- Prepares answers to common questions
- Aligns preparation with job requirements

**Tools Used**:
- Web Scraper
- Serper Search
- PDF Search Tool
- File Reader


## 📁 Project Structure

```
Agentic-Job-Hunter/
│
├── L7_job_application_crew.ipynb  # Main notebook
├── utils.py                        # Utility functions
├── .env                            # API keys (not tracked)
├── .gitignore                      # Git ignore file
│
├── YOUR_CV.pdf                     # Your resume (not tracked)
│
├── tailored_resume.md              # Generated output (not tracked)
├── interview_materials.md          # Generated output (not tracked)
│
└── README.md                       # This file
```


## 🙏 Acknowledgments

- [CrewAI](https://crewai.com) - Multi-agent orchestration framework
- [OpenAI](https://openai.com) - GPT-4 Turbo language model
- [Serper](https://serper.dev) - Web search API


---

<div align="center">

**🎯 Land Your Dream Job with AI-Powered Applications**

Made with ❤️ by developers, for developers

[Report Bug](https://github.com/iitsh/Agentic-Job-Hunter/issues) · [Request Feature](https://github.com/iitsh/Agentic-Job-Hunter/issues) · [Documentation](https://github.com/iitsh/Agentic-Job-Hunter/wiki)

</div>
