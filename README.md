# android-docker
Dockerfile and instructions for running docker instance with emulator.

The image adds to the thrillian emulator the android sdk, scala and java.

The image starts 3 services: adb, ssh, vnc. Refer to [https://github.com/thyrlian/AndroidSDK](https://github.com/thyrlian/AndroidSDK) for more information.


# Build the docker image

Build the `cuplv-android-emulator` image

```cd emulator && docker build -t cuplv-android-emulator```


# Run the container

```docker run -di -p 5037:5037 -p 2222:22 -p 5901:5901 --name=cuplv-android-emulator cuplv-android-emulator```

The container still does not run an emulator (it exposes adb on port 5037, ssh on port 2222, and vnc on port 5901)

To run an emulator on the running container:
`docker exec -it <container id> /bin/bash`

And then from inside the container:
`emulator -avd test -noaudio -no-boot-anim -accel on -gpu off`

In your derived docker images you can add start the android emulator at startup time through supervisord (just add a configuration).

