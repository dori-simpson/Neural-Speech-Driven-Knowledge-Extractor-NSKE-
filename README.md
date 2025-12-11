# Neural-Speech-Driven-Knowledge-Extractor-NSKE-



```markdown
# Video Intelligence Pipeline
A fully automated pipeline that ingests videos from Amazon S3, transcribes speech into text, cleans and normalizes the text, extracts key phrases and named entities using AWS Comprehend, and loads the results into Amazon OpenSearch for visualization through Kibana.

This project demonstrates an end-to-end **AI-powered video understanding system** using Python, AWS services, and Jupyter notebooks.

---

#  Features

- **Video ingestion** from Amazon S3  
- **Automatic transcription** using AWS Transcribe  
- **Text normalization and cleaning**  
- **Key phrase extraction** (topics, concepts)  
- **Named entity extraction** (locations, organizations, people)  
- **Data merging and structuring with Pandas**  
- **Indexing into OpenSearch**  
- **Search & dashboard visualization** in Kibana  
- **Fully automated pipeline** from raw video → insights dashboard  

---

#  Architecture

```

S3 (videos)
↓
AWS Transcribe
↓
S3 (transcriptions)
↓
Text Cleaning (Python, NLTK)
↓
AWS Comprehend
↓
Key Phrases + Entities
↓
Merged DataFrame
↓
Amazon OpenSearch
↓
Kibana Dashboard

```

---

#  Technologies Used

- **Python**
- **Jupyter Notebook**
- **AWS S3**
- **AWS Transcribe**
- **AWS Comprehend**
- **AWS IAM**
- **Amazon OpenSearch Service**
- **Kibana**
- **Pandas, NumPy, Matplotlib**
- **NLTK for NLP preprocessing**

---

 # Here is a simple explanation of each part of this code using python and Jupyter notebooks. Everyone needs a refresher!


# **PART 1 — Getting the videos**

```bash
!aws s3 cp ...
````

Think of S3 like a big toy box in the cloud.
This command copies videos from one box to your own box so you can use them.

---

# **PART 2 — Listing What’s in S3**

```python
conn = client('s3')
for key in conn.list_objects(...):
    print(key['Key'])
```

This looks inside your S3 bucket and prints the names of the videos.

---

# **PART 3 — Importing Tools**

```python
import boto3, numpy, pandas, ...
```

These are all helpers:

* boto3 → talk to AWS
* pandas → work with tables
* matplotlib → create charts
* nltk → work with words
* uuid → create random job names
* re → clean text
* stopwords / tokenizer / stemmer → language cleaning

---

# **PART 4 — Turning Videos into Text (Transcribing)**

```python
transcribe_client.start_transcription_job(...)
```

This tells AWS Transcribe:
“Listen to this video and write down everything it says.”

---

# **PART 5 — Storing Output Filenames**

```python
output_files = []
```

This list remembers which text file came from which video.

---

# **PART 6 — Normalizing the Text**

```python
def normalize_text(content):
    ...
```

This "washes" the text:

* removes links
* makes letters lowercase
* fixes spacing
* removes stray symbols

---

# **PART 7 — Preparing Text for Comprehend**

```python
upload_comprehend_s3_csv(...)
```

Comprehend is a robot that reads text and finds important ideas.
You upload cleaned text into S3 in CSV form so Comprehend can read it.

---

# **PART 8 — Extracting Key Phrases**

```python
start_key_phrases_detection_job(...)
```

This tells Comprehend:
“Find the important ideas in each line.”

---

# **PART 9 — Waiting for Comprehend**

```python
while ... != 'COMPLETED':
    sleep(10)
```

You check every 10 seconds until the job is done.

---

# **PART 10 — Getting the Results**

```python
download_file(...)
tarfile.open(...)
```

This downloads Comprehend's results (in a zip-like tar file), opens it, and extracts the output.

---

# **PART 11 — Extracting Names, Places, Organizations**

```python
extract_entities(...)
```

This finds:

* people
* places
* organizations
* more

It’s like circling special words in a story.

---

# **PART 12 — Merging All Data Into One Table**

```python
mergedDf = df.merge(...)
```

You combine:

* transcription
* key phrases
* locations
* organizations

into one clean dataset.

---

# **PART 13 — Creating the OpenSearch Domain**

```python
es_client.create_elasticsearch_domain(...)
```

This builds a search engine (like your own private Google) for exploring the results.

---

# **PART 14 — Waiting for the Domain**

Like waiting for a machine to warm up.

---

# **PART 15 — Indexing Into OpenSearch**

```python
helpers.bulk(...)
```

Uploads everything into OpenSearch so you can:

* search
* filter
* visualize

---

# **PART 16 — Opening Your Dashboard**

```python
print(f'https://{es_endpoint}/_plugin/kibana')
```

This gives you a link to Kibana where you can explore:

* charts
* keywords
* transcripts
* entities
* insights

---

#  **Example Use Cases**

* Media companies analyzing large video archives
* Automatic metadata generation
* Customer call-center insights
* Lecture/video content understanding
* Research projects involving speech-to-text + NLP
* Semantic search over audio/video files










