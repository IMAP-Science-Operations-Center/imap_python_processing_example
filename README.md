 # Container Example Code

This the basic code for creating a Docker container. 
For questions contact: laura.sandoval@lasp.colorado.edu.

## Python Setup

It is recommended that a virtual environment is created within the project:
1. Make a virtual environment using `python -m venv venv` and activate it 
with `source venv/bin/activate`. 
2. Generate requirements.txt only if additional libraries are required. Otherwise, use the default project requirements.txt.
3. pip install -r requirements.txt

Note: If an error is thrown when installing psycopg2, you may need to read requirements for installing psycopg2: 
https://www.psycopg.org/docs/install.html#build-prerequisites. On Mac simply install Postgres.app, 
which comes with a Postgres server, client, and command line utilities (https://postgresapp.com/)


## Example Algorithm Usage

To run
`python src/algorithm_example.py --help`


## Building and Running a Docker Image Locally

To build the image run the following command from the Dockerfile directory. You might add -t option to tag your image 
and --rm to remove intermediate containers after the build is done.

`docker build -t my-image --rm .`

Now we can run our image using bind mounting. In our example, we will name the container ‘my_app’. 
Adding --rm option will remove the container automatically after the container exits.

`docker run --rm -it \
  -e PROCESSING_DROPBOX=/opt/data/dropbox \
  --volume="$(pwd)/container_example_data:/opt/data" \
  my-image:latest /opt/data/dropbox/input_manifest_20220923t000000.json`

The script `run_container_example.sh` should contain this code as well. You can build and run the example container
with `./run_container_example.sh`. Docker must be running, you must have permissions to execute the script, and
you must be in the same directory as the script. If you get a permission error, 
run `chmod 755 run_container_example.sh`
