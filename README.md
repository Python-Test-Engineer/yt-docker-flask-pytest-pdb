Build a Flask Docker image that is then used as a base for a PyTest Docker image that runs tests in a container as well as enabling a PDB breakpoint to be used.

[YouTube Video](https://youtu.be/Jsf5S8cZj1Y)

Inspired by [Python in Containers](https://www.udemy.com/course/python-in-containers/) (wait for sale to get for around $20 USD). Updated and modified by me for this repo.

- use of -f flag for Dockerfiles
- use of ARG in Dockerfile to enable CLI input to build the FROM command
- use of .pdbrc to set breakpoints when building a Dockerfile debug container

## *Ensure Docker is running!*


## Set up

- `git clone https://github.com/Python-Test-Engineer/yt-docker-flask-pytest-pdb`
- `cd yt-docker-flask-pytest-pdb`
- `python -m venv venv`

## Build Flask Image

- `cd multistage`
- `docker build -t factors_flask_pdb -f Dockerfile.flask .` - see cmd.md.
- `docker run -it --rm -p 5000:5000 factors_flask_pdb`
- `http://127.0.0.1:5000/32345678` - runs endpoint to calculate factors in 3 secs
- `http://127.0.0.1:5000/12345678` - under 1 sec

You should see something like this:

```
Factors of 12345678 are 1, 2, 3, 6, 9, 18, 47, 94, 141, 282, 423, 846, 14593, 29186, 43779, 87558, 131337, 262674, 685871, 1371742, 2057613, 4115226, 6172839, 12345678. Computed in 0.8488622859999992 seconds.
```
You will see `factors_flask_pdb` in Docker Desktop.

You can CTRL+C to close.

## Build Test image

- `cd ..` to go back to root of project
- `cd simpletests`
- `docker build -t factors_flask_tester -f Dockerfile.tester --build-arg BaseImage=factors_flask_pdb .` - see cmd.md

 You will see factors_flask_tester in Docker Desktop. This is our PyTest container.

- `docker run -it --rm -v ${PWD}:/data factors_flask_tester` to run tests and generate reports. These are configured in tester.sh.

## Build Debug Image

- `docker build -t factors_flask_debug -f Dockerfile.debug --build-arg BaseImage=factors_flask_pdb .` Yo will see 

- `docker run -it --rm -p 5000:5000 factors_flask_debug` runs PDB debugger. `debub\.pdbrc` has two breakpoints set:

```
b 22
b 82
```

enter c to continue and q to quit

*factors_flask_pdb does not need to be running - it is built in to the testing image.*


