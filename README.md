<div align=right>
<h2 align=right> Xe Softworks </h2>
<img src="https://camo.githubusercontent.com/beb0b377380084d9906e6c317706af49db4463f2fd37818cb7758bd21f5867ed/68747470733a2f2f64726976652e6c756c7a622e696e2f66696c652e7068703f713d363336386165616263663838312e706e672367682d6461726b2d6d6f64652d6f6e6c79" height=130 width=130>
</div>

<div align=center>
<img src="https://raw.githubusercontent.com/XeSoftworks/Quark/main/quark.webp?token=GHSAT0AAAAAABXA6SQWRGHU4KLWVK3JNSUYY3I2BDQ" height=200 width=200>

<h1> Quark </h1>
Quark is an enterprise Discord multitool/AIO wrapper and framework for automating Discord accounts.

Quark is developed by Xe Softworks, and maintained by Xe Softworks. For more info, visit [xesoft.works](https://xesoft.works)

</div>





<hr> 



# Basic Examples
### Sending a message

Send a message with the content *'testing quark'*, after the message is sent delete after 10 seconds.

```python
from wrapper import *

Discord = Discord('TOKEN')

content = Discord.send_message(
    channel = 904513273058177055,
    message = 'testing quark',
    delete_after = 10
).json()

print(content)
```

Output: `Sent: True; Status: 200`

### Getting user details
Get a users account details including username, user tag, user ID, connections, and mutual servers 
```python
from wrapper import *

Discord = Discord('TOKEN')

content = Discord.get_user(
    user = 1,
).json()

print(content)
```

### Buying Nitro
Buy nitro if the account has a valid credit card linked
```python
from wrapper import *

for token in open('tokens.txt', 'r').readlines():
    Discord = Discord(str(token.rstrip()))

    response = Discord.buy_nitro(
        amount = 1
    )

    print(response)
```

Output: `discord.gift/675yZrKaLQgqsT94, ODc2NTAyMzYyMTemzZy68WGe.xY-j3j.t-Pk9pCttPEE9iYd9dskTDavexY`

### Multiple token reactions
Create multiple reactions to a message 
```python
from wrapper import *

def send(w):
    content = w.create_reaction(
        channel = 904627884944138240,
        message = 904634461356965888,
        reaction = 'cool'
    ).json()
    
    print(content)

for token in open('tokens.txt', 'r').readlines():
    Wrapper = Discord(token.rstrip())
    send(Wrapper)
```


Output: `Status: 200`

# Basics

### Rate Limiting: REST

| Rest Type     | API Location  | Limit         |
| ------------- | ------------- | ------------- |
| POST Message  | Per-Channel  | 5/5s              |
| DELETE Message| Per-Channel  | 5/1s           |
| PUT/DELETE Reaction  | Per-Channel  | 300/300s              |
| PATCH Member | Per-Guild  |  10/10s             |
| PATCH Member Nick | Per-Guild  |  1/1s             |
| PATCH Username | Per-Account  | 2/3600s
| All Requests  | Per-Account  |  50/1s             |


### Rate Limiting: WS

| Rest Type     | API Location  | Limit         |
| ------------- | ------------- | ------------- |
|     Gateway Connect |   Per-Account    | 1/5s
|     Presence Update |   Per-Session  | 5/60s
|   All Sent Messages | Per-Session   | 120/60s
