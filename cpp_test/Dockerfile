# Get the base Ubuntu image from Docker Hub
FROM ubuntu:latest

# Update apps on the base image
RUN apt-get -y update && apt-get install -y

# Install the Clang compiler
RUN apt-get -y install clang && apt-get -y install git \
&& apt-get -y install wget &&  apt-get -y install build-essential\
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/ggerganov/whisper.cpp

WORKDIR whisper.cpp

RUN ./models/download-ggml-model.sh base.en

RUN make

RUN ./main -m models/ggml-base.en.bin -f samples/jfk.wav


# Run the output program from the previous step
CMD ["bash"]
