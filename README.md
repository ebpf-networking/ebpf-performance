# ebpf-performance
 ~/workspace/cni-bash/kind/delete.sh
 ~/workspace/cni-bash/kind/create.sh
 kubectl apply -f ~/workspace/bash-cni/bashcni-ds.yml

 Testing with 
 Ubuntu 20.04 in a VM
 uname -r = 5.13.0-44-generic
 kind version = kind v0.14.0 go1.18.2 linux/amd64

 ./run_server runs the iperf3 server
 ./run_client (in another window) runs the iperf3 client
