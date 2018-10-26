## Flask app for serving Tensorflow trained model

#### Running local

```bash
FLASK_APP=app.py FLASK_DEBUG=1 python -m flask run

curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/flask-tf/samples/edsheeran.jpg" http://localhost:5000/detect_image

curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/flask-tf/samples/bradpitt.jpg" http://localhost:5000/detect_image

curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/flask-tf/samples/brianredmond.jpg" http://localhost:5000/detect_image
```

#### Model in AKS

```bash
IMAGE=edsheeran.jpg
IMAGE=bradpitt.jpg
IMAGE=brianredmond.jpg
IMAGE=ed-sheeran-puppet.jpg

IP=flask-tf.e1b1189837d740fbad69.eastus.aksapp.io && curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/flask-tf/samples/$IMAGE" http://$IP/detect_image

IP=flask-tf.b7c8110bf9aa4867a05d.westeurope.aksapp.io && curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/flask-tf/samples/$IMAGE" http://$IP/detect_image
```

#### Container

```bash
export IMAGE_TAG=3.0

docker build -t chzbrgr71/edsheeran-flask-app:$IMAGE_TAG .

docker push chzbrgr71/edsheeran-flask-app:$IMAGE_TAG

docker run -d --name flask -p 5000:5000 chzbrgr71/edsheeran-flask-app:$IMAGE_TAG
```

#### Helm Install

helm install --name flask-tf --set service.ingressDNSName=flask-tf.e1b1189837d740fbad69.eastus.aksapp.io ./chart

helm install --name flask-tf --set service.ingressDNSName=flask-tf.b7c8110bf9aa4867a05d.westeurope.aksapp.io ./chart


### Setup Github webhook

```bash
ACR_NAME=briaracr    
GIT_PAT=
SLACK_WEBHOOK=
SP=
PASSWORD=
TENANT=
CLUSTER_RESOURCE_GROUP=
CLUSTER_NA_NAME=
CLUSTER_EU_NAME=

az acr task create \
    --registry $ACR_NAME \
    --name flask-tf \
    --context https://github.com/chzbrgr71/flask-tf.git \
    --branch master \
    --file acr-task.yaml \
    --git-access-token $GIT_PAT \
    --set-secret SLACK_WEBHOOK=$SLACK_WEBHOOK \
    --set-secret SP=$SP \
    --set-secret PASSWORD=$PASSWORD \
    --set-secret TENANT=$TENANT \
    --set-secret CLUSTER_RESOURCE_GROUP=$CLUSTER_RESOURCE_GROUP \
    --set-secret CLUSTER_NA_NAME=$CLUSTER_NA_NAME \
    --set-secret CLUSTER_EU_NAME=$CLUSTER_EU_NAME
```