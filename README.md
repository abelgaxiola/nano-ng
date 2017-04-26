Docker Image with an Angular app on Microsoft's NanoServer with IIS
---
# Created using microsoft/iis:nanoserver
### Image size 1.15 GB
The Angular source code is inside a folder named websrc. The websrc folder is inside the same folder where the Dockerfile resides.

Contents of the Dockerfile used:

    # Indicates that the nanoserver image will be used as the base image
    FROM microsoft/iis:nanoserver

    # Metadata indicating an image maintainer
    MAINTAINER @abelgaxiola

    # Delete the default website files
    RUN powershell -Command Remove-Item -Recurse C:\inetpub\wwwroot\*

    # Copy the contents of websrc folder into the default website folder
    COPY ./websrc c:/inetpub/wwwroot

    # Sets a command or process that will run each time a container is run from the new image
    CMD [ "CMD" ]

Docker commands used:

    docker build -t south-to-north .
	docker run -d --name south-to-north -p 80:80 south-to-north
	docker inspect --format '{{ .NetworkSettings.Networks.nat.IPAddress }}' south-to-north

The last command returns the IP Address of the running image.

The website can now be viewed and interacted with by copying the IP Address into a web browser's address bar

On Docker Hub: [Nano-Ng](https://hub.docker.com/r/abelgaxiola/nano-ng/)
