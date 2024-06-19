<!-- docker build -t factors_flask_[]:cython-multi -f Dockerfile.cython-multi .

docker run -it --rm -p 5000:5000 factors_flask:cython-multi -->

<!-- docker build -t factors_flask_pdb -f Dockerfile.cython-multi .

docker run -it --rm -p 5000:5000 factors_flask_pdb -->

docker build -t factors_flask_pdb -f Dockerfile.flask .

docker run -it --rm -p 5000:5000 factors_flask_pdb

http://127.0.0.1:5000/32345678