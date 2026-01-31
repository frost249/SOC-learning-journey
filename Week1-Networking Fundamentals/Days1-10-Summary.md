# Week 1 Progress: Days 1-10 Summary

**Period:** January 21-31, 2026  
**Total Hours:** ~25 hours  
**Status:** Behind schedule but actively learning

## What I Accomplished

### Wireshark Packet Analysis
**Skills Acquired:**
- Can identify victim's IP address in PCAP files
- Understand basic packet structure (headers, payload)
- Know how to use display filters
- Can extract malicious files

**Filters I Learned:**
```
http.request               # Find HTTP requests
tcp.flags.syn==1          # Find SYN packets
dns                       # DNS traffic
ip.src == X.X.X.X        # Filter by source IP
http.request.method == "GET"  # Find GET requests
```

**PCAPs Analyzed:**
1. **Exercise: 2014-11-15-Rig-EK-traffic.pcap**
   - Found victim IP: 172.16.165.165
   - Extracted file hash.
   - Malicious domain: 24corp-shop.com

2. **Exercise: Live Traffic**
   - Victim IP: 10.0.2.15
   - Decrypted TLS using SSLKEYLOG.

3. **Exercise - 2024-11-26-traffic-analysis-exercise.pcap (In Progress)**
   - Challenge: Multiple compromised websites
   - Still investigating: A '.cab' file has been found for windows update

### Subnetting Mastery
**Skills Acquired:**
- Can calculate subnet masks manually
- Understand CIDR notation (/24, /16, etc.)
- Know how to find network and broadcast addresses
- Learned VLSM (Variable Length Subnet Masking)

**Example Calculations I Can Do:**
```
192.168.1.0/24
├── Network: 192.168.1.0
├── Broadcast: 192.168.1.255
├── First usable: 192.168.1.1
├── Last usable: 192.168.1.254
└── Total hosts: 254

10.0.0.0/16
├── Network: 10.0.0.0
├── Broadcast: 10.0.255.255
└── Total hosts: 65,534
```

**Confidence Level:** 80% - Can subnet in my head now

### Network Concepts
- TCP vs UDP differences
- Three-way handshake (SYN, SYN-ACK, ACK)
- NAT (Network Address Translation)
- Common ports memorized: 21, 22, 23, 25, 53, 80, 443, 445, 3389

### Tools & Commands
**md5sum:**
```bash
md5sum malicious_file.exe  # Calculate file hash
```

**Basic network commands:**
```bash
ip addr show               # Show interfaces
ping -c 4 google.com      # Test connectivity
nslookup google.com       # DNS lookup
```

## Challenges Faced

1. **Advanced PCAPs are difficult**
   - Complex attack chains hard to follow
   - Multiple compromised websites confusing
   - Need more practice.

2. **Time management**
   - Initially planned 10 hrs/day
   - Actually doing 2-4.5 hrs/day
   - Need to increase consistency

3. **Documentation gap**
   - Learned a lot but didn't document
   - Starting GitHub late (Day 10)
   - Will commit daily going forward

## Skills Assessment

| Skill | Before | Now | Target |
|-------|--------|-----|--------|
| Wireshark | 0/10 | 5/10 | 8/10 |
| Subnetting | 2/10 | 8/10 | 9/10 |
| Network Concepts | 3/10 | 6/10 | 8/10 |
| PCAP Analysis | 0/10 | 4/10 | 7/10 |

## What's Working

- Hands-on practice with real PCAPs
- Subnetting clicked after practice
- Understanding packet structure improving
- Starting to see patterns in malicious traffic

## What Needs Improvement

- Increase daily study hours (target: 8-10 hrs)
- Document learning immediately
- Follow structured plan more closely
- Ask for help when stuck

**Date Documented:** January 31, 2026  
**Next Update:** Daily commits starting Day 11
