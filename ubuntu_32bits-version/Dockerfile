FROM i686/ubuntu
MAINTAINER Boutry Thomas 'thomas.boutry@x3rus.com'

# install apps 
RUN  apt-get update && DEBIAN_FRONTEND=noninteractive  apt-get install -y vim \
        bc  \
        openssh-server \
        man \
        dnsutils \
        wget \
        sudo \
        net-tools \
        psmisc \
        telnet \
        whois \
        curl \
        git \
        gitk \
        screen \
        byobu \
        unzip \
        lsof \
        software-properties-common \
        supervisor \
        && apt-get clean all \
        && rm -rf /var/lib/apt/lists/*
 

## Set timezone
#
RUN echo "America/Montreal" > /etc/timezone && \
    dpkg-reconfigure -f noninteractive tzdata

# Create default user "BOB" with password toto
RUN useradd -s /bin/bash -m  bob && \
    echo "bob:toto" | chpasswd && \
    usermod -G sudo bob

# Create sSh directory to be able to start ssh
RUN mkdir -p /var/run/sshd

COPY conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Remove DNS validation for ssh
RUN echo "\n UseDNS no" >> /etc/ssh/sshd_config && \
        sed -e 's/PrintLastLog yes/PrintLastLog no/' -i /etc/ssh/sshd_config

# Set locale
RUN locale-gen en_CA.UTF-8
ENV LC_ALL en_CA.UTF-8
ENV LANG en_CA.UTF-8 
ENV LANGUAGE en_CA:en
RUN dpkg-reconfigure locales

EXPOSE 22
CMD ["/usr/bin/supervisord"]

