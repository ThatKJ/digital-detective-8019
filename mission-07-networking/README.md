# Mission 7 — How computers communicate

## 1. Task / objective

Explain the basic network types and concepts, test whether my laptop can reach a
public website, look up the address behind a domain name, and describe what
happens step by step when a browser opens a website.

## 2. Work completed

### Task 7.1 — Network concepts

| Concept | Explanation in my own words | Example |
|---|---|---|
| LAN | A network inside one small area, usually one building or one room, where the devices are close enough to be connected by one router or switch. | My home Wi-Fi. The laptop, the phone and the TV are all on the same LAN and can talk to each other without going out to the internet. |
| MAN | A network that is bigger than a building but still limited to one city or a large campus. Usually several LANs joined together. | A college campus with separate networks in each block, or a city cable operator serving one area. |
| WAN | A network that covers a large geographical area, connecting cities or countries. The internet is the biggest WAN. | A bank connecting its branches in different cities, or the internet itself. |
| DNS | The naming system that turns a name I can read into the numeric address a computer needs. It is a lookup service, not a connection. | Typing `example.com` and getting back `172.66.147.243`. |
| Router | A device that joins two or more networks and decides where to send each packet next. At home it is the box that joins my LAN to my ISP's network. | My home router sending my request out to the internet and the reply back to my laptop. |
| Protocol | An agreed set of rules for how two devices format, send and acknowledge data. Without a shared protocol the bytes arrive but mean nothing. | HTTP for web pages, TCP for reliable delivery, IP for addressing, DNS for name lookup. |
| Packet switching | Data is cut into small packets. Each packet carries the destination address and can take a different path. They are put back in order at the other end. | A photo I upload leaves as many packets, and they do not all travel the same route. |
| Client-server | One computer asks for something and another supplies it. The client starts the conversation; the server waits and responds. | Safari on my laptop (client) asking a web server for `example.com` and getting the page back. |

### Task 7.2 — Connectivity and DNS observations

**Connectivity test.** I ran `ping -c 4 example.com`. The real result:

    PING example.com (172.66.147.243): 56 data bytes
    64 bytes from 172.66.147.243: icmp_seq=0 ttl=55 time=79.504 ms
    64 bytes from 172.66.147.243: icmp_seq=1 ttl=55 time=57.609 ms
    64 bytes from 172.66.147.243: icmp_seq=2 ttl=55 time=62.505 ms
    64 bytes from 172.66.147.243: icmp_seq=3 ttl=55 time=65.910 ms

    4 packets transmitted, 4 packets received, 0.0% packet loss
    round-trip min/avg/max/stddev = 57.609/66.382/79.504/8.130 ms

**What a connectivity test shows.** It shows whether small test packets can
reach that host and come back. Four were sent, four came back, and nothing was
lost, so the path from my laptop to that server was working at that moment. It
also gives the round-trip time, about 66 ms on average, which is roughly how long
one packet needs to go and return.

**What it cannot establish.** It does not prove the website works. A server can
answer ping and still return an error page, and many servers block these test
packets completely while the website is fine. It says nothing about the port or
service, so it cannot tell me whether the web server itself is running. It also
does not measure how fast a page will load, because a page is many kilobytes and
the test was four small packets.

**DNS lookup.** I ran `nslookup example.com`, `host example.com` and
`dig example.com +short`. The real result:

    $ nslookup example.com
    Server:		8.8.8.8
    Address:	8.8.8.8#53

    Non-authoritative answer:
    Name:	example.com
    Address: 104.20.23.154
    Name:	example.com
    Address: 172.66.147.243

    $ host example.com
    example.com has address 104.20.23.154
    example.com has address 172.66.147.243
    example.com has IPv6 address 2606:4700:10::6814:179a
    example.com has IPv6 address 2606:4700:10::ac42:93f3
    example.com mail is handled by 0 .

**What a DNS lookup displays.** The IP address or addresses that the name points
to. It also shows which DNS server answered (in my case a public resolver at
8.8.8.8, which is a service anyone can use, not my own address), and for some
domains the IPv6 addresses and the mail server. This domain returned two IPv4
addresses, which is normal: large sites are served from more than one machine so
traffic can be shared.

**What it cannot establish.** That the server is reachable, that the site is up,
or that the browser will load anything. It also does not tell me which of the two
addresses my browser will use. A correct DNS answer only means the name is
mapped to an address.

**The role of DNS when I type a website name.** A browser cannot connect to a
name, only to an address. So the first thing that has to happen is a DNS lookup
that converts `example.com` into something like `172.66.147.243`. Only after
that answer arrives can a connection be opened.

I did not publish my own IP address or Wi-Fi name, and I did not run
`traceroute`, because its first lines show the local router address on my home
network.

### Task 7.3 — What happens when you open a website

1. I type `example.com` into the browser. The browser (the **client**) checks its
   cache, then asks the operating system to resolve the name.
2. The request goes to a **DNS** server. DNS replies with the IP address for that
   name, for example `172.66.147.243`.
3. The client opens a connection to that address. The packets leave my laptop,
   go to my **router**, and the router forwards them towards my internet
   provider and onwards.
4. The packets travel across the network using **packet switching**, so they may
   take different routes and are reassembled in order at the destination.
5. The request reaches the **server**, which reads it. Both sides follow the same
   **protocol** (HTTPS over TCP/IP), so each understands the format of the other.
6. The server sends a **response**: a status code, some headers and the page
   content, again as packets.
7. The browser receives the response, reads the HTML, asks for the images, CSS
   and scripts it needs, and draws the finished page on screen.

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `ping -c 4 example.com` | Sends four test packets to check whether the host can be reached and how long the round trip takes. |
| `nslookup example.com` | Asks the configured DNS server which address belongs to the name. |
| `host example.com` | Does the same lookup and also shows IPv6 and mail records. |
| `dig example.com +short` | A shorter lookup that prints only the addresses. |
| Terminal and a browser | To run the commands and cross-check the site. |

## 4. My understanding

Before this mission I thought opening a website was one action. It is at least
three separate ones: finding the address (DNS), getting the data there and back
(IP and routing), and understanding that data (HTTP). Each one can fail on its
own, which explains why "the internet is down" covers several different problems.

DNS is the part I found most interesting. The name is only for people. The
computer works entirely with numbers, and DNS is the translation service that
hides those numbers from me.

The connectivity test taught me to be careful about what a result proves. Four
replies and zero loss looked like a clean bill of health, but it only proves the
path to that one host worked for those four packets. It says nothing about the
web page.

Packet switching also explains something practical: a large file does not need a
single unbroken connection. It can be spread across many paths and put back
together, which is why the internet keeps working when one route is busy or
broken.

## 5. Difficulties faced

- `ping` printed an IP address even though I typed a name, which means DNS was
  already used before ping started. I had thought of them as separate steps.
- `nslookup` said "Non-authoritative answer" and I did not know if that meant the
  result was untrustworthy.
- The two tools gave the addresses in a different order, and `host` showed four
  addresses while `dig` showed two.
- I was not sure what I was allowed to paste, since the command output contains
  addresses.

## 6. How I resolved them

- I realised `ping` has to resolve the name first, which is exactly the DNS step.
  Seeing the address in the first line was proof that the lookup happened.
- I read "non-authoritative" as "this answer came from a cache, not straight from
  the domain's own server". It is still a real answer, it just may be a few
  minutes old.
- I understood that one name can point to several machines, and tools show them
  in whatever order the answer arrives. Both tools were reporting the same set.
  `dig +short` printed only IPv4 addresses by default, which is why it showed
  fewer lines than `host`.
- I decided to publish only the public example domain and its addresses, and to
  leave out anything about my own network: no local IP, no router address, no
  Wi-Fi name. I also skipped `traceroute` for that reason.

## 7. Evidence / files

- `mission-07-networking/README.md` - this file.
- `evidence/mission-07/connectivity-test.txt` - real `ping` output.
- `evidence/mission-07/dns-lookup.txt` - real `nslookup`, `host` and `dig`
  output.

## 8. Commit details

Commit message:

    Explain networking concepts and website communication

Pushed to `main` on GitHub.
