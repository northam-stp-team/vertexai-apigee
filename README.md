## [Work in progress]
## Intro

This demo shows how to productionalize machine learning models using [Vertex AI Prediction](https://cloud.google.com/vertex-ai/docs/predictions/getting-predictions) and [Apigee](https://cloud.google.com/apigee).

![Architecture](/images/vertexai_apigee_architecture.png)

By using Apigee with VertexAI, customers can create enterprise single and multi-tenant machine learning systems that autoscale, monitor, observe and monetize machine learning models with lower upfront opex investment and faster go-to-market rates. 

On top of this, this solution bridges the gap between technical and business teams by building business intelligence dashboards to help in troubleshooting bottlenecks and consumption broadly or per tenant. BQML can be integrated to forecast usage for future resource planning or for anomaly detection.

In this demo, we'll first build an English to Spanish translation model with a sequence-to-sequence Transformer and deploy it to a Vertex AI endpoint for online prediction. By using Vertex AI Prediction endpoints, we get managed infrastrcture that is both scalable and fault tolerant for which we use to serve our machine learning models.

After the model has been deployed, we'll create an Apigee reverse proxy which we'll use as an API gateway to serve our model. By using Apigee, we create a multi-tenant enterprise ready solution facade for our machine learning APIs and provides security, rate limiting, quotas, analytics and more.

## Setup

[Optional]
If you would like to use the pretrained model instead of training your own then before cloning this repo make sure you have installed [git lsf](https://git-lfs.github.com/) and ran the command `git lfs install`, then clone the repo. This is so that the model weights are downloaded correctly when cloning the repo.

1. You'll need to enable the following apis:
    - Vertex AI
    - Compute
    - Container registry

    You can do it in one command using the [gcloud cli](https://cloud.google.com/sdk/docs/install)

    ```bash
    gcloud services enable compute.googleapis.com \
        containerregistry.googleapis.com  \
        aiplatform.googleapis.com
    ```

1. If you would like to build, train and deploy the model from scratch, you can run through the [Seq2SeqTranslation.ipyb notebook](/notebooks/Seq2SeqTranslation.ipynb).