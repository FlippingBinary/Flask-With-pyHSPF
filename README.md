# Flask-With-pyHSPF
Dockerfile which builds and environment with pyHSPF and Flask

## NLDAS2 Authentication
You must set a username and password for NLDAS2 downloads by using environment variables

`docker run -dp 5000:5000 --rm -e USERNAME='your username' -e PASSWORD 'your password' flippingbinary/flask-with-pyhspf`

## Persistent storage for cache
If you want persistent storage, you'll also need to mount a directory to /home/flask/cache
You can mount a folder named "cache" in the present directory with the Windows command below:

`docker run -dp 5000:5000 --rm -e USERNAME='your username' -e PASSWORD 'your password' --mount src="$(pwd)/cache",target=/home/flask/cache,type=bind flippingbinary/flask-with-pyhspf`

The Linux/MacOS equivalent might look like this, but I haven't tested it (yet):

`docker run -dp 5000:5000 --rm -e USERNAME='your username' -e PASSWORD 'your password' -v "$(pwd)/cache":/home/flask/cache flippingbinary/flask-with-pyhspf`

## Persistent container
If you want to keep the container around to run automatically or something, remove the "--rm" argument.

## Usage
Request data from the precipitation API by calling http://localhost:5000/precipitation with form data defining 'start_date' and 'end_date' to be a valid date range. For example, 'start_date' could be the string '1/1/1980' and 'end_date' could be '1/2/1980' to automatically retrieve one day of data for West Virginia and calculate the average precipitation.

Request data from the evaporation API by calling http://localhost:5000/evaporation with form data defining 'start_date' and 'end_date' to be a valid date range. For example, 'start_date' could be the string '1/1/1980' and 'end_date' could be '1/2/1980' to automatically retrieve one day of data for West Virginia and calculate the average potential evaporation.

Request a list of cached GRIB files by calling http://localhost:5000/

There is currently no way to adjust bounding box. It is hard-coded to West Virginia.
