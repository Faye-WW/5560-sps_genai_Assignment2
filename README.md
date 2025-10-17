SPS GenAI API
1. Project Overview
This project extends the FastAPI application from Assignment 1 by adding a Convolutional Neural Network (CNN) image classifier trained on CIFAR-10, while still supporting spaCy embeddings. The API can run locally or via Docker.

2. Features
Word embedding using spaCy
Sentence embedding + cosine similarity
Image classification API using CNN (CIFAR-10)
Docker deployment
Organized helper library for model training

3. Environment Setup
Clone the repository
```bash
git clone https://github.com/Faye-WW/5560-sps_genai_Assignment2.git
cd 5560-sps_genai_Assignment2
```
Create a virtual environment
```bash
python3 -m venv .venv
source .venv/bin/activate       # Mac/Linux
.\.venv\Scripts\activate        # Windows
```
Install dependencies
```bash
pip install -r requirements.txt
python -m spacy download en_core_web_md
```

4. Train the CNN Model (CIFAR-10)
Before classification, train the CNN model:
```
python -m app.train_cnn
```
This will generate:
```
models/cnn.pt
```

5. Run the Server

From the project root directory, run:

`uvicorn app.main:app --reload`

You should see something like:

`Uvicorn running on http://127.0.0.1:8000`

4. Test the API

Method 1: Swagger UI (Recommended)

Go to 👉 http://127.0.0.1:8000/docs

You can explore and test all endpoints interactively.

Method 2: Using curl

(1) Word embedding
```bash
curl -X POST "http://127.0.0.1:8000/embed/word" \
     -H "Content-Type: application/json" \
     -d '{"word":"apple"}'
```

(2) Sentence embedding
```bash
curl -X POST "http://127.0.0.1:8000/embed/sentence" \
     -H "Content-Type: application/json" \
     -d '{"text":"Hello world"}'
```

(3) Batch sentence embeddings
```bash
curl -X POST "http://127.0.0.1:8000/embed/sentence" \
     -H "Content-Type: application/json" \
     -d '{"texts":["Hello world","Good morning"]}'
```

(4) Word similarity
```bash
curl -X POST "http://127.0.0.1:8000/similarity/words" \
     -H "Content-Type: application/json" \
     -d '{"a":"king","b":"queen"}'
```

(5) Sentence similarity
```bash
curl -X POST "http://127.0.0.1:8000/similarity/sentences" \
     -H "Content-Type: application/json" \
     -d '{"a":"I love apples","b":"I enjoy oranges"}'
```

5. Project Structure
```text
sps_genai/
├── app/
│   ├── embeddings.py    # spaCy embedding functions
│   └── main.py          # FastAPI entry point
│
├── README.md
├── requirements.txt
└── .gitignore
```

6. Notes

Always activate the .venv environment before running the server.

If you see (base) from Anaconda, deactivate it first:
```bash
conda deactivate
source .venv/bin/activate
```

