# Web

### **Starter (100pts)** <a href="#starter-100pts" id="starter-100pts"></a>

#### Description <a href="#description" id="description"></a>

**mera tu sir chakra raha tum dekh lo …** [**random**](https://challs.aupctf.live/starter/)

#### Approach <a href="#approach" id="approach"></a>

When we look it the website, we notice that each letter of the flag is scattered randomly across different parts of the screen. However, looking at the source code, we can find the flag.

![Untitled](https://about/write-ups/aupctf/web/1.webp#center)

***

**Flag: `aupCTF{w45n't-th47-h4rd-r1gh7}`**

***

#### Description <a href="#description-1" id="description-1"></a>

Carefully analyze the source code. [Click Here](https://challs.aupctf.live/header/)

#### Approach <a href="#approach-1" id="approach-1"></a>

visiting the site we get the source code

```
def headar_easy(request):
    if request.META.get('HTTP_GETFLAG') == 'yes':
        context = {
            'flag': '[REDACTED]',
        }
        
        return render(request, 'aa/flag.html', context)
    
    return render(request, 'aa/index.html')
```

Upon inspecting the source code, it’s clear that when we send a request to the site with a specific header “GETFLAG” and set its value to “yes,” the server will respond with the flag.

```
──(kali㉿iasad)-[~/CTFs/aupctf]
└─$ curl -H "GETFLAG: yes" https://challs.aupctf.live/header/

aupCTF{cust0m-he4d3r-r3qu3st}
```

***

**Flag: `aupCTF{cust0m-he4d3r-r3qu3st}`**

***

### **SQLi - 1 (100pts)** <a href="#sqli---1-100pts" id="sqli---1-100pts"></a>

#### Description <a href="#description-2" id="description-2"></a>

[Click Here](https://challs.aupctf.live/sqli-1/)

#### Approach <a href="#approach-2" id="approach-2"></a>

with a simple SQL injection payload we can get the flag ie: **`‘or 1=1`**

***

**Flag: `aupCTF{3a5y-sql-1nj3cti0n}`**

***

### **SQLi - 2 (200pts)** <a href="#sqli---2-200pts" id="sqli---2-200pts"></a>

#### Description <a href="#description-3" id="description-3"></a>

[Click Here](https://challs.aupctf.live/sqli-2/)

#### Approach <a href="#approach-3" id="approach-3"></a>

this time some restrictions are made but we can still get the flag with this payload. **`-- or '1'='1'`**

***

**Flag: `aupCTF{m3d1um-sql-1nj3cti0n}`**

***

### **Time Heist (100pts)** <a href="#time-heist-100pts" id="time-heist-100pts"></a>

#### Description <a href="#description-4" id="description-4"></a>

use your time travel skills to recover the hidden flag. [Click Here](https://iasad.me/)

#### Approach <a href="#approach-4" id="approach-4"></a>

The description specifically suggests utilizing your time travel skills, indicating the use of [archives.org](https://web.archive.org/) to view this site in its past state.

By conducting a search for “[iasad.me/tags](https://iasad.me/tags/)” on [archives.org,](https://web.archive.org/) we can access numerous snapshots of the website, including the specific snapshot from May 28th, 2023, where we can find the flag.

![Untitled](<../../../.gitbook/assets/2 (1).webp>)

![Untitled](<../../../.gitbook/assets/3 (1).webp>)

we can see a tag named flag opening at we find a page that has the flag for us in source code

![Untitled](<../../../.gitbook/assets/4 (1).webp>)

***

**Flag: `aupCTF{y0u-ar3-4-tru3-t1m3-tr4v3l3r}`**

***

### **Directory (200pts)** <a href="#directory-200pts" id="directory-200pts"></a>

#### Description <a href="#description-5" id="description-5"></a>

The flag is buried in one of the directory. [Click Here](https://challs.aupctf.live/dir/)

#### Approach <a href="#approach-5" id="approach-5"></a>

The provided website has 1000 subdirectories, and only one of them contains the flag. We can write a Python script to check all the subdirectories.

**script.py**

```
import requests

base_url = "https://challs.aupctf.live/dir/page/"
format = "aupCTF{"
pages = 1000

def visit_page(page_number):
    url = base_url + str(page_number) + "/"
    print(f"Checking: {url}")
    response = requests.get(url)
    if response.status_code == 200 and format in response.text:
        print(f"Found flag on page {page_number}!")
        print(response.text)
        exit()
        

for page_number in range(1, pages + 1):
    visit_page(page_number)
```

**output**

```
┌──(kali㉿iasad)-[~/CTFs/aupctf/the-chosen-one]
└─$ python script.py
--------------------------------------------------
Checking: https://challs.aupctf.live/dir/page/709/
Checking: https://challs.aupctf.live/dir/page/710/
Checking: https://challs.aupctf.live/dir/page/711/
Checking: https://challs.aupctf.live/dir/page/712/
Found flag on page 712!
<!DOCTYPE html>
<html>
<head>
    <title>You Found Me</title
<body>
    <h1>Here is your flag, You deserve it</h1>
    <br>
    <h2>The flag is: aupCTF{d1r3ct0r13s-tr1v14l-fl4g}</h2>
</body>
</html>
```

Threading can be used to enhance the speed of the process.

***

**Flag: `aupCTF{d1r3ct0r13s-tr1v14l-fl4g}`**

***

### **Conundrum (300pts)** <a href="#conundrum-300pts" id="conundrum-300pts"></a>

#### Description <a href="#description-6" id="description-6"></a>

[Superuser](https://challs.aupctf.live/conundrum/)

#### Approach <a href="#approach-6" id="approach-6"></a>

we are presented with a login page. some digging and you find robots.txt that has 2 disallowed entries.

![Untitled](<../../../.gitbook/assets/5 (1).webp>)

Now that we have wordlists for username and password, we can proceed to initiate a brute-force attack. By examining the payload of the form, we observe that it includes three fields: username, password, and a CSRF token.

![Untitled](<../../../.gitbook/assets/6 (1).webp>)

The situation becomes interesting due to the presence of CSRF protection, which prevents us from directly brute-forcing the login using conventional methods such as Hydra

But Burp Suite’s Intruder tool can perform brute-force attack in this scenario easily.

To begin, set the attack type to “cluster bomb” within Burp Suite Intruder. Define the payload positions for both the username and password fields.

Next, configure the payload sets for the username and password fields. This allows you to input a list of possible values for each field, which will be iterated through during the attack.

Once the configurations are in place, initiate the attack by clicking the “Start Attack” button.

During the attack, carefully observe the response length. It serves as an indicator for a successful attempt.

![Untitled](../../../.gitbook/assets/7.webp)

Even though if you managed to log in with the username “starlord69” and the password “1A8$5k7!eR”, unfortunately, No flag yet.

![Untitled](../../../.gitbook/assets/8.webp)

However, it suggests that we need to log in as an admin to obtain the flag. To accomplish this, we can include the payload “admin=True” in our login request.

![Untitled](../../../.gitbook/assets/9.webp)

***

**Flag: `aupCTF{V1ct0ri0usChall3ng3r!}`**

***
