# CHANGELOG

## v1.0.1

**Add MIG support:"mixed strategy"**

**Add support for kubernetes v1.22+**

## v1.0.1.1

**Bugs fixed**

a pod can be scheduled to a node where its core usage is 100 - Fixed

cudevshr.cache can't be modified with non-root users - Fixed

## v1.0.1.2

**Add custom resource name**

A task with cores=100 will allocate all device memory(virtual device memory excluded)

## v1.0.1.3

**nvidia.com/gpucores will limit the GPU utilization inside container**
Prior than v1.0.1.3, nvidia.com/gpucores will not limit utilization inside container, we have fixed it in v1.0.1.3

## v1.0.1.4

**Add nvidia.com/gpumem-percentage resoure name**
This resource indicates the device memory percentage of GPU, can not be used with "nvidia.com/gpumem". If you want an exclusive GPU, specify both the "nvidia.com/gpucores" and "nvidia.com/gpumem-percentage" to 100

**Add GPU type specification**
You can set "nvidia.com/use-gputype" annotation to specify which type of GPU to use. "nvidia.com/nouse-gputype" annotation to specify which type of GPU to avoid.

## v1.0.1.5

Fix an monitor "desc not found" error

Add "devicePlugin.sockPath" parameter to set the location of vgpu.sock

## v1.1.0.0

**Major Update: Device Memory will be counted more accurately**
serveral device memory usage, including cuda context, modules, parameters, reserved addresses will be counted in v1.1.0.0

**Update to be compatable with CUDA 11.6 and Driver 500+**

**Rework monitor strategy**
Monitor will mmap control file into address space instead of reading it in each query.

## v1.1.1.0

**Fix segmentation fault when invoking cuMallocAsync**

**Core Utilization Oversubscribe and priority-base scheduling**
Currently we have two priority, 0 for high and 1 for low. The core utilization of high priority task won't be limited to resourceCores unless sharing GPU node with other high priority tasks.
The core utilization of low priority task won't be limited to resourceCores if no other tasks sharing its GPU.
See exmaple.yaml for more details

**Add Container Core Utilization policy**
See details in docs/config.md(docs/config_cn.md)

## v2.2

**Update device memory counting mechanism to compat with CUDA 11.3+ task**
sometimes vgpu-scheduler won't able to collect device memory usage when running cuda11.3+ compiled tasks in v1.x version of vgpu-scheduler. We solve this problem by reworking device memory counting mechanism.

**Use node annotation instead of grpc to communicate between scheduler and device-plugin**
In v1.x version of vgpu-scheduler, we use grpc to communicate between scheduler and device-plugin, but we reimplement this communication in v2.x by using node annotation, to make it more stable and readable.

**modified nvidia-container-runtime is no longer needed**
We remove self-modified nvidia-container-runtime in v1.x, because we now use node lock to track pod and container information. so this nvidia-container-runtime is no longer needed.

## v2.2.7

**BUG fix**

fix tasks with "gpumem-percentage" not working properly

fix dead lock when a process die with its lock not released

**Adjust certain logs**

**update go modules to more recent version in order to support k8s v1.25**

## v2.2.8

**BUG fix**

fix vGPUmonitor not working properly with containerd

fix installation error on k8s v1.25+





