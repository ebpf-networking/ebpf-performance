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
