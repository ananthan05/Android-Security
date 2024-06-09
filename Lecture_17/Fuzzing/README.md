## Fuzzing

“fuzzing” technique to test the security and vulnerabilities of crypto libraries in Android applications.

The tools used for fuzzing in this lecture include

1. **OSS-Fuzz:** Continuous Fuzzing Service for Open Source Software
2. **ClusterFuzz:** Scalable Fuzzing Infrastructure
3. **FuzzBench:** Fuzzer benchmarking as a service

which are automated processes used by Google for open-source projects.

Fuzzing involves testing the behavior and vulnerabilities of functions by manipulating inputs, such as strings or images.

[Fuzzing](https://github.com/google/fuzzing) Refer this for more information.

These are all common fuzzing tools, but we will be discussing the CDF (crypto differential fuzzing) tool.

##   CDF (crypto differential fuzzing)

CDF is a tool to automatically test the correctness and security of cryptographic software. CDF can detect implementation errors, compliance failures, side-channel leaks, and so on.

CDF implements a combination of unit tests with "differential fuzzing", an approach that compares the behavior of different implementations of the same primitives when fed edge cases and values maximizing the code coverage.

Unlike general-purpose fuzzers and testing software, CDF is:

- **Smart**: CDF knows what kind of algorithm it's testing and adapts to the tested functions.
- **Fast**: CDF tests only what needs to be tested and parallelizes its tests as much as possible.
- **Polyvalent**: CDF isn't specific to any language or API, but supports arbitrary executable programs or scripts.
- **Portable**: CDF will run on any Unix or Windows platform, since it is written in Go without any platform-specific dependencies.

The purpose of CDF is to provide more efficient testing tool to developers and security researchers, being more effective than test vectors and cheaper than manual audit of formal verification.

[CDF](https://github.com/kudelskisecurity/cdf)Refer this for more information.


## INSTALLATION

![image](https://github.com/ananthan05/Android-Security/assets/140697378/6e389c52-b90e-46ae-8e64-4db65145801d)

```
git clone https://github.com/kudelskisecurity/cdf.git
```

![image](https://github.com/ananthan05/Android-Security/assets/140697378/70d734d6-fe5d-4417-a478-d3da45978a85)

![image](https://github.com/ananthan05/Android-Security/assets/140697378/e2426f0a-ffc6-488a-b1c8-3319bd568e8c)

## First build the cdf binary.

```
 make examples-all
```
 will build all the examples.
 
 while 
 ```
make examples-go
```
 will only build the Go examples.

```
make test
```
will run unit tests (of CDF).

