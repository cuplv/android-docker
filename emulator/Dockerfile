FROM thyrlian/android-sdk-vnc

RUN apt-get update
RUN apt-get install wget

RUN cd /opt/android-sdk/ && wget https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip
RUN cd /opt/android-sdk && echo "A" | unzip sdk-tools-linux-3859397.zip
RUN sdkmanager "platform-tools" "platforms;android-23" "emulator"
#RUN sdkmanager "system-images;android-23;default;x86_64"
#RUN echo "no" | avdmanager create avd -n test -k "system-images;android-23;default;x86_64"

RUN sdkmanager "system-images;android-23;google_apis;armeabi-v7a"
RUN echo "no" | avdmanager create avd -n test -g google_apis -k "system-images;android-23;google_apis;armeabi-v7a"

RUN apt-get install -y apt-transport-https sudo curl software-properties-common

# Oracle Java Jdk 8
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk7-installer
# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# sbt
RUN echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
RUN sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
RUN sudo apt-get update
RUN sudo apt-get install -y sbt

# Necessary for ARM emulator
ENV QT_QPA_PLATFORM offscreen
ENV LD_LIBRARY_PATH ${ANDROID_HOME}/tools/lib64:${ANDROID_HOME}/emulator/lib64:${ANDROID_HOME}/emulator/lib64/qt/lib

