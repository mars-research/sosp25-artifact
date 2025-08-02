# Atmosphere: Practical Verified Kernels with Rust and Verus

Thank you for volunteering to evaluate the SOSP25 artifacts. Welcome! 

This documentation contains the steps necessary to reproduce the artifacts for our paper titled **Atmosphere: Practical Verified Kernels with Rust and Veruss**.

## Overview

The general steps include:

1. Share your GitHub ID or SSH key to get access to the codebase. The code will be released on conference day
1. Reserve machines from Cloudlab https://www.cloudlab.us/ or use machines already set up.
1. Run experiments
1. Verify results

## Verification time/line count and system call microbenchmarks
https://github.com/mars-research/atmosphere/tree/AE-verification-bench-%2B-syscall_benchs

## NVEM benchmarks
There are three different configs for the NVME benchmarks. We've created a different branch for each config.

### Driver 
https://github.com/mars-research/atmosphere/tree/AE_NVME_Driver
### One CPU core shared by client and driver
https://github.com/mars-research/atmosphere/tree/AE_NVME_C1
### Two CPU cores for client and driver
https://github.com/mars-research/atmosphere/tree/AE_NVME_C2

To run the benchmark, first create a NVMe image:
```
fallocate -l100G nvme.img
```
Run the kernel, and the kernel will start the benchmark automatically
```
atmo run --release --nvme-img="$PWD/nvme.img"
```
To change the batch size, change `batch_sz` variable under `dom0/src/nvme_client.rs` to `1` or `32`. The batch size is currently hardcoded; we apologize for the inconvenience.

If the test gets stuck (the console prints progress for each 5%, and there are four runs), reboot `atmo`. 

After the benchmark is finished, the console will print the result. After that, you may change the batch size or switch to a different branch to test different configs. 
