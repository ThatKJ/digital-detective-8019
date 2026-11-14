# Mission 7 — How computers communicate

## 1. Task / objective

Explain the basic network types and ideas, test whether my laptop can reach a
public website, look up the address behind a domain name, and describe what
happens step by step when a browser opens a page.

## 2. Work completed

### Task 7.1 — Network concepts

| Concept | What it means, in my words | Example |
|---|---|---|
| LAN | A network in one small area, usually one room or building, where devices are close enough to share one router or switch. | My home Wi-Fi. The laptop, phone and TV are all on it and can talk to each other without going out to the internet. |
| MAN | Bigger than a building but still one city or large campus. Usually several LANs joined together. | Separate networks in each block of a college campus, or a city cable operator serving one area. |
| WAN | Covers a large area and joins cities or countries. The internet is the biggest WAN. | A bank linking branches in different cities, or the internet itself. |
| DNS | The naming system that turns a name I can read into the number a computer needs. It is a lookup, not a connection. | Typing `example.com` and getting back `172.66.147.243`. |
| Router | A device that joins two or more networks and decides where each packet goes next. At home it is the box between my LAN and my provider. | My home router sending my request out and the reply back to my laptop. |
| Protocol | Rules both sides agree on for how data is laid out, sent and acknowledged. Without them the bytes arrive but mean nothing. | HTTP for pages, TCP for reliable delivery, IP for addressing, DNS for names. |
| Packet switching | Data is cut into small packets. Each one carries the destination and can take a different route, and they are put back in order at the other end. | A photo I upload leaves as many packets, and they do not all go the same way. |
| Client-server | One computer asks, another answers. The client starts it, the server waits and replies. | Safari on my laptop asking a web server for `example.com`. |

### Task 7.2 — Connectivity and DNS

**Reaching a host.** I ran `ping -c 4 example.com`. The real result:

    PING example.com (172.66.147.243): 56 data bytes
    64 bytes from 172.66.147.243: icmp_seq=0 ttl=55 time=79.504 ms
    64 bytes from 172.66.147.243: icmp_seq=1 ttl=55 time=57.609 ms
    64 bytes from 172.66.147.243: icmp_seq=2 ttl=55 time=62.505 ms
    64 bytes from 172.66.147.243: icmp_seq=3 ttl=55 time=65.910 ms

    4 packets transmitted, 4 packets received, 0.0% packet loss
    round-trip min/avg/max/stddev = 57.609/66.382/79.504/8.130 ms

**What this test shows.** Whether small test packets can get to that host and come
back. Four went out, four came back, nothing was lost, so the path from my laptop
to that server worked at that moment. It also gives the round trip, about 66 ms
on average, which is roughly how long one packet takes to go and return.

**What it cannot show.** It does not prove the website works. A server can answer
ping and still hand back an error page, and plenty of servers block these test
packets completely while their website is perfectly fine. It says nothing about
ports or services, so it cannot tell me whether the web server is running. It
also does not predict how fast a page will load, because a page is many
kilobytes and I sent four tiny packets.

**Looking up the name.** I ran `nslookup example.com`, `host example.com` and
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

**What this shows.** The address or addresses the name points to. It also shows
which DNS server answered, in my case a public resolver at 8.8.8.8, which anyone
can use and is not my own address. For some domains it shows IPv6 addresses and
the mail server too. This domain returned two IPv4 addresses, which is normal,
because big sites are served from more than one machine so traffic can be
shared.

**What it cannot show.** That the server is reachable, that the site is up, or
that a browser will load anything. It also cannot tell me which of the two
addresses my browser will actually use. A correct DNS answer only means the name
is mapped to an address.

**Why DNS matters when I type a name.** A browser cannot connect to a name, only
to an address. So the very first thing that has to happen is a lookup that turns
`example.com` into something like `172.66.147.243`. Only after that answer
arrives can a connection be opened.

I did not publish my own IP address or my Wi-Fi name, and I skipped `traceroute`,
because its first lines show the local router address on my home network.

### Task 7.3 — What happens when you open a website

1. I type `example.com`. The browser, which is the **client**, checks its own
   cache, then asks the operating system to resolve the name.
2. The question goes to a **DNS** server. It answers with an address such as
   `172.66.147.243`.
3. The client opens a connection to that address. The packets leave my laptop, go
   to my **router**, and the router passes them towards my provider and onwards.
4. On the way they use **packet switching**, so different packets may travel
   different routes and get reassembled in order at the far end.
5. The request reaches the **server**, which reads it. Both sides follow the same
   **protocol**, HTTPS over TCP/IP, so each understands the other's format.
6. The server sends back a **response**: a status code, some headers and the page
   content, again as packets.
7. The browser reads the HTML, asks for the images, CSS and scripts it needs, and
   draws the page on screen.

## 3. Commands / tools used

| Command | Purpose |
|---|---|
| `ping -c 4 example.com` | Sends four test packets to see if the host can be reached and how long the round trip takes. |
| `nslookup example.com` | Asks the configured DNS server which address belongs to the name. |
| `host example.com` | Does the same lookup and also shows IPv6 and mail records. |
| `dig example.com +short` | A shorter lookup that prints only the addresses. |
| Terminal and a browser | To run the commands and cross-check the site. |

## 4. My understanding

Before this mission I thought opening a website was one action. It is at least
three. Finding the address is DNS, getting data there and back is IP and routing,
and understanding that data is HTTP. Each one can fail on its own, which explains
why "the internet is down" can mean several completely different problems.

DNS is the part I found most interesting. Names are for people. The computer
works entirely in numbers, and DNS is the service that hides those numbers from
me.

The connectivity test taught me to be careful about what a result actually
proves. Four replies and zero loss looked like a clean bill of health, but it
only covers four small packets on one path. It says nothing about the web page.

Packet switching explains something practical too. A big file does not need one
unbroken connection. It can be spread across many routes and rebuilt at the other
end, which is why the internet keeps working when a path is busy or broken.

## 5. Difficulties faced

- `ping` printed an IP address even though I typed a name, so DNS had already
  happened before the test even started. I had thought of them as separate steps.
- `nslookup` said "Non-authoritative answer" and I could not tell whether that
  meant the result was untrustworthy.
- The tools listed the addresses in a different order, and `host` showed four
  where `dig` showed two.
- I was not sure what I was allowed to paste, because the output contains
  addresses.

## 6. How I resolved them

- I realised `ping` has to resolve the name before it can send anything, so the
  address on the first line is the lookup happening right in front of me.
- I read "non-authoritative" as "this answer came from a cache, not straight from
  the domain's own server". It is still a real answer, it may just be a few
  minutes old.
- I understood that one name can point to several machines, and tools show them
  in whatever order they arrive. Both tools were reporting the same set.
  `dig +short` printed only IPv4 by default, which is why it showed fewer lines.
- I decided to publish only the public example domain and its addresses, and to
  keep everything about my own network out: no local IP, no router address, no
  Wi-Fi name. That is also why I skipped `traceroute`.

## 7. Evidence / files

- `mission-07-networking/README.md` - this file.
- `evidence/mission-07/connectivity-test.txt` - the real `ping` output.
- `evidence/mission-07/dns-lookup.txt` - the real `nslookup`, `host` and `dig`
  output.

## 8. Commit details

Commit message:

    Explain networking concepts and website communication

Pushed to `main` on GitHub.
