# Use the latest Ubuntu image
FROM ubuntu:latest

# Update package lists
RUN apt-get update

# Install netcat-openbsd
RUN apt-get install -y netcat-openbsd

# Install curl
RUN apt-get install -y curl

# Install git
RUN apt-get install -y git

# Install make
RUN apt-get install -y make

# Install kubectl dependencies
RUN apt-get install -y apt-transport-https ca-certificates gnupg lsb-release

# Add Kubernetes apt repository
RUN apt-get install -y apt-transport-https ca-certificates curl gpg
RUN curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key |  gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
RUN echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' |  tee /etc/apt/sources.list.d/kubernetes.list
# Update package lists again after adding Kubernetes repository
RUN apt-get update

# Install kubectl
RUN apt-get install -y kubelet kubeadm kubectl && apt-mark hold kubelet kubeadm kubectl && apt-get install -y kubectl && curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/kubectl
# Clean up APT when done
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
# Verify installation
RUN curl --version && \
    kubectl version --client && \
    git --version && \
    make --version

# Set bash as the default shell
CMD ["/bin/bash"]
