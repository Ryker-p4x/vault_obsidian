- Application data is wrapped in headers sequentially (TCP/UDP headers at Transport, IP headers at Network, and Ethernet frames at Data Link) as it moves down the network stack.
    
- Intermediate hardware unpacks (decapsulates) and repacks these headers to route packets across the internet to their destination.