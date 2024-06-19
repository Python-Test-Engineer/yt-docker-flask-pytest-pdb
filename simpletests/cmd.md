<!-- 

docker build -t factors_flask:tester -f Dockerfile.tester --build-arg BaseImage=factors_flask:cython-multi .

docker run -it --rm -v ${PWD}:/data factors_flask:tester

docker build -t factors_flask:debug -f Dockerfile.debug --build-arg BaseImage=factors_flask:cython-multi .

docker run -it --rm -p 5000:5000 factors_flask:debug -->

# RUN TESTS - GOOD

docker build -t factors_flask:tester -f Dockerfile.tester --build-arg BaseImage=factors_flask_pdb .

docker run -it --rm -v ${PWD}:/data factors_flask:tester


# RUN DEBUG - GOOD

docker build -t factors_flask:debug -f Dockerfile.debug --build-arg BaseImage=factors_flask_pdb .

docker run -it --rm -p 5000:5000 factors_flask:debug

http://127.0.0.1:5000/32345678