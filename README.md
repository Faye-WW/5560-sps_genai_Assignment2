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

6. Test the API   
Method 1: Swagger UI (Recommended)  
Go to http://127.0.0.1:8000/docs   
You can explore and test all endpoints interactively.  

Method 2: Using curl  
Upload an image and classify  
```bash
curl -X POST "http://127.0.0.1:8000/classify/image" \
  -H "accept: application/json" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@cat.jpg"
```

7. Run with Docker  
Build image:  
```
docker build -t sps-genai .
```
Run container (mount model file):  
```
docker run -p 8000:8000 -v $(pwd)/models:/app/models sps-genai
```
Access API:  
http://127.0.0.1:8000/docs  

8. Project Structure  
```text
sps_genai/
│
├── app/
│   ├── main.py           # FastAPI API
│   ├── embeddings.py     # spaCy embeddings
│   ├── inference.py      # CNN prediction
│   └── train_cnn.py      # CNN training
│
├── helper_lib/           # CNN helper modules
│   ├── model.py          # CNN architecture
│   ├── trainer.py        # training loop
│   ├── data_loader.py    # CIFAR10 loader
│   └── utils.py
│
├── models/               # cnn.pt saved model (ignored by Git)
├── Dockerfile
├── requirements.txt
├── .gitignore
└── README.md
```

9. Notes  
Always activate the .venv environment before running the server.  
If you see (base) from Anaconda, deactivate it first:  
```bash
conda deactivate
source .venv/bin/activate
```




