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


