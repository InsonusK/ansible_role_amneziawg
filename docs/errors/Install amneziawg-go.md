# Go verision incoorrect
```output
 stderr: |-
    go: downloading go1.24 (linux/amd64)
    go: download go1.24 for linux/amd64: toolchain not available
    make: *** [Makefile:20: amneziawg-go] Error 1
```

**Solution**
change variable go_package, setup new verion of GO