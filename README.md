# **Background Removal App** - Transparent Images

This project provides a robust and scalable solution for removing image backgrounds, generating transparent PNG outputs. The application is containerized with Docker and deployed on **Google Cloud Run**, ensuring high availability, accessibility, and easy scaling.

## **Features**

- **Background Removal**: Effortlessly removes the background from uploaded images.
- **Transparent PNG Output**: Produces high-quality PNG images with transparent backgrounds.
- **Scalable Deployment**: Designed for production with scalable deployment on Google Cloud Run.

---

## **Demo**

Access the live application:  
👉 [Background Removal App](https://remover-934068568901.us-central1.run.app/)  

Below is a preview of the app interface:  

<img src="https://github.com/lakkawardhananjay/bg-removes/assets/92675267/70ebd127-1db3-4309-b1aa-8f1ec36e916a" width="200" />
<img src="https://github.com/lakkawardhananjay/bg-removes/assets/92675267/12c836fc-625b-466d-a06f-dfa0c04f7fa0" width="200" />
<img src="https://github.com/lakkawardhananjay/bg-removes/assets/92675267/4fd740c1-4610-4929-aed5-9d845ebd9206" width="200" />
<img src="https://github.com/lakkawardhananjay/bg-removes/assets/92675267/6a7b5d9f-b280-4c6c-a853-a6a6bf8b49f5" width="200" />

---

## **Prerequisites**

Ensure the following are installed and configured:  
- Python 3.8 or later  
- Docker and Docker Compose  
- Google Cloud SDK (for deployment)  

---

## **Installation for Local Development**

Follow these steps to set up the project for local development:

1. Clone this repository:
   ```bash
   git clone https://github.com/lakkawardhananjay/bg-removes.git
   cd bg-removes
   ```

2. Install project dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run the container locally:
   ```bash
   docker-compose up
   ```

4. Access the API locally:  
   Use the endpoint: `http://localhost:5000/remove_background`

---

## **API Usage**

### **Endpoint**

- **POST**: `http://<host>:<port>/remove_background`

### **Request Format**

Send a JSON payload containing the base64-encoded image data:
```json
{
  "image_data": "base64_encoded_image_data"
}
```

### **Response Format**

The API responds with a JSON payload containing the processed image data:
```json
{
  "processed_image_data": "base64_encoded_PNG_data"
}
```

### Example Request (Using cURL):
```bash
curl -X POST http://localhost:5000/remove_background \
-H "Content-Type: application/json" \
-d '{
  "image_data": "<base64_encoded_image>"
}'
```

---

## **Deployment to Google Cloud**

This project uses **Google Cloud Artifact Registry** and **Cloud Run** for deployment. Follow the steps below for production deployment:

### **Pre-requisites**

1. Google Cloud project with the following services enabled:
   - Artifact Registry
   - Cloud Run

2. Install and authenticate the Google Cloud SDK:
   ```bash
   gcloud auth login
   gcloud auth configure-docker [REGION]
   ```

### **Steps for Deployment**

1. Build the Docker image:
   ```bash
   docker-compose build
   ```

2. Tag and push the image to **Artifact Registry**:
   ```bash
   docker tag <IMAGE_ID> gcr.io/[PROJECT_ID]/background-removal:latest
   docker push gcr.io/[PROJECT_ID]/background-removal:latest
   ```

   Replace:
   - `<IMAGE_ID>`: Docker image ID from `docker images`.
   - `[PROJECT_ID]`: Your Google Cloud Project ID.

3. Deploy the application to **Cloud Run**:
   ```bash
   gcloud run deploy background-removal \
     --image gcr.io/[PROJECT_ID]/background-removal:latest \
     --platform managed \
     --region [REGION] \
     --allow-unauthenticated
   ```

   Replace:
   - `[PROJECT_ID]`: Your Google Cloud Project ID.
   - `[REGION]`: Your preferred Google Cloud region (e.g., `us-central1`).

4. After successful deployment, note the service URL provided by Cloud Run. Use this URL to access the API.

---

## **Production API Reference**

### **Endpoint**

- **POST**: `https://<cloud_run_service_url>/remove_background`

Replace `<cloud_run_service_url>` with your Cloud Run service URL.

### **Request & Response**

Use the same format as described in the [API Usage](#api-usage) section.

---

## **Contributing**

We welcome contributions from the community! To get started:
- Fork this repository.
- Create a new feature branch.
- Submit a pull request with detailed descriptions of your changes.

For major changes, please open an issue first to discuss your proposal.

---

## **License**

This project is licensed under the [MIT License](LICENSE).  

Feel free to use, modify, and distribute it in personal or commercial projects.  
