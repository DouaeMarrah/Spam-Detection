# Spam Detection System

## Project Overview

This project implements a simple spam detection system that leverages machine learning models and the distributed NoSQL database Apache Cassandra. It is designed to classify emails as spam or non-spam in real-time using natural language processing (NLP) techniques. The system features a web API for seamless integration with external applications.

##  Demonstration

A video demonstration is available, showcasing the system's functionality:

- **Real-time Interaction:** See how the web interface processes email content instantly.
- **Live Prediction:** Watch the system classify sample messages (e.g., "Hello, do you want to meet tomorrow?" vs. "Congratulations, you've won 100K!") as "Spam" or "Not Spam".
- **Full Workflow:** The video covers the entire process, from launching the application to receiving and interpreting results.

*(The video file is included in the project repository or available for download separately.)*

## Features

- **Real-time Spam Detection:** Classify incoming emails instantly using a trained Naïve Bayes model.
- **Scalable Data Storage:** Utilizes Apache Cassandra for distributed, high-availability storage of email data and predictions.
- **RESTful API:** Built with Flask to allow external applications to submit emails for classification via a simple HTTP POST request.
- **Continuous Improvement:** The architecture supports model retraining using the growing historical data stored in Cassandra.
- **Containerized Deployment:** Docker and Docker Compose are used for easy and consistent setup and deployment.

## Technologies Used

- **Python:** Core language for data processing, model training, and API development.
- **Apache Cassandra:** NoSQL database for scalable and high-performance data storage.
- **Docker & Docker Compose:** For containerization and managing multi-container applications.
- **Flask:** Micro web framework for building the REST API and serving the web interface.
- **Scikit-learn:** For the machine learning model (`MultinomialNB`) and text vectorization (`CountVectorizer`).
- **NLTK:** For natural language processing tasks (stopword removal, lemmatization).
- **Cassandra Driver:** The `cassandra-driver` library for connecting Python to the Cassandra database.

## Project Architecture

1.  **Data Storage (Cassandra):**
    *   Emails and their labels (`spam`/`ham`) are stored in a table named `messages`.
    *   The system is designed to easily scale with increasing data volume.

2.  **Data Processing & Model Training (Python):**
    *   Emails are fetched from Cassandra, cleaned, and preprocessed (removing special characters, lemmatization, stopword removal).
    *   The text is vectorized using a Bag-of-Words model with bigrams.
    *   A Naïve Bayes classifier is trained on the processed data.

3.  **Real-Time Prediction (Flask API):**
    *   A web server receives email content via a JSON request.
    *   The received text undergoes the same preprocessing pipeline.
    *   The trained model predicts the class (`spam` or `not spam`).
    *   The result is returned as a JSON response.

## Installation & Setup

### Prerequisites

- **Docker**
- **Docker Compose**
- **Python 3.8+** and **pip** (if not using Docker for the Python app)

### Method 1: Using Docker Compose (Recommended)

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd spam-detection-cassandra
    ```

2.  **Start the services:** This command will start both Cassandra and the Flask application.
    ```bash
    docker-compose up
    ```

3.  **Initialize the Database (in a new terminal):**
    *   Run the script to create the keyspace, table, and import data from `spam.csv`.
    ```bash
    # If using Python locally
    python init_cassandra.py
    python import_data.py
    # Or if the scripts are also containerized, use docker exec
    ```

### Method 2: Manual Setup

1.  **Start Cassandra with Docker:**
    ```bash
    docker run --name cassandra -d -p 9042:9042 cassandra:latest
    ```

2.  **Install Python dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Initialize Cassandra and Import Data:**
    ```bash
    python init_cassandra.py
    python import_data.py
    ```

4.  **Run the Flask application:**
    ```bash
    python app.py
    ```



## File Structure

├── app.py # Main Flask application
├── train_model.py # Script for training the ML model
├── init_cassandra.py # Script to create the Cassandra keyspace and table
├── import_data.py # Script to import data from spam.csv into Cassandra
├── spam.csv # Example dataset for training (not provided here)
├── templates/
│ └── index.html # Simple web interface HTML file
├── requirements.txt # Python dependencies
├── docker-compose.yml # Docker Compose configuration
└── Report.pdf # Full project report (in French)

## Future Enhancements

- Integrate a more advanced model like DistilBERT for improved contextual understanding.
- Add support for multilingual spam detection.
- Implement user feedback to improve the model continuously (active learning).
- Develop a more sophisticated front-end interface.


 **The detailed project report (in French) is available in the file `rapport.pdf`.**
