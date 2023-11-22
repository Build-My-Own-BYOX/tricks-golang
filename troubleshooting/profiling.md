# troubleshooting > profilling

## Empty memory profilling result
- Reason: This may comes from the rate that the profiler samples the memory usage.
- Solution: 
    - Decrease `runtime.MemProfileRate` as low as you need
        - Don't make it too low, because the profiler will show a lot of uncecessary data
    - Use `alloc_space` to get correct data
- Additional information from the official documentation (https://pkg.go.dev/runtime#MemProfileRate): 
    ```
    To include every allocated block in the profile, set MemProfileRate to 1.
    To turn off profiling entirely, set MemProfileRate to 0.
    ```
- References: 
    - `alloc_space` option for pprof: https://austburn.me/blog/go-profile.html