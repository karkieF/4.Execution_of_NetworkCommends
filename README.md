# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>

## program:

## client.py :
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input('Enter the website you want to ping: ').strip()
    if not ip:
        print('Please enter a valid hostname.')
        continue
    if ip.lower() in ('quit', 'exit'):
        print('Closing client.')
        break

    s.send(ip.encode())
    data = s.recv(4096)
    if not data:
        print('Server closed connection.')
        break

    print('Server response:\n' + data.decode())
```
### server.py:
```
import socket
from pythonping import ping

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print('Server listening on localhost:8000')

c, addr = s.accept()
print('Client connected from', addr)

while True:
    hostname = c.recv(1024).decode().strip()
    if not hostname:
        print('No hostname received; closing connection.')
        break

    print(f'Ping request for: {hostname}')
    try:
        result = ping(hostname, count=4, verbose=False)
        response = str(result)
    except Exception as e:
        response = f'ERROR: {type(e).__name__}: {e}'
        print('Ping failed:', response)

    c.send(response.encode())
```

## Output
### client.py:
<img width="537" height="209" alt="image" src="https://github.com/user-attachments/assets/05fdc5cc-fe0e-4e16-a54f-75b02c7f6049" />

### server.py:
<img width="419" height="94" alt="image" src="https://github.com/user-attachments/assets/2f23d12e-76b9-49e1-abd9-836dd804c6cb" />

## Result
Thus Execution of Network commands Performed 
