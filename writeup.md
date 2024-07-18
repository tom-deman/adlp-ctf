# Write-up ADLP CTF

## Project Context

You are hired to do a recognition test (and only passive recognition) for the company adlp-corp.com.

<https://adlp-corp.com/>
Using all the techniques you learn to gather information, try to know your target as well as possible.

You have to find 9 flags that prove your passage. Be careful, not all flags have the same syntax.

---

<br>

- The first step I did was browsing the website: <https://adlp-corp.com/> and I used the right click "show source code" option.
I found the first flag in the source code by using "ctrl + f" and looking for ADLP guessing that the flags might start with ADLP{something}.

ADLP{HTML_COMMENT_FL4G_G456688}

<br>

- The second one is also in the source code at the end of the javascript tag where we see:

```javascript
const t = 'QURMUHtKU19DT05TT0xFX0c3ODk0NDE5ODE2fQ=='
console.log(atob(t))
```

Executing this javascript code reveal this:
(Note that we can retrieve this flag by just looking into the javascript console of the website)

ADLP{JS_CONSOLE_G7894419816}

<br>

- For the third one I went to see what files I could find in the website sources.
I browsed to the "main.js" file where another call to atob() is done. (since atob is used to decode base64 it was easy to guess something was hidden there) I just printed the result of this code with a console.log() to see what the variable's content was:
(Note that we can also retrieve this flag just by looking into the cookies of the website)

```javascript
const f= 'VlZaV1UxUldWa2xrUlhSV1RWUnNSVlpFUVRWVVJrNVdWbXhTV1UxSFRYcFVNRkp5VFVVMVZWVlVTazlXUm1zeFZEQlNSazF0V2xKUVZEQTk='
const v='F=' + atob(atob(atob(atob(f)))) + ';'
console.log( v )
```

ADLP{JS_COOKIES_G7894546569816}

<br>

- For the fourth flag I inspected the css files (same as I did earlier with the main.js ) and in the main css file as a css comment we see:

ADLP{CSS_HSBUSGYIG569816}

<br>

- For the fifth and six flag I tried to find popular files like sitemap and robots.txt. So I simply tried to add /robots.txt at the end of the url and that gave me the flag:

ADLP{ROBOTS_TXT_G569816}

<br>

- Sixth flag is the same as the previous one but with /sitemap.txt at the end of the url:

ADLP{SITM4PAS_XML_G569816}

<br>

- For the flag 7 I did a search on <https://whois.domaintools.com> and searched for "adlp-corp.com" and found nothing interesting except the ip: 52.51.133.160.
With this IP I used Shodan to find more infos and fell on this: (TXT domain):

BC{DESCRIPTIVE-DOMAIN-TXT}

<br>

At this point I was a bit stuck and still had to find 2 flags.

- I downloaded the images and used steghide to see if the pdf was hidden in an image but couldn't find anything.
- I also used exiftool with those images but ... nothing.
- I tried to find the adress of the company on google map but it lead nowhere.
- I Tried to use different passive enumeration website but still nothing more.
- I Tried to see if the mobile version was different but I dind't found anything interesting.
- I tried to use the wayback machine but the website seems identical 2 years ago and now.
