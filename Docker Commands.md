# Check for docker images
docker images

# Build docker from current working directory
docker build .

# Check newly created docker images
docker images

# run docker image just created
docker run -p 5000:5000 [Container ID]

