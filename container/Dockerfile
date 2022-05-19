FROM ubuntu:latest
WORKDIR /app
#COPY iperf3 /bin/
#COPY libiperf.so.0.0.0 /lib/x86_64-linux-gnu/
#COPY libsctp.so.1.0.18 /lib/x86_64-linux-gnu/
RUN ln -s libiperf.so.0.0.0 /lib/x86_64-linux-gnu/libiperf.so.0
RUN ln -s libsctp.so.1.0.18 /lib/x86_64-linux-gnu/libsctp.so.1 
RUN apt-get update
RUN apt-get -y install apt-utils
RUN apt-get -y upgrade
RUN apt-get -y install linux-tools-common linux-tools-5.15.0-30-generic linux-tools-generic
RUN apt-get -y install iperf3
RUN apt-get -y install ubuntu-dbgsym-keyring
RUN echo "deb http://ddebs.ubuntu.com jammy main restricted universe multiverse" >/etc/apt/sources.list.d/ddebs.list
RUN apt-get update
#RUN apt-get -y install debian-goodies
#RUN find-dbgsym-packages iperf3
RUN apt-get -y install iperf3-dbgsym libc6-dbg libiperf0-dbgsym libsctp1-dbgsym
RUN apt-get -y install perl
COPY stackcollapse-perf.pl ./
COPY flamegraph.pl ./
RUN ls -l /usr/bin/perf
COPY run_iperf3 ./
COPY run_perf_script ./
EXPOSE 5000
CMD [ "/app/run_iperf3" ]
