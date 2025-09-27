# Instructor RAG Chatbot

A Retrieval-Augmented Generation (RAG) chatbot that answers questions about instructors using CSV data and displays relevant instructor images. The system uses semantic search with FAISS and OpenAI's GPT models to provide contextual, accurate responses about instructor information.

## Features

- **Semantic Search**: Uses sentence transformers and FAISS for efficient similarity search
- **Dynamic Image Display**: Automatically shows instructor photos based on query context
- **RAG Architecture**: Combines retrieval and generation for accurate, context-aware responses
- **Interactive UI**: Built with Gradio for easy web-based interaction
- **Identity Resolution**: Smart detection of which instructor is being discussed

---

## 📂 Project Structure

```
your-project/
├── data/
│   └── instructors.csv          # Instructor data file
├── images/
│   ├── instructor1.jpg          # Instructor photos
│   ├── instructor2.jpg
│   └── instructor3.jpg
└── chatbot.py                   # Main application code
```

---

## 🛠️ Requirements

### Python Version
- Python 3.8 or later

### Required Packages
Install dependencies using pip:
```bash
pip install pymupdf faiss-cpu sentence-transformers gradio matplotlib seaborn openai
```

### Additional Requirements
- **OpenAI API Key**: Required for GPT model access
- **CSV Data File**: Instructor data with required columns
- **Image Files**: Photos of instructors for display

---

## 🚀 Setup Instructions

### 1. Clone/Download the Code
Save the provided Python code as `chatbot.py` in your project directory.

### 2. Set Your OpenAI API Key
Update the API key in the code:
```python
os.environ["OPENAI_API_KEY"] = "your-actual-openai-api-key-here"
```

### 3. Prepare Your Data Files

**CSV File Format (`data/instructors.csv`):**
Your CSV must include these columns:
- `name`: Full instructor name
- `title`: Job title
- `company`: Company/organization
- `skills`: Technical skills (comma-separated)
- `bio`: Biography/description
- `fun_things`: Fun facts or interesting information
- `linkedin_url`: LinkedIn profile URL

**Example CSV:**
```csv
name,title,company,skills,bio,fun_things,linkedin_url
John Smith,Senior Developer,Tech Corp,"Python,JavaScript,React","Experienced developer with 10+ years","Plays guitar and loves hiking",https://linkedin.com/in/johnsmith
Jane Doe,Data Scientist,AI Solutions,"Python,ML,TensorFlow","PhD in Computer Science, AI researcher","Marathon runner and coffee enthusiast",https://linkedin.com/in/janedoe
```

### 4. Update Configuration
Modify these sections in the code to match your data:

**File Paths:**
```python
CSV_FILE = "data/instructors.csv"

INSTRUCTOR_IMAGES = {
    "instructor1": "images/john_smith.jpg",
    "instructor2": "images/jane_doe.jpg",
    # Add more as needed
}
```

**Name Mappings:**
```python
NAME_TO_KEY = {
    "John Smith": "instructor1",
    "Jane Doe": "instructor2",
    # Must match names in your CSV
}

INSTRUCTOR_ALIASES = {
    "instructor1": [r"\bjohn\b", r"\bsmith\b", r"john\s+smith"],
    "instructor2": [r"\bjane\b", r"\bdoe\b", r"jane\s+doe"],
    # Add regex patterns to detect each instructor
}
```

---

## 🏃‍♂️ How to Run

1. **Execute the Script**
   ```bash
   python chatbot.py
   ```

2. **Access the Interface**
   - The Gradio interface will launch automatically
   - Open the provided local URL in your browser
   - A public sharing URL will also be generated

3. **Start Chatting**
   - Ask questions about your instructors
   - The chatbot will display relevant instructor photos
   - Conversation history is maintained during the session

---

## 🎯 Usage Examples

Try asking questions like:
- "What are John's technical skills?"
- "Tell me about Jane's background"
- "What are some fun facts about our instructors?"
- "Who has experience with machine learning?"
- "Compare the backgrounds of all instructors"

The chatbot will:
- Search the CSV data semantically
- Generate contextual responses using OpenAI
- Display the relevant instructor's photo
- Only answer from the provided data

---

## 🔧 Configuration Options

### Model Settings
```python
EMBEDDING_MODEL_NAME = "all-MiniLM-L6-v2"  # Sentence transformer model
OPENAI_MODEL = "gpt-4o-mini"               # GPT model for generation
RETRIEVE_K = 3                             # Number of chunks to retrieve
MAX_TOKENS = 350                           # Response length limit
```

### Customizing Identity Detection
Add more patterns to help the system recognize instructor names:
```python
INSTRUCTOR_ALIASES = {
    "instructor1": [
        r"\bjohn\b", 
        r"\bsmith\b", 
        r"john\s+smith",
        r"senior\s+developer"  # Can include titles too
    ],
}
```

---

## 🏗️ How It Works

1. **Data Processing**: CSV rows are converted into structured text chunks
2. **Embedding**: Text chunks are encoded using sentence transformers
3. **Indexing**: FAISS index enables fast similarity search
4. **Query Processing**: User questions are encoded and matched against the index
5. **Response Generation**: OpenAI GPT generates answers using retrieved context
6. **Image Selection**: System determines which instructor photo to display based on context

---

## 🚨 Troubleshooting

**Common Issues:**

1. **"Please set OPENAI_API_KEY" Error**
   - Update the API key in the code
   - Ensure your OpenAI account has sufficient credits

2. **"FileNotFoundError" for CSV or Images**
   - Check that file paths are correct
   - Ensure files exist in the specified locations

3. **No Images Displayed**
   - Verify image file paths in `INSTRUCTOR_IMAGES`
   - Check that image files exist and are readable
   - Ensure `NAME_TO_KEY` mappings match CSV names exactly

4. **Poor Response Quality**
   - Add more detailed information to your CSV
   - Adjust `RETRIEVE_K` to retrieve more/fewer context chunks
   - Update instructor aliases for better name detection

---

## 💡 Tips for Better Results

- **Rich Data**: Include detailed biographies and diverse information in your CSV
- **Clear Names**: Use consistent naming in your CSV and mappings
- **Good Images**: Use clear, professional photos for better visual experience
- **Specific Queries**: More specific questions often yield better responses
- **Regular Updates**: Keep your instructor data current for best results

---

## 🔒 Security Notes

- Keep your OpenAI API key secure and never commit it to version control
- Consider using environment variables for sensitive configuration
- The system only answers from provided data, limiting information exposure

---

## 📄 License

This project is provided for educational and demonstration purposes. Ensure you have appropriate rights to use instructor data and images.
