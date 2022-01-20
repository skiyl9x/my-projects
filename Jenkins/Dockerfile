FROM jenkins/jenkins

ARG HOST_UID=1000
ARG HOST_GID=998

USER root
RUN apt-get update && \ 
apt-get install ca-certificates curl gnupg lsb-release -y && \
curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && \
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
$(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
apt-get update && \
apt-get install docker-ce docker-ce-cli containerd.io -y

RUN curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
chmod +x /usr/local/bin/docker-compose && \
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose 

RUN usermod -u $HOST_UID jenkins
RUN groupmod -g $HOST_GID docker
RUN usermod -aG docker jenkins

USER jenkins
