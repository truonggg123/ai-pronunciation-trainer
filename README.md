# SpeakMaster AI 🎙️

> **An AI-powered English pronunciation trainer and intelligent dictionary built with Dynamic Programming, Trie data structure, OpenAI Whisper, and SQL Server.**

---

## 📌 Overview

**SpeakMaster AI** is an interactive, full-stack educational desktop/web application inspired by Elsa Speak. The project combines state-of-the-art speech recognition with foundational Data Structures and Algorithms (DSA) to deliver real-time pronunciation assessment, phoneme alignment, autocomplete word suggestion, and personalized progress tracking.

Developed as a collaborative academic project for the **Data Structures and Algorithms (DSA)** curriculum (Spring 2026), SpeakMaster emphasizes **ground-up algorithm implementations** (such as dynamic programming for Levenshtein distance and prefix trees for autocompletion) rather than relying exclusively on black-box external packages.

---

## ✨ Key Features

- 🎧 **AI-Powered Pronunciation Evaluation**:
  - Utilizes **OpenAI Whisper** for robust speech-to-text recognition directly from microphone input.
  - Generates clear, native audio models for comparison via **gTTS** (Google Text-to-Speech).
  - Converts text to International Phonetic Alphabet (**IPA**) phonemes using `eng_to_ipa`.

- ⚡ **DSA Core Algorithms (In-House Implementations)**:
  - **Dynamic Programming (Levenshtein Distance)**: Word-level edit distance algorithm implemented with a 2D dynamic programming matrix.
  - **Traceback & Visual Diff**: Backtracking alignment that visualizes pronunciation accuracy with color-coded feedback (🟢 Correct, 🔴 Mispronounced/Missing).
  - **Prefix Tree (Trie)**: High-performance autocomplete engine storing 10,000+ English words for instant search suggestions ($O(L)$ prefix lookup complexity).

- 📖 **Comprehensive English - Vietnamese Dictionary**:
  - Fast SQL-backed dictionary querying over 25,000+ definitions, phonetic notations, word classes, and usage examples.
  - Instant autocomplete search bar with fast interactive suggestions.

- 🔐 **Account & History Management**:
  - Secure user registration and login protected with **SHA-256** password hashing.
  - Stores all attempts, audio similarity metrics, and historical scores in **Microsoft SQL Server** via dedicated stored procedures.

- 🎨 **Modern & Responsive UI**:
  - Sleek interface built with **Gradio** and custom CSS inspired by modern e-learning platforms.
  - Visual circle gauge for overall score, formatted lexical cards, and floating interactive animations.

---




## 📂 Project Structure

```text
Project-Spring26/
├── algorithm.py                  # Custom Levenshtein DP & visual alignment algorithm
├── app.py                        # Main Gradio application entry point
├── auth.py                       # User authentication and password hash management
├── database.py                   # SQL Server connector & stored procedure wrapper
├── dictionary_logic.py           # SQL dictionary querying & word definition retriever
├── history.py                    # History logging and user practice retrieval
├── logic.py                      # Integration layer connecting Whisper, IPA, & DP scoring
├── search_engine.py              # Prefix Tree (Trie) autocomplete implementation
├── research_engine.py            # Extended Trie engine with benchmarks & documentation
├── speech_module.py              # OpenAI Whisper & gTTS audio handler
├── ui_components.py              # Custom CSS styles, components, and HTML formatters
├── setup_database.sql            # Database creation script with schemas & stored procedures
├── setup_dictionary_db.py        # ETL script importing CSV lexicon to SQL Server
├── google-10000-english-usa.txt  # Frequency dictionary corpus for Trie indexing
├── English - Vietnamese.csv      # Bilingual dictionary dataset
├── requirement.txt               # Project Python package dependencies
└── README.md                     # Project documentation
```

---

## ⚙️ Installation & Setup

### 1. Prerequisites

- **Python**: Version `3.10` or higher.
- **Microsoft SQL Server**: Local instance (e.g., SQL Express or Developer edition).
- **ODBC Driver**: [ODBC Driver 17 for SQL Server](https://learn.microsoft.com/en-us/sql/connect/odbc/download-odbc-driver-for-sql-server).
- **FFmpeg**: Required by Whisper and pydub for audio processing.
  - *Windows*: Download from [gyan.dev](https://www.gyan.dev/ffmpeg/builds/), extract, and add the `bin` directory to your `System PATH`.

### 2. Clone the Repository

```bash
git clone https://github.com/truonggg123/Project-Spring26.git
cd Project-Spring26
```

### 3. Create a Virtual Environment & Install Dependencies

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows (PowerShell):
.\venv\Scripts\Activate.ps1
# Windows (cmd):
.\venv\Scripts\activate.bat
# Linux/macOS:
source venv/bin/activate

# Install required packages
pip install -r requirement.txt
```

### 4. Database Setup

1. Open **SQL Server Management Studio (SSMS)** or execute `setup_database.sql` via `sqlcmd`:
   ```bash
   sqlcmd -S localhost -E -i setup_database.sql
   ```
2. *(One-time)* Import the English - Vietnamese dictionary into SQL Server:
   ```bash
   python setup_dictionary_db.py
   ```

### 5. Environment Configuration

You can configure connection parameters via environment variables or use the default local values:

| Variable | Default Value | Description |
| :--- | :--- | :--- |
| `DICT_SQL_SERVER` | `localhost\SQLEXPRESS03` | SQL Server host / instance name |
| `DICT_SQL_DATABASE` | `PronunciationDB` | Database name |
| `MOCK_MODE` | `false` | Set to `true` to bypass Whisper and speed up UI testing |

### 6. Run the Application

```bash
python app.py
```

After starting, navigate to your web browser at:
```text
http://127.0.0.1:7860
```

---

## 🧪 Development & Mock Mode

For development machines without a dedicated GPU or when working strictly on UI/database logic, you can enable **Mock Mode**:

```powershell
$env:MOCK_MODE="true"
python app.py
```

This bypasses OpenAI Whisper model loading while preserving all navigation, dictionary, and account functionality.

---

## 📜 Academic Note

This project is submitted in fulfillment of the coursework requirements for **Project-Spring26**. All core algorithmic elements—including the **2D DP matrix for string editing** and the **Trie structure for prefix search**—were designed and implemented from scratch by the project team.
