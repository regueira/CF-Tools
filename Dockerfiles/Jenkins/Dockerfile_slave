FROM jenkins/jnlp-slave
ENV AWS_CLI_VERSION 1.14.4
RUN id 
USER root
RUN apt-get update && \
	apt-get -y install apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common && \
	curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
	add-apt-repository \
	"deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
	$(lsb_release -cs) \
	stable" && \
	apt-get update && \
	apt-get -y install docker-ce

RUN apt-get update && \
	apt-get install -y python python-pip ca-certificates groff less bash grep && \
	pip --no-cache-dir install awscli==${AWS_CLI_VERSION}
RUN usermod -aG docker jenkins
RUN groupmod -g 996 docker
USER jenkins
SHELL ["/bin/bash", "-c"]
###Additional steps below

VOLUME ["/var/jenkins_home/"]