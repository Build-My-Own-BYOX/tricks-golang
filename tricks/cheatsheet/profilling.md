# tricks > cheatsheet > profiling

- Run cpu & memory profile with test: 
    ```
    go test <package> -cpuprofile cpu.prof -memprofile mem.prof
    ```

- Interact with profile output file
    ```
    pprof mem.prof
    ```

- Interact memory profile with allocate space type
    ```
    pprof --alloc_space mem.prof
    ```