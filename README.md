A Docker image with [ROS](http://www.ros.org/) and [Intel SGX](https://software.intel.com/en-us/sgx) [SDK and
PSW](https://github.com/01org/linux-sgx) (platform software, i.e., runtime) installed.
You can use it as a base Docker image for your apps which use Intel SGX.

Intel SGX [kernel module](https://github.com/01org/linux-sgx-driver) has to be installed and loaded on the
host and you have to provide it to the container when you run it:

```
docker run -d --device /dev/isgx --device /dev/mei0 --name test-ros-sgx tatetian/ros-sgx
docker exec -t -i test-ros-sgx bash
```

SDK is installed under `/opt/intel/sgxsdk`. You should do:

```
source /opt/intel/sgxsdk/environment
```

in your bash script to load the SDK environment.
