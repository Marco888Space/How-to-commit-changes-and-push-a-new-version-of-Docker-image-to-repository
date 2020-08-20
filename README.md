# How to commit changes and push a new version of Docker image to repository

1. Login to Docker:
```
docker login --username=DOCKER_HUB_LOGIN
```

2. Make some changes to image. For example:
```
docker run --entrypoint=/bin/bash -it -v $PWD/somefolder/somefile.txt:/somefolder/somefile.txt REPOSITORY_NAME/IMAGE_NAME:OLD_TAG_NAME
```
Here we use "volume mounting" option to get acces to somefile.txt on our host machine from the inside of image.
For multiple files "volume mounting" just add another -v option like this:
```
docker run --entrypoint=/bin/bash -it -v $PWD/somefolder/somefile1.txt:/somefolder/somefile1.txt -v $PWD/somefolder/somefile2.txt:/somefolder/somefile2.txt REPOSITORY_NAME/IMAGE_NAME:OLD_TAG_NAME
```

3. When we are ready to commit changes to image, check the containers list:
```
docker ps -a
```

4. Copy the container id with the changes in it and then execute this command:
```
docker commit -m "CHANGE_LOG_MESSAGE" CONTAINER_ID_WITH_CHANGES REPOSITORY_NAME/IMAGE_NAME:NEW_TAG_NAME
```

5. Push the updated image to repository
```
docker push REPOSITORY/IMAGE_NAME:NEW_TAG_NAME
```

6. Remove unused containers:
```
docker rm $(docker ps -aq)
```

7. Remove old version of the image:
```
docker image rmi REPOSITORY_NAME/IMAGE_NAME:OLD_TAG_NAME
```

## How to tag image
```
docker tag IMAGE_ID REPOSITORY_NAME/IMAGE_NAME:NEW_TAG_NAME
```

## General Docker commands you should know
* Run Docker image in daemon mode using explicit port inside the container
```
docker run -p 5000:4000 -d REPOSITORY/IMAGE_NAME:TAG_NAME
```
> Where 5000 is a host machine port that is mapped to 4000 - private port inside the container.

* Show application logs
```
docker logs CONTAINER_ID
```

* Stop Docker container
```
docker stop CONTAINER_ID
```
