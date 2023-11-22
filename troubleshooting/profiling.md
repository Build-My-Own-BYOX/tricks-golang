# troubleshooting > profilling

## Profiling with go test
- To profile, there are 2 steps needed:
    - generate profile output file
    - analysis that output file

- The first step `generate profile output file` can be done in 2 ways: 
    - Way 1: Specify commands when running `go test`. Example: running `go test <package> -cpuprofile cpu.prof` will generate `cpu.prof`, which is a CPU profile output
        - This way is impossible with `go run`
    - Way 2: Write the profile output file by code
        ```
        cpuProfile, err := os.Create("cpu.prof")
        if err != nil {
            log.Fatal(err)
        }
        pprof.StartCPUProfile(cpuProfile)
        defer pprof.StopCPUProfile()
        ```

- The second step is using `pprof` to analysis with profile output file. Example: `pprof cpu.prof`

- Both of the above steps can be done by only single click to `Profile <test_function> with 'CPU Profiler'` in Goland.

- References: 
    - pprof library: https://github.com/google/pprof
    - CPU Profiler in GOland: https://www.jetbrains.com/help/go/cpu-profiler.html


## Empty memory profilling result
- Reason: This may comes from the rate that the profiler samples the memory usage.
- Solution: Decrease `runtime.MemProfileRate` as low as you need
    - Don't make it too low, because the profiler will show a lot of uncecessary data
- Additional information from the official documentation (https://pkg.go.dev/runtime#MemProfileRate): 
    ```
    To include every allocated block in the profile, set MemProfileRate to 1.
    To turn off profiling entirely, set MemProfileRate to 0.
    ```
- References: 
    - `alloc_space` option for pprof: https://austburn.me/blog/go-profile.html