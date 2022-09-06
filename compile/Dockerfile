FROM rockylinux:9.0

RUN dnf install -y ruby \
    ruby-devel \
    "@Development Tools" && \
    gem install jekyll -v 4.2.2 && \
    if [[ -f /etc/yum/protected.d/systemd.conf ]];then rm -f /etc/yum/protected.d/systemd.conf; fi && \
    dnf remove -y ruby-devel \
    "@Development Tools" && \
    dnf clean -y all && \
    rm -rf /var/cache/dnf/*

ARG CACHEBUST=1

RUN dnf install -y git && \
    git clone https://github.com/jdbalgos/jdbalgos.github.io.git /srv/jekyll && \
    dnf remove -y git && \
    dnf clean -y all && \
    rm -rf /var/cache/dnf/* && \
    echo $CACHEBUST

EXPOSE 4000

WORKDIR /srv/jekyll

RUN sed -i 's/^#host/host/' _config.yml && \
    sed -i 's/^#port: [0-9][0-9][0-9][0-9]/port: 4000/' _config.yml

CMD /usr/local/bin/jekyll serve --baseurl ""
