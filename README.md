![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat) <a href="https://twitter.com/tamimhasan404">
    <img src="https://img.shields.io/badge/author-@tamimhasan404-orange.svg?style=square&logo=twitter">
  </a>

# FFUF-Tips-And-Tricks

![maxresdefault](https://user-images.githubusercontent.com/66991901/106985150-167bd600-6793-11eb-95ab-dfb5774192f0.jpg)


### So what is ffuf?

Ffuf(fuzz faster u fool) is a great tool used for fuzzing. It has become really popular lately with bug bounty hunters/penetration tester. It is written in Go language.For this you can fuzz a large amount of words within a minute.

### Before using ffuf tool just see this image once

![Screen-Shot-2017-02-26-at-6 54 41-AM](https://user-images.githubusercontent.com/66991901/106984127-2eeaf100-6791-11eb-8d98-da088f374a53.png)

## wordlist:

Option name: -w

Use wordlist on ffuf for more affectively fuzzing. I use SecLists-master for example. You can choose yours. I have my own for dir brute forcing you can find it on https://github.com/tamimhasan404/wordlist.git

```
./ffuf -w /root/Desktop/SecLists-master/Discovery/Web-Content/raft-large-directories.txt -u https://xyz.com/FUZZ
```

/root/Desktop/SecLists-master/Discovery/Web-Content/raft-large-directories.txt this is just a path where is the wordlist is situated.

## Fuff with all domain

This is a common problem for beginners that they don’t know how to use fuff in all of their collected subdomains as fuff has no default option for list of domains like dirsearch. So here is something for you which I found in https://twitter.com/0xJin tweet.

```
cat live.txt | xargs -I@ sh -c 'ffuf -w wordlists.txt -u @/FUZZ -mc 200'
```

## Filtering:


Option name: -fc

If you don’t want to see any kind of specific status code then you can just filter them.

```
./ffuf -w /root/Desktop/SecLists-master/Discovery/Web-Content/raft-large-directories.txt -u https://xyz.com/FUZZ -fc 401,403,404
```
Comma-separated list of codes and ranges


## Recursion:

Option name: -recursion

With this option, it tries to find all possible dir accordingly your given wordlist. Let me explain if ffuf find /index.php dir then it fuzz it again with /index.php/wordlist. 
Suppose it finds/index.php/configtest.php then it fuzz it again like this /index.php/configtest.php/wordlist.

```
./ffuf -w /root/Desktop/SecLists-master/Discovery/Web-Content/raft-large-directories.txt -u https://xyz.com/FUZZ -recursion
```

## Recursion-Depth:

Option name: -recursion-depth

By default recursion depth level is 0.with this you set how many specific numbers of dir it find for you. Like 2,3 or 4 etc.

```
./ffuf -w /root/Desktop/SecLists-master/Discovery/Web-Content/raft-large-directories.txt -u https://xyz.com/FUZZ -recursion-depth 2
```
Here you see I set recursion-depth 2. Now ffuf find 2 dir basis of my wordlist if these dir are available on the targeted website then stop.


## Extention:

Option name: -e

```
./ffuf -w /root/Desktop/SecLists-master/Discovery/Web-Content/raft-large-directories.txt -u https://xyz.com/FUZZ -e .html,.php,.txt,.pdf
```
Sometimes it gives you valuable information. Which is maybe goldmine on your penetration testing/bug hunting.For this, you have to choose extension base on your target.


## Silent:

Option name: -s

If you just print the result and don’t see any kind of fuzzing process on your terminal then use silent option.

```
./ffuf -w /root/Desktop/SecLists-master/Discovery/Web-Content/raft-large-directories.txt -u https://xyz.com/FUZZ -s
```

## Output:

Choose one -of json, ejson, html, md, csv

I generally use | tee for result output. But if you want to get output on GUI(graphical user interface) for your better understand/client demand then your CM is.

```
./ffuf -w /root/Desktop/SecLists-master/Discovery/Web-Content/raft-large-directories.txt -u https://xyz.com/FUZZ -of html -o ffuf-result
```

## Subdomain Enumeration

```
./ffuf -w /root/Desktop/wordlist.txt -u http://FUZZ.ab.com -of html -o result
```
Remember use http:// protocol after "-u" because sometimes many subdomains do not run over https.

## Throttle(Last one but an important one)

Option name: -rate 2 (set your number 2,3 etc)

This is very useful because with this you throttle/delay your request. As you know ffuf is very fast tool with that a large number of wordlist makes much noise on the server which may cause to block your IP,Dos,Slow down the server etc. To avoid this you can use -rate and your CM is.

```
./ffuf -w /root/Desktop/SecLists-master/Discovery/Web-Content/raft-large-directories.txt -u https://xyz.com/FUZZ -rate 2
```
rate 2 means two requests per second. You can also customize the number.

- Here are some other useful options on ffuf:

timeout → HTTP request timeout in seconds (default: 10)

-V → Show version information (default: false/off)

-t → Number of concurrent threads(default: 40)

-v → Verbose/details output,printing full URL and redirect location (if any) with the results (default:false/off)

-mc → Match HTTP status codes, or "all" for everything (default: 200,204,301,302,307,401,403)

mode → Multi-wordlist operation mode.Available modes: clusterbomb, pitchfork (default: clusterbomb(1 to 1,2 to 2)

Thank you💕 

### To dig deep

https://youtu.be/aN3Nayvd7FU     
                                  
https://youtu.be/iLFkxAmwXF0
                                 
https://youtu.be/IjHrwKAmGn8     



