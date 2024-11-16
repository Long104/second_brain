---
date: 2024-11-12
tags:
    -
hubs:
    - "[[]]"
urls:
    -
---
# colima



## colima

- colima delete # delete existing instance
- colima start

> For more usage options
-   colima --help
- colima start --help
> Or use a config file
- colima start --edit

> create VM with 1CPU, 2GiB memory and 10GiB storage.
- colima start --cpu 1 --memory 2 --disk 10

> modify an existing VM to 4CPUs and 8GiB memory.
- colima stop
- colima start --cpu 4 --memory 8

> create VM with Rosetta 2 emulation. Requires v0.5.3 and MacOS >= 13 (Ventura) on Apple Silicon.
- colima start --vm-type=vz --vz-rosetta
