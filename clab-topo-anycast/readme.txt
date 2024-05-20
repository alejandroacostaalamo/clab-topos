+--------+   +----------+   +-------+                 +---------+
| Client |---| R1       |---| R2    |-----------------| ServerA |
|        |   |AS65001   |   |AS65002|                 | POP-A   |
+--------+   +----------+   +-------+                 | AS65000 |
                |    /                                +---------+
                |   /
                |  /
             +--------+          +-------+            +---------+
             | R3     |----------| R4    |------------| ServerB |
             |AS65003 |          |AS65004|            | POP-B   |
             +--------+          +-------+            | AS65000 |
                |    /                                +---------+
                |   /
                |  /
             +-------+   +-------+                 +---------+
             | R5    |---| R6    |-----------------| ServerC |
             |AS65005|   |AS65006|                 | POP-C   |
             +-------+   +-------+                 | AS65000 |
                                                   +---------+


IP Addressing
Client: 2001:db8:1::/64
R1-R2: 2001:db8:12::/64
R1-R3: 2001:db8:13::/64
R2-R3: 2001:db8:23::/64
R3-R4: 2001:db8:34::/64
R3-R5: 2001:db8:35::/64
R4-R5: 2001:db8:45::/64
R5-R6: 2001:db8:56::/64
R2-ServerA: 2001:db8:2a::/64
R4-ServerB: 2001:db8:4b::/64
R6-ServerC: 2001:db8:6c::/64
All POP announcing: 2001:db8:ffff::/48 from AS 65000

Scenario:	
– Announce the same address space from multiple POPs	
– Multiple paths in BGP, best one selected based on policy	
- Using BGP ADDPATH in one router to make it more educational

• Benefits:	
– Increased reliability	
– Traffic Engineering
– Improved performance	
– Localized impact of DoS attacks	

Each pop:
– Announce one /48 via BGP (2001:db8:ffff::/48)
– Static default route to the provider in each POP

Recommended testing:
.- Check BGP and Routing table in different routers, at least in:
 .- frr1, frr2, frr3
.- From the client (client) you can wget http://testanycast.acostasite.com
.- Check the index.html (more index.html) you downloaded in should say ServerA
.- Delete index.html (rm index.html)
.- Shutdown BGP session in serverA
.- Wait one min and then from the client (client) wget http://testanycast.acostasite.com
.- Check the index.html (more index.html) you downloaded in should say Serverb
.- Then shutdown BGP session in serverB
.- Wait one min and then from the client (client) wget http://testanycast.acostasite.com
.- Check the index.html (more index.html) you downloaded in should say ServerC


