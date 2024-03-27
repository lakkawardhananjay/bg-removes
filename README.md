## Background Removal APP - Transparent Images

This project provides a Python API for removing backgrounds from images and making them transparent. The application is containerized and deployed on Google Cloud Run, allowing for easy scaling and accessibility.

### Features

* Removes background from uploaded images.
* Generates transparent PNG output.
* Scalable deployment on Google Cloud Run.

### Prerequisites

<img src="https://github.com/lakkawardhananjay/bg-removes/assets/92675267/70ebd127-1db3-4309-b1aa-8f1ec36e916a" width="200" /> <img src="https://github.com/lakkawardhananjay/bg-removes/assets/92675267/12c836fc-625b-466d-a06f-dfa0c04f7fa0" width="200" /> <img src="https://github.com/lakkawardhananjay/bg-removes/assets/92675267/4fd740c1-4610-4929-aed5-9d845ebd9206" width="200" /> <img src="https://github.com/lakkawardhananjay/bg-removes/assets/92675267/6a7b5d9f-b280-4c6c-a853-a6a6bf8b49f5" width="200" />


### Installation (Local Development)

1. Clone this repository.
2. Install dependencies:

```bash
pip install -r requirements.txt
```

### Usage

1. Run the container locally:

```bash
docker-compose up
```

2. Send a POST request to `http://localhost:5000/remove_background` with the following format:

```json
{
  "image_data": "base64_encoded_image_data"
}
```

3. The API will respond with the processed image data in PNG format with a transparent background.

**Note:** This is for local development only. Refer to the deployment section for production use.

### Deployment (Google Cloud)

This project leverages Google Cloud Artifact Registry and Cloud Run for deployment. 

**Requirements:**

* A Google Cloud Project with Artifact Registry and Cloud Run enabled.

**Steps:**

1. Configure your Google Cloud project and obtain necessary credentials.
2. Build and push the Docker image to your Artifact Registry:

```bash
docker-compose build
gcloud auth configure-docker [REGION]
gcloud docker -- TAG gcr.io/[PROJECT_ID]/background-removal:latest
gcloud docker -- PUSH gcr.io/[PROJECT_ID]/background-removal:latest
```

**Replace:**

* `[REGION]` with your Google Cloud region (e.g., us-central1)
* `[PROJECT_ID]` with your actual project ID

3. Deploy the application to Cloud Run:

```bash
gcloud run deploy background-removal \
  --image gcr.io/[PROJECT_ID]/background-removal:latest \
  --platform managed \
  --region [REGION] \
  --allow-unauthenticated
```

**Replace:**

* `[REGION]` with your Google Cloud region (e.g., us-central1)
* `[PROJECT_ID]` with your actual project ID

4. After successful deployment, the API endpoint will be available in the Cloud Run service URL.

### API Reference

* **Endpoint:** `POST http://<cloud_run_service_url>/remove_background`
* **Request Body:**

```json
{
  "image_data": "base64_encoded_image_data"
}
```

* **Response:**

```json
{
  "processed_image_data": "base64_encoded_PNG_data"
}
```

**Note:** Replace `<cloud_run_service_url>` with the actual URL provided by Cloud Run after deployment.

### Contributing

We welcome contributions to this project. Please refer to the contributing guidelines (to be added) before submitting pull requests.

### License

