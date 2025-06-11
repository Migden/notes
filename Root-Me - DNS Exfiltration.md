
-----

This challenge was a very difficult one, it involved a pcap file that contained DNS traffic. Just looking at the requests we could tell information was being passed to a malicious DNS server via DNS exfiltration by including hexadecimal strings in the request.

I initially attempted to get all the queries and put them into a file and extract all the information. First i used GUI Wireshark and exported selected, but found tshark was easier to interact with since it was on the command line.

I was stumped as i was extracting a corrupted PNG file meaning i had got the information but some stupid issue was preventing me from analyzing the image in editors due to corruption.

I never figured it out but learnt a lot. a pretty much got the full PNG but some stupid characters messing the whole thing up

Key learning points:
- RegEx and tr are good for data manipulation
- DNS can transport information
- Their is python libraries to interact with DNS packets
- Pay attention to the format of DNS packets (Weird variations can occur)

`Grep will not return values if it is not plaintext, bypass with --text flag `

Man fuck i hate challenges like this, it was meant to be a medium bro