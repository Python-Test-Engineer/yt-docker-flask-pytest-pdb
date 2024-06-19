
# RUN TESTS - GOOD

docker build -t factors_flask_tester -f Dockerfile.tester --build-arg BaseImage=factors_flask_pdb .

docker run -it --rm -v ${PWD}:/data factors_flask_tester

# RUN DEBUG - GOOD

docker build -t factors_flask_debug -f Dockerfile.debug --build-arg BaseImage=factors_flask_pdb .

docker run -it --rm -p 5000:5000 factors_flask_debug

