FROM elasticsearch:5.1.1

EXPOSE 9200 9300
ADD sources.list /etc/apt/sources.list
#RUN ./bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v5.1.1/elasticsearch-analysis-ik-5.1.1.zip
#RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN apt-get update && apt-get install zip
RUN mkdir -p /usr/share/elasticsearch/plugins/ik
RUN cd /usr/share/elasticsearch/plugins/ik && wget https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v5.1.1/elasticsearch-analysis-ik-5.1.1.zip && unzip elasticsearch-analysis-ik-5.1.1.zip
RUN apt-get install -y git
RUN git clone git://github.com/mobz/elasticsearch-head.git
RUN wget -P /root/ https://npm.taobao.org/mirrors/node/v8.9.3/node-v8.9.3-linux-x64.tar.xz
RUN tar -Jxf /root/node-v8.9.3-linux-x64.tar.xz -C /root/ && \
    mv /root/node-v8.9.3-linux-x64 /usr/local/node && \
    rm -rf /root/node-v8.9.3-linux-x64.tar.xz
    #echo 'export NODE_HOME=/usr/local/node' >> ~/.profile && \
    #echo 'export PATH=$PATH:$NODE_HOME/bin' >> ~/.profile
    #sh source ~/.profile
ENV NODE_HOME /usr/local/node
ENV PATH $PATH:$NODE_HOME/bin