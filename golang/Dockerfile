FROM golang
#ADD sources.list /etc/apt/sources.list

#COPY ./package/etcd-v3.1.8-linux-amd64.tar.gz /root/
RUN apt-get update
RUN apt-get install -y supervisor cron
	#&& tar -zxvf /root/etcd-v3.1.8-linux-amd64.tar.gz -C /root/ \
	#&& rm -rf /root/etcd-v3.1.8-linux-amd64.tar.gz \
	#&& mv /root/etcd-v3.1.8-linux-amd64 /usr/local/etcd \
RUN mkdir -p /var/log/supervisor

#ENV PATH $PATH:/usr/local/etcd

#EXPOSE 2379

RUN apt-get install -y lsof
RUN export GOROOT=/usr/local/go \
	&& export PATH=$PATH:$GOROOT/bin

#CMD ["/etc/init.d/ssh", "start -D"]
CMD ["/usr/bin/supervisord"]
