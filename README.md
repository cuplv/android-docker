# android-docker
Dockerfile and instructions for running docker instance with emulator.

The image adds to the thrillian emulator the android sdk, scala and java.

The image starts 3 services: adb, ssh, vnc. Refer to [https://github.com/thyrlian/AndroidSDK](https://github.com/thyrlian/AndroidSDK) for more information.


# Build the docker image

Build the `cuplv-android-emulator` image

```cd emulator && docker build -t cuplv-android-emulator```


# Run the container interactively

```docker run -di -p 5037:5037 --name=cuplv-android-emulator cuplv-android-emulator```

The container still does not run an emulator.

To run an emulator on the running container:
`docker exec -it <container id> /bin/bash`

And then from inside the container:
`emulator -avd test -noaudio -no-boot-anim -accel on -gpu off`

In your derived docker images you can add start the android emulator at startup time through supervisord (just add a configuration).

