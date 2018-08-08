# Dogestore

## Introduction
```
Secret Cloud Storage System: This is a new system to store your end-to-end encrypted secrets. Now with SHA3 integrity checks!
```

First challenge I have attempted completely on my own. We get 2 files from the attachement: ```fragment.rs``` and ```encrypted_secret```. Right away we see that this is a rust file. I'm not familiar at all with rust therefore the first task will be to translate the code to python and perhaps simplify where I can.

## Translating to python

This was the resulting python script:
```python
from Crypto.Cipher import AES
import base64
import hashlib

flag_size = 56
flag_data_size = flag_size * 2

class Unit:
    def __init__(self, letter,size):
        self.letter = letter
        self.size = size

def deserialize(data):
    secret = []
    for i in range(0, len(data),2):
        secret.append(Unit(data[i],data[i+1]))
    return secret

def decode(data):
    res = []
    for unit in res:
        res.append(bytes([unit.letter]) * (unit.size + 1))
    return res

def decrypt(data):
    key = get_key()
    iv = get_iv()
    cipher = AES.new(key,AES.MODE_CBC,iv)
    decrypted = cipher.decrypt(data)
    return decrypted

def store(data):
    if len(data) != len(flag_data_size):
        print "Error"
    decrypted = decrypt(data)
    secret = deserialize(decrypted)
    expanded = decode(secret)
    h = hashlib.sha256()
    stringi = base64.encodestring(h.digest(expanded))
    return stringi
```

## Finding the weakness
TODO requires netwrok access
