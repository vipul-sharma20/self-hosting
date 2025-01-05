FROM debian:bullseye-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    git \
    cmake \
    wget \
    libopenblas-dev \
    libfftw3-dev \
    python3 \
    ca-certificates \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

WORKDIR /app

RUN git clone https://github.com/ggerganov/whisper.cpp.git

WORKDIR /app/whisper.cpp

RUN make

RUN sh ./models/download-ggml-model.sh large-v3-turbo-q5_0

EXPOSE 7659

ENTRYPOINT ["./server"]

CMD ["--host", "0.0.0.0", "--port", "7659", "--model", "models/ggml-large-v3-turbo-q5_0.bin"]
