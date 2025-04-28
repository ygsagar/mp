#  Vulnerability Detection VS Code Extension

A real-time vulnerability detection tool integrated into Visual Studio Code.  
Detects vulnerabilities as you write Python code by connecting to a machine learning API.

---

##  Quickstart

1. **Clone the repository**:
    ```bash
    git clone https://github.com/your-username/vulnerability-detection.git
    cd vulnerability-detection
    ```

2. **Run the Flask API locally** *(or deploy to Google Cloud Run)*.

3. **Update the API URL** inside the VS Code extension.

4. **Launch and test the extension**!

---

##  Project Structure

```plaintext
vulnerability-detection/
├── api/              # Flask API backend
├── extension/        # VS Code extension
├── README.md         # Project instructions
├── Dockerfile        # Dockerfile for API
├── requirements.txt  # Python dependencies
└── ...
` ``` `


## Running the API Locally

Follow these steps to run the Flask API on your machine:

1. Navigate to the API folder:

    ```bash
    cd api/
    ```

2. Create a virtual environment:

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3. Install the required Python packages:

    ```bash
    pip install -r requirements.txt
    ```

4. Run the Flask server:

    ```bash
    python app.py
    ```

5. The server will be available at:

    ```
    http://127.0.0.1:5000/
    ```

---

##  Deploying the API to Google Cloud Run

Follow these steps to deploy your API to the cloud:

1. Authenticate to Google Cloud:

    ```bash
    gcloud auth login
    gcloud config set project YOUR_PROJECT_ID
    ```

2. Enable the required services:

    ```bash
    gcloud services enable run.googleapis.com
    gcloud services enable containerregistry.googleapis.com
    ```

3. Build the Docker image:

    ```bash
    docker build -t vulnerability-detection-api .
    ```

4. Tag the Docker image:

    ```bash
    docker tag vulnerability-detection-api gcr.io/YOUR_PROJECT_ID/vulnerability-detection-api
    ```

5. Push the Docker image to Google Container Registry:

    ```bash
    docker push gcr.io/YOUR_PROJECT_ID/vulnerability-detection-api
    ```

6. Deploy the image to Google Cloud Run:

    ```bash
    gcloud run deploy vulnerability-detection-api \
      --image gcr.io/YOUR_PROJECT_ID/vulnerability-detection-api \
      --platform managed \
      --region YOUR_REGION \
      --allow-unauthenticated
    ```

7. After deployment, note the public API URL, e.g.:

    ```
    https://vulnerability-detection-api-xyz.a.run.app/
    ```

---

## 🛠 Setting Up the VS Code Extension

Follow these steps to run the extension locally:

1. Navigate to the extension folder:

    ```bash
    cd extension/
    ```

2. Install Node.js dependencies:

    ```bash
    npm install
    ```

3. Update the API URL:

    - Open `src/extension.ts`.
    - Replace the existing API URL with your deployed URL:

    ```typescript
    const API_URL = 'https://YOUR_CLOUD_RUN_URL/predict';
    ```

4. Compile the extension:

    ```bash
    npm run compile
    ```

5. Launch the extension:

    - Press `F5` inside Visual Studio Code.
    - A new **Extension Development Host** window will open.
    - Open a Python file and start writing code — vulnerabilities will be detected in real-time!

---

