## Flask app for serving Tensorflow trained model

#### Running local

```bash
FLASK_APP=app.py FLASK_DEBUG=1 python -m flask run

curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/image-classification/label-image/edsheeran.jpg" http://localhost:5000/detect_image

curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/image-classification/label-image/bradpitt.jpg" http://localhost:5000/detect_image

curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/image-classification/label-image/brianredmond.jpg" http://localhost:5000/detect_image

curl -F "image.jpg=@/Users/brianredmond/gopath/src/github.com/chzbrgr71/image-classification/label-image/edsheeran.jpg" http://40.78.47.97:5000/detect_image
```

#### Container

```bash
docker build -t chzbrgr71/edsheeran-flask-app:1.1 .

docker push chzbrgr71/edsheeran-flask-app:1.1

docker run -d --name flask -p 5000:5000 chzbrgr71/edsheeran-flask-app:1.1
```