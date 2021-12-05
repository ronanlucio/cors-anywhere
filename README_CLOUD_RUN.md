# Deploying CORS-AnyWhere to Google Cloud Run

## Enable Cloud Run API

```
gcloud services list --available
gcloud services enable run.googleapis.com
```

## Set default region

```
gcloud run regions list
gcloud config set run/region us-central1
```


## Deploying to Cloud Run from source

1. Add a "start" entry to "scripts" block on package.json file

    Example:

    ```
    "scripts": {
        "start": "node index.js"
    },
    ```

2. Execute a "gcloud run deploy"

```
gcloud run deploy cors-anywhere --update-env-vars CORSANYWHERE_WHITELIST='https://your-origin-website'
```

## Building and Deploying

Alternatively, you can build and deploy your image to Cloud Run.
This can be necessary in case you're using a external CI/CD tool.

### Configure Docker to build containers locally

```
gcloud auth configure-docker
gcloud components install docker-credential-gcr
```

### Build container image

```
gcloud builds submit --tag cors-anywhere:0.4.4 .
```

### Deploy it to Cloud Run

```
gcloud run deploy cors-anywhere --image cors-anywhere:0.4.4
```
