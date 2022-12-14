FROM ubuntu:22.10

Label Purpose : "AWS Pyspark"

# Install necessary dependencies

RUN apt-get update && apt-get install -y wget \
    && apt-get install -y nano \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install JDK
RUN mkdir envs

RUN mkdir envs/javase

WORKDIR /envs/javase

SHELL ["/bin/bash", "-c"]

RUN wget --no-check-certificate --no-cookies --header \
 "Cookie: oraclelicense=accept-securebackup-cookie" \
 https://download.oracle.com/java/19/latest/jdk-19_linux-x64_bin.tar.gz

RUN tar xvzf jdk-19_linux-x64_bin.tar.gz

RUN mv jdk-19.0.1 java

# Install java path to bash
RUN cat ~/.bashrc

ENV PATH "$PATH:/envs/javase/java/bin/"
ENV JAVA_HOME "/envs/javase/java/"

RUN source ~/.bashrc

#Install maven

RUN mkdir /envs/maven

WORKDIR /envs/maven

RUN wget https://dlcdn.apache.org/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.tar.gz

RUN tar xvzf apache-maven-3.8.6-bin.tar.gz

RUN mv apache-maven-3.8.6 apache_maven


ENV PATH "$PATH:~/.local/bin:/envs/javase/java/bin:/envs/maven/apache_maven/bin"

# Create maven project, configure dependencies for AWS


RUN mkdir /projects

WORKDIR /projects

RUN mvn -B archetype:generate \

  -DarchetypeGroupId=org.apache.maven.archetypes \

  -DgroupId=com.sample.myapps \

  -DartifactId=app

RUN cd app/

ENV USER ZubeyirO
ENV SHELL /bin/bash

CMD ["bash"]
