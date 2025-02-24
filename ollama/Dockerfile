FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install required dependencies
RUN apt-get update && apt-get install -y \
    curl \
    sudo \
    unzip \
    && rm -rf /var/lib/apt/lists/*

# Download and install Ollama
RUN curl -fsSL https://ollama.com/install.sh | sh

# Expose the API port
EXPOSE 11434

# Start Ollama in the background and wait for it to be fully ready before pulling the model
RUN ollama serve & \
    while ! curl -s http://localhost:11434/api/version >/dev/null; do sleep 1; done && \
    ollama pull deepseek-r1:7b && \
    pkill ollama

# Start Ollama in the background and keep the container running
CMD ["ollama", "serve"]
