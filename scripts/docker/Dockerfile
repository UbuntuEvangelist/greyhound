FROM connormanning/entwine:latest
MAINTAINER Connor Manning <connor@hobu.co>

ENV CC clang
ENV CXX clang++

RUN (wget -qO- https://deb.nodesource.com/setup_4.x | bash -) && \
    apt-get install -y nodejs supervisor && \
    rm -rf /var/lib/apt/lists/*

RUN npm install -g node-gyp && npm update npm -g && npm cache clean

ADD http://www.timeapi.org/utc/now /tmp/bust-cache
RUN git clone "https://github.com/hobu/greyhound.git" && \
    cd greyhound && \
    make && \
    make install

EXPOSE 80
EXPOSE 443
EXPOSE 8989
VOLUME /opt/data

CMD greyhound dockerstart && greyhound log

# Sample invocation:
#       docker run -it -p 8080:80 -v ~/greyhound:/opt/data connormanning/greyhound

