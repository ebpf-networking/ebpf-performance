FROM debian:latest
WORKDIR /app
COPY iperf3 /bin/
COPY libiperf.so.0.0.0 /lib/x86_64-linux-gnu/
COPY libsctp.so.1.0.18 /lib/x86_64-linux-gnu/
RUN ln -s libiperf.so.0.0.0 /lib/x86_64-linux-gnu/libiperf.so.0
RUN ln -s libsctp.so.1.0.18 /lib/x86_64-linux-gnu/libsctp.so.1 
COPY run_iperf3 ./
EXPOSE 5000
CMD [ "/app/run_iperf3" ]
