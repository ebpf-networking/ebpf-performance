# ebpf-performance
### Set up 3 machines
 One to be test controller and kubernetes master, the others to be kubernetes workers
 Ubuntu 20.04
### Set up a non-root user on each machine
### Allow the test controller to 'ssh' to the worker machines
### Clone the repositories onto the test controller
```
cd
mkdir workspace
cd workspace
git clone git@github.com:ykt-networking/ebpf-performance-results.git
git clone git@github.com:ykt-networking/ebpf-performance.git
```
### Clone the repository onto the workers
```
cd
mkdir workspace
cd workspace
git clone git@github.com:ykt-networking/ebpf-performance.git
```
### Enable the workers to access kernel symbols
This step needs to be repeated after every reboot of the workers
```
sudo sh -c "echo 0  > /proc/sys/kernel/kptr_restrict"
sudo sh -c "echo -1 > /proc/sys/kernel/perf_event_paranoid"
```
### Install 'perf' on the workers
The packages to install are dependent on the kernel level. If you issue 'perf' you will be told a package to install for the 'perf' command. Install this and issue 'perf' again. Then you will be told 2 more packages to install. Here are the packages that were required on my machine
```
sudo apt install linux-tools-common
sudo apt install linux-tools-5.4.0-1028-ibm linux-tools-ibm
```
### Start Kubernetes with the chosen CNI
Starting Kubernetes and configuring a CNI is beyond the scope of this README.
### Run the test
On the master node, issue commands
```
cd
cd workspace/ebpf-performance
./run_flamegraph tjcw-kube-1 tjcw-kube-2 /home/tjcw/workspace/ebpf-performance-results/test-directory
```
This assumes the worker nodes are called tjcw-kube-1 and tjcw-kube-2 , and you want the results placed in directory `test-directory` of repository `ebpf-performance-results`
### Browse the resulting flamegraphs
On my Linux Thinkpad, the commands for this are
```
cd
cd eclipse-workspace-java/ebpf-performance-results
git fetch origin
git merge --ff-only origin/main
```
and browse to URL `file:///home/tjcw/eclipse-workspace-java/ebpf-performance-results/test-directory/server-flamegraph.svg` or `file:///home/tjcw/eclipse-workspace-java/ebpf-performance-results/test-directory/client-flamegraph.svg` . There are some additional files placed in this directory :
 `client.cpu` : Reported client CPU time for the duration of the test
 `client_per_tick` : Bits transferred per tick of client CPU
 `server.cpu` : Reported server CPU time for the duration of the test
 `server.log` : Last 10 lines of the server iperf3 output
 `server_per_tick` : Bits transferred per tick of server CPU

