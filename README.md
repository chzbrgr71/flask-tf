## Flask app for serving Tensorflow trained model

#### Running local

```bash
FLASK_APP=app.py FLASK_DEBUG=1 python -m flask run

curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/flask-tf/samples/edsheeran.jpg" http://localhost:5000/detect_image

curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/flask-tf/samples/bradpitt.jpg" http://localhost:5000/detect_image

curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/flask-tf/samples/brianredmond.jpg" http://localhost:5000/detect_image

IP=40.113.127.129
curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/flask-tf/samples/edsheeran.jpg" http://$IP:5000/detect_image

curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/flask-tf/samples/bradpitt.jpg" http://$IP:5000/detect_image
```

#### Container

```bash
export IMAGE_TAG=1.5

docker build -t chzbrgr71/edsheeran-flask-app:$IMAGE_TAG .

docker push chzbrgr71/edsheeran-flask-app:$IMAGE_TAG

docker run -d --name flask -p 5000:5000 chzbrgr71/edsheeran-flask-app:$IMAGE_TAG
```

#### Helm Setup

helm install --name flask-tf --set image=chzbrgr71/edsheeran-flask-app,imageTag=1.5 ./chart

Helm deploy. https://github.com/AzureCR/cmd/tree/master/helm  