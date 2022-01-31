# Docker Image

These are the steps to make a Docker image for an Edgeware node

1.  in the `Dockerfile` in the root directory make sure that at the top you are using `FROM paritytech/ci-linux:production as builder` otherwise, it will not build.

![User-uploaded Image](https://static.slab.com/prod/uploads/9yelyblh/posts/images/PZnZa1wLoS1xRMKpkOzQ4KSq.png)

Add a caption

1.  Run command `docker build .` Then it will start building it will take a while about 30minutes.
2.  Make sure you have a docker hub account and that you are signed in on the docker app
3.  Once it is completed rename the image by running `docker images` to check for the image id then run the command `image tag <image id> <your-name>/edgeware-node:v3.3.3` this will rename it once you are happy with the name to push to docker hub run command `docker push <your-name>/edgeware-node:v3.3.3`

Troubleshooting

If the above image failed to compile `edgeware-cli`, then it's because your machine doesn't have enough memory, or your docker doesn't have enough memory available. Try and increase Docker's available memory by a few notches, by going to Docker Desktop settings.