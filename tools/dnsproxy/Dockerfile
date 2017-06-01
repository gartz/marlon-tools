# How to build:
# docker build -t gartz/simple-dns -t gartz/simple-dns:latest .
# docker push gartz/simple-dns

FROM python:2.7
LABEL maintainer="Gabriel Reitz Giannattasio <gabriel@samba.tv>" \
    description="This is an easy and simple to use DNS server writen by marlonyao <yaolei135@gmail.com>"

EXPOSE 53
WORKDIR /

COPY dnsproxy.py /dnsproxy.py

RUN chmod +x /dnsproxy.py \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        vim-tiny \
        telnet \

    && pip install -U pip \

    && (rm -rf /.env* || true) \
    && (find / -type d -name __pycache__ -exec rm -rf "{}" \; || true) \
    && (find / -type f -name \*.pyc -exec rm -f {} \; || true) \

    # Clean up cached files and git repo
    && (rm -rf ~/.cache/pip) \
    && rm -rf /var/lib/apt/lists/*

CMD /dnsproxy.py -s 8.8.8.8 -f /hosts -H 0.0.0.0
