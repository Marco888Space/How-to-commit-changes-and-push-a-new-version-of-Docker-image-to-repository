# How to commit changes and push a new version of Docker image to repository

1. Login to Docker:
```
docker login --username=DOCKER_HUB_LOGIN
```

2. Make some changes to image:
```
docker run --entrypoint=/bin/bash -it -v $PWD/somefolder/somefile.txt:/somefolder/somefile.txt REPOSITORY_NAME/IMAGE_NAME:OLD_TAG_NAME
```
In this example we use "volume mounting" option to get acces to somefile.txt on our host machine from the inside of image.

3. When we are ready to commit changes to image, check the containers list:
```
docker ps -a
```

4. Copy the container id with the changes in it and the execute this command:
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
