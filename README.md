# android-docker
Dockerfile and instructions for running docker instance with emulator.



# Build the docker image

Build the `cuplv-android-emulator` image

```cd emulator && docker build -t cuplv-android-emulator```


# Run the container interactively

```docker run -di -p 5037:5037 --name=cuplv-android-emulator cuplv-android-emulator```


The container run an android emulator named "test"


# Set up the emulator on Stack.cs

- Login to the Stack.cs
```
ssh centos@ip 
```

- Install docker on Stack
```
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2

sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

sudo yum install docker-ce
sudo systemctl start docker
```

- pull the repository

```
git clone https://github.com/cuplv/android-docker
```

- Build the docker image and run the container
