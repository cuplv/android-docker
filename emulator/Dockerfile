FROM thyrlian/android-sdk-vnc

WORKDIR /app

ADD . /app

RUN apt-get update
RUN apt-get install wget
RUN cd /opt/android-sdk/ && wget https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip
RUN cd /opt/android-sdk && echo "A" | unzip sdk-tools-linux-3859397.zip
RUN sdkmanager "platform-tools" "platforms;android-23" "emulator"
RUN sdkmanager "system-images;android-23;default;x86_64"
RUN echo "no" | avdmanager create avd -n test -k "system-images;android-23;default;x86_64"