# android-docker
Dockerfile and instructions for running docker instance with emulator.


# Login to the Stack.cs
```
ssh centos@ip 
```

# Install docker on Stack
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
# pull the images
docker pull thyrlian/android-sdk-vnc    

# Create the container
```
yum -y install wget
wget https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip
yum -y install unzip
unzip sdk-tools-linux-3859397.zip
docker run -d --privileged -v /dev/kvm:/dev/kvm  -p 8080:5901 -p 2222:22 -p 5037:5037 -v <Android_SDK_PATH>:/opt/android-sdk thyrlian/android-sdk-vnc
docker exec -it container_hash bash
```
# Download the emulator images in the container
```
sdkmanager “platform-tools” “platforms;android-23” “emulator”
sdkmanager “system-images;android-23;default;x86_64”
```
# Create emulator
```
avdmanager create avd -n test -k "system-images;android-23;default;x86_64"
```
# Run emulator
```
emulator -avd test -noaudio -no-boot-anim -accel on -gpu off &
```

# To install Scala and SBT
``` 
apt-get install  apt-transport-https
curl https://bintray.com/sbt/rpm/rpm | sudo tee /etc/yum.repos.d/bintray-sbt-rpm.repo
apt-get install scala
echo "deb https://dl.bintray.com/sbt/debian /" |  tee -a /etc/apt/sources.list.d/sbt.list
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
apt-get update
apt-get install sbt
```

# Docker commands

general info 
```
docker info
```

list images
```
docker image ls
```

run an image
```
docker run [image name]
```

create an image from dockerfile
```
docker build -t [image name] .
```

stop a running container (container id comes from docker container ls)
```
docker container stop [container id]
```

run shell in docker container
```
docker exec -it my-app-container bash
```

remove all images
```
docker system prune -a
```

