# DeepSpeed on Sunspot Meeting Notes

# 2023-03-29
- [ ] Able to use MPICH + `cxi`
- [ ] Question about why I'm using `mpich` instead of `deepspeed` launcher directly
- [ ] [10:16 AM] Agrawal, Nishant

1. Ensure conda is not conflicting with system default  
2. If topo is not working, we need to debug  
3. Run without ccl backend and use MPICH collectives  
4. Memory leak on CPU, high VM  
5. 12 application processes are pinned to one socket(host) threads only. Not distributed across 2 sockets??  
6. fabrics ports are not same (ze_premitives.cpp)