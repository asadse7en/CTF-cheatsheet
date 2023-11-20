# OSINT

### **Git (100pts)** <a href="#git-100pts" id="git-100pts"></a>

#### Description <a href="#description" id="description"></a>

Do You Know! The current CTF you’re participating in is actually running on my BSCS final year project, called [`fypCTF`](https://github.com/asadse7en/fypCTF). Why not take a peek and see if you can find anything interesting? **Flag format: `aupCTF{your-answer}`**

#### Approach <a href="#approach" id="approach"></a>

visiting the GitHub repo we can see the l33t words in a tag [5t4r-th3-r3p0](https://github.com/topics/5t4r-th3-r3p0)

![Untitled](https://about/write-ups/aupctf/osint/1.webp#center)

***

**Flag: `aupCTF{5t4r-th3-r3p0}`**

***

### **Ash (100pts)** <a href="#ash-100pts" id="ash-100pts"></a>

#### Description <a href="#description-1" id="description-1"></a>

Throughout my gaming journey, I have achieved the incredible feat of being a two-time back-to-back Combo Breaker Champion. I’m curious if you can find the exact count of tournaments I have emerged victorious in my primary game.

**Flag format: `aupCTF{count}`**

#### Approach <a href="#approach-1" id="approach-1"></a>

A quick Google search reveals that the challenge revolves around Arslan Ash, who impressively secured the title of Combo Breaker Champion two times in a row. Arslan Ash has emerged victorious in numerous tournaments

for reliable sports data, [Liquipedia](https://liquipedia.net/fighters/Arslan\_Ash/Results) as a credible source. According to Liquipedia, Arslan Ash has won a total of 19 taken 7 tournaments.

***

**Flag: `aupCTF{19}`**

***

### **Centurion (100pts)** <a href="#centurion-100pts" id="centurion-100pts"></a>

#### Description <a href="#description-2" id="description-2"></a>

One of the oldest Institution created by the person in the photo. Your task is to find the institution created by him and find the first ever-batch strength and the date it opened.

[centurion.png](https://aupctf.s3.eu-north-1.amazonaws.com/Centurion.png)

**Flag Format: `aupCTF{dd/mm/yy_strengthofthebatch}`**

#### Approach <a href="#approach-2" id="approach-2"></a>

reverse search the image and you will find that the person in the photo is Sir Sahibzada Abdul Qayyum who created Islamia Collage Peshawar

you can find the creation date and the strength of first batch in the following 2 articles

[Historical Background](https://icp.edu.pk/page.php?abc=201506230501115)

_The College began its instructional activities, six months later i.e on 1st October 1913._

[Islamia College, Peshawar](https://www.topuniversities.com/universities/islamia-college-peshawar)

_The college, which began its educational voyage with just 33 students in 1913, became a full-fledged University in 2008._

***

**Flag: `aupCTF{1/10/1913_33}`**

***

### **Records (200pts)** <a href="#records-200pts" id="records-200pts"></a>

#### Description <a href="#description-3" id="description-3"></a>

Our website has been hacked, and the attackers have hidden a flag in an unexpected location in a **txt**. To find the flag, you’ll need to look beyond the usual pages and directories on our website. Keep in mind that the attackers may have used clever tricks to hide the flag, so you’ll need to be creative in your search. Remember, the flag may be hiding in plain sight, but you’ll need to know where to look. Good luck!

[website](https://iasad.me/)

#### Approach <a href="#approach-3" id="approach-3"></a>

looking at the DNS records of [iasad.me](https://iasad.me/) using [dnsrecords.io](http://dnsrecords.io/) we can find the flag in the txt record

![Untitled](https://about/write-ups/aupctf/osint/2.webp#center)

***

**Flag: `aupCTF{st0p-l00k1ing-my-dns-r3c0rds}`**

***

### **Wisdom (200pts)** <a href="#wisdom-200pts" id="wisdom-200pts"></a>

#### Description <a href="#description-4" id="description-4"></a>

I was curious to discover the total number of books present within our library. help me find it

[photo](https://aupctf.s3.eu-north-1.amazonaws.com/view.jpg)

**Flag format: `aupCTF{TotalBooks-TotalJournals}`**

#### Approach <a href="#approach-4" id="approach-4"></a>

By conducting a reverse image search, you can easily identify the location as the Library of Agriculture University Peshawar. Simply search for “Agriculture University Peshawar library” and you will come across the official webpage of the library, which can be found [**here**](http://www.aup.edu.pk/library.php).

![Untitled](https://about/write-ups/aupctf/osint/3.webp#center)

***

**Flag: `aupCTF{113600-11605}`**

***

### **Don’t copyvio me (200pts)** <a href="#dont-copyvio-me-200pts" id="dont-copyvio-me-200pts"></a>

#### Desciption <a href="#desciption" id="desciption"></a>

I love Wikipedia because it’s free and open source to view - but I also hate it because people can remove content if they think it’s a “copyright violation” - even if it’s not. Our University kept having that happen to us - but thankfully our page looks pretty great right now!

Can you tell me who kept doing that to the university and the total bytes of data they deleted? Don’t use any commas.

**Flag format: `aupCTF{username_#}`**

#### Approach <a href="#approach-5" id="approach-5"></a>

Visit the Wikipedia page of Agriculture University Peshawar and click on “[View History](https://en.wikipedia.org/w/index.php?title=University\_of\_Agriculture,\_Peshawar\&action=history\&offset=\&limit=500)” to access the revision history. Perform a search for “copy” within the revisions, and you will discover a few relevant results. However, note the title “**Don’t copyvio me**”. Therefore, further searching for “**copyvio**” yields only two results, both made by user: **Joelmills**. On first time, he deleted approximately 10,003 bytes, and on second time, approximately 9,966 bytes were removed.

***

**Flag: `aupCTF{Joelmills_19969}`**

***

### **About-Face (300pts)** <a href="#about-face-300pts" id="about-face-300pts"></a>

#### Description <a href="#description-5" id="description-5"></a>

I’d love to work for a social media company when they’re just starting out. Imagine getting a job at thefacebook, I mean facebook, I mean Meta - whatever they want to go by these days, way back when?

Come to think of it, dropping the from their name was probably the smartest idea they ever had. My uncle said he applied for a role with their Network Operations team after he heard that they dropped ’the’ from their name, but never heard back and thinks it’s because the person he emailed left their job.

I don’t believe him, but he told me I can always reach out to the person he emailed to confirm. I doubt they still work there, but can you tell me the role he applied for and the first name of the person he reached out to? He said it should be easy to figure out - that team had only one role available that year and he applied before December.

**Flag Format: `aupCTF{role_title_firstname}` All lowercase.**

#### Approach <a href="#approach-6" id="approach-6"></a>

There are a few important points from the description:

* when did facebook dropped the from Thefacebook? **In 2005**
* when did his uncle applied for the job? **before December 2005**
* his Uncle applied in the network operations team

It is well-known that Facebook changed its domain in 2005. Therefore, to gather information about Facebook prior to this change, we should explore the archives before December of that year. By utilizing the Wayback Machine and searching for facebook.com, we can access numerous snapshots. Our focus lies on the year 2005, specifically before December.

![Untitled](https://about/write-ups/aupctf/osint/4.webp#center)

Let’s examine the snapshot from November 27, 2005

![Untitled](https://about/write-ups/aupctf/osint/5.webp#center)

Upon examining the jobs page, various positions are listed. However, the specific job we are interested in can be found within the operations department.

![Untitled](https://about/write-ups/aupctf/osint/6.webp#center)

***

**Flag: `aupCTF{senior_linux_systems_administrator_robin}`**

***
