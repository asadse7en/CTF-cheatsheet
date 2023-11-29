# Forensics

&#x20; challenge info &#x20;

| Name:       | `Threat`                                    |
| ----------- | ------------------------------------------- |
| Category:   | `Forensics`                                 |
| Difficulty: | `Easy`                                      |
| Points:     | `100`                                       |
| Link:       | [`aupCTF`](https://tryhackme.com/jr/aupctf) |

### **Threat (100pts)** <a href="#threat-100pts" id="threat-100pts"></a>

#### Description <a href="#description" id="description"></a>

Tom had always been curious about programming, and one day he stumbled upon a new coding language that he had never heard of before. Excited to learn more, he asked ChatGPT for some resources to get started. ChatGPT provided a link to a website that had some useful tutorials and code samples. But when Tom tried to download one of the files, his computer started behaving strangely. After running the commands **md5sum tutorial.pdf > result.txt** and **cat result.txt**, the following output is received: `d0ee6ffc8ce0e7f21cdcbd5e98c2dd4174a5d1b0266ec7f69075a0d9bea14757`

`Flag Format: aupCTF{popular threat label}`

#### Approach <a href="#approach" id="approach"></a>

High probability that its a Virus so lets search the hash on [VirusTotal](https://www.virustotal.com/gui/home/search) and we get this

[https://www.virustotal.com/gui/file/d0ee6ffc8ce0e7f21cdcbd5e98c2dd4174a5d1b0266ec7f69075a0d9bea14757](https://www.virustotal.com/gui/file/d0ee6ffc8ce0e7f21cdcbd5e98c2dd4174a5d1b0266ec7f69075a0d9bea14757)

![Untitled](https://about/write-ups/aupctf/forensics/1.webp#center)

&#x20; flag  `aupCTF{trojan.nanocore/msil}`  challenge info &#x20;

| Name:       | `I Love Math`                               |
| ----------- | ------------------------------------------- |
| Category:   | `Forensics`                                 |
| Difficulty: | `Easy`                                      |
| Points:     | `100`                                       |
| Link:       | [`aupCTF`](https://tryhackme.com/jr/aupctf) |

### **I Love Math (100pts)** <a href="#i-love-math--100pts" id="i-love-math--100pts"></a>

#### Description <a href="#description-1" id="description-1"></a>

Challenge: [math](https://aupctf.s3.eu-north-1.amazonaws.com/math.pdf)

#### Approach <a href="#approach-1" id="approach-1"></a>

The challenge file is a pdf, with a week password. and can be easily cracked with john

`pdf2john math.pdf > hash`

```
┌──(kali㉿iasad)-[~/CTFs/aupctf]
└─$ john hash
Using default input encoding: UTF-8
Loaded 1 password hash (PDF [MD5 SHA2 RC4/AES 32/64])
Cost 1 (revision) is 6 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
naruto           (math.pdf)     
1g 0:00:00:00 DONE (2023-06-26 15:38) 
Use the "--show --format=PDF" options to display all of the cracked passwords
Session completed.
```

Open the document, but its empty! `I can't see anything here`. try selecting all text (Ctrl+A) to reveal potentially invisible text.

![Untitled](https://about/write-ups/aupctf/forensics/2.webp#center)

now do some math revision and you will get the flag

&#x20; flag  `aupCTF{I_Love_Math_6_1}`  challenge info &#x20;

| Name:       | `Password Recovery`                         |
| ----------- | ------------------------------------------- |
| Category:   | `Forensics`                                 |
| Difficulty: | `Medium`                                    |
| Points:     | `200`                                       |
| Link:       | [`aupCTF`](https://tryhackme.com/jr/aupctf) |

### **Password Recovery (200pts)** <a href="#password-recovery--200pts" id="password-recovery--200pts"></a>

#### Description <a href="#description-2" id="description-2"></a>

We stumble upon a lost smartphone that holds crucial data for an ongoing investigation. Unfortunately, the owner seems to have forgotten the screen lock password, but there is a glimmer of hope. The victim, in an attempt to remember the password, left a clue on the phone’s lock screen. use your forensics skills to find the password.

[Challenge file](https://aupctf.s3.eu-north-1.amazonaws.com/locked.tar.gz)

Hint💡: In android lock screen info is saved in a database

#### Approach <a href="#approach-2" id="approach-2"></a>

Once the download and extraction process is complete, we discover that it’s a disk image (.dd). The description suggests that this image contains data from a smartphone, and the hint suggest to locate a lock screen database and find what the user left behind on the lookscreen.

we can use either FTK® Imager or Autopsy to for this task

![Untitled](https://about/write-ups/aupctf/forensics/3.webp#center)

![Untitled](https://about/write-ups/aupctf/forensics/4.webp#center)

![Untitled](https://about/write-ups/aupctf/forensics/5.webp#center)

```
┌──(kali㉿iasad)-[~/CTFs/aupctf]
└─$ echo -n 'cDQkc3cwMDByZENMVTM=' | base64 -d

p4$sw000rdCLU3
```

&#x20; flag  `aupCTF{p4$sw000rdCLU3}`  challenge info &#x20;

| Name:       | `Kingsman`                                  |
| ----------- | ------------------------------------------- |
| Category:   | `Forensics`                                 |
| Difficulty: | `Hard`                                      |
| Points:     | `300`                                       |
| Link:       | [`aupCTF`](https://tryhackme.com/jr/aupctf) |

### **Kingsman (300pts)** <a href="#kingsman--300pts" id="kingsman--300pts"></a>

#### Description <a href="#description-3" id="description-3"></a>

Welcome to Kingsman, the world’s most elite intelligence agency where we pride ourselves on our cutting-edge technology. However, it appears that our highly sophisticated security system has been breached by an unknown hacker. Even our state-of-the-art AI, Merlin, has failed to protect our system against this intrusion. Your mission, if you choose to accept it, is to use your advanced decryption skills to bypass our highly flawed password policy and uncover the secrets that lie within. Get ready for the ultimate test of your intelligence as you embark on this daring mission to decrypt the hidden message that awaits. Only by cracking the code will you be able to claim your victory and prove yourself worthy of becoming a Kingsman agent. So, are you ready to accept this challenge?

The password requirements are as follows:

1. The first character must be a digit.
2. The second character must be a special character. `" ! @ $ % ^ & * ( ) "`
3. A pet name should follow the special character.
4. An uppercase letter comes next.
5. Finally, a lowercase letter.

Remember, Your objective is to crack the encryption and reveal the hidden message.

**Challenge file:** [**encrypted.7z**](https://aupctf.s3.eu-north-1.amazonaws.com/encrypted.7z)

Hint💡: Don’t tell anyone that i gave you names of the [pets](https://aupctf.s3.eu-north-1.amazonaws.com/pets.txt)

#### Approach <a href="#approach-3" id="approach-3"></a>

We have a password-protected file accompanied by a password policy in the provided description. Our task is to generate a wordlist that follows above rules using either **crunch** tool or Python.

**Password Policy: Number + Spacial char + Pet name + Uppercase + Lowercase**

```
import string

special_chars = "!@#$%^&*()_+"
pets = ["roxy"]

for pet in pets:
    for char in special_chars:
        for digit in range(10):
            for upper in string.ascii_uppercase:
                for lower in string.ascii_lowercase:
                    password = str(digit) + char + pet + upper + lower
                    print(password)
                    with open('wordlist.txt', 'a') as f:
                        f.write(password + '\n')
```

Now that we have the wordlist, let’s proceed with cracking the password. First we need to convert the file’s hash using the command **`7z2john > hash`**.

```
┌──(kali㉿iasad)-[~/CTFs/aupctf]
└─$ john hash --wordlist=wordlist.txt                    
Using default input encoding: UTF-8
Loaded 1 password hash (7z, 7-Zip archive encryption)
No password hashes left to crack (see FAQ)

┌──(kali㉿iasad)-[~/CTFs/aupctf]
└─$ john hash --show                 
secret.7z:9@roxyFk

1 password hash cracked, 0 left
```

```
┌──(kali㉿iasad)-[~/CTFs/aupctf]
└─$ 7z x encrypted.7z # Extract Zip
...

┌──(kali㉿iasad)-[~/CTFs/aupctf]
└─$ cat flag.txt
Here is your Reward  YXVwQ1RGe2owaG5jcjRjazVwYTU1dzByZDUhfQ==

┌──(kali㉿iasad)-[~/CTFs/aupctf]
└─$ echo -n 'YXVwQ1RGe2owaG5jcjRjazVwYTU1dzByZDUhfQ==' | base64 -d
aupCTF{j0hncr4ck5pa55w0rd5!}
```

&#x20; flag  `aupCTF{j0hncr4ck5pa55w0rd5!}`  challenge info &#x20;

| Name:       | `MemDump`                                   |
| ----------- | ------------------------------------------- |
| Category:   | `Forensics`                                 |
| Difficulty: | `Hard`                                      |
| Points:     | `300`                                       |
| Link:       | [`aupCTF`](https://tryhackme.com/jr/aupctf) |

### **MemDump (300pts)** <a href="#memdump--300pts" id="memdump--300pts"></a>

#### Description <a href="#description-4" id="description-4"></a>

You are investigating a potential security incident within your organization. Malicious activity has been detected on one of the company’s servers. To gather more information, you need to analyze a memory image of the affected server. You are provided with a memory image of the infected host.

you need to download the memory image from this link: [download file](https://aupctf.s3.eu-north-1.amazonaws.com/memdump2.mem)

Your goal is to find the flag, which consists of the process name of the malicious activity.

Flag format: `aupCTF{processname.exe}`

#### Approach <a href="#approach-4" id="approach-4"></a>

Once the file has been downloaded, it appears to be a memory dump. The description asks us to search for any potential malware within it. To do this, we can use a tool called “volatility,” which offers a useful plugin called “malfind.” By executing a simple command using this plugin, we can identify any suspicious or malicious processes present in the memory dump.

![Untitled](https://about/write-ups/aupctf/forensics/6.webp#center)

the commands in volatility2 and vol3 are different here is a nice [cheatsheet](https://blog.onfvp.com/post/volatility-cheatsheet/)
