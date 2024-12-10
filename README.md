# Task details

**Run Knot Resolver (https://www.knot-resolver.cz/) in Docker with networking in "host" mode**

**Configure Knot Resolver to return NXDOMAIN when querying for A record of "google.com"**

**Collect tcpdump of you sending the DNS query for google.com and getting a NXDOMAIN response and prove that the response was returned to the client**

**Prepare a short presentation that can be used as a guide by anyone else to achieve the same what you did**
______________________________
10.12.

**Dockerfile** https://www.uschovna.cz/zasilka/QX57Y52GKN55SS9V-PZU

     docker run -d --name knot-resolver_cusrom1 --network host   -v /Users/Sajgon/Desktop/kresd.conf:/etc/knot-resolver/kresd.conf   cznic/knot-resolver:6
     root@docker-desktop:/etc/knot-resolver# find / -name "kresd*"
     /run/knot-resolver/kresd0.conf
     /run/knot-resolver/kresd1.conf
     /usr/sbin/kresd
     /usr/lib/knot-resolver/kres_modules/http/kresd.js
     /usr/lib/knot-resolver/kres_modules/http/kresd.css
     /etc/knot-resolver/kresd.conf

     root@docker-desktop:/etc/knot-resolver# ps aux | grep kresd 
     root        18  0.0  0.3 2245908 28928 ?       S    20:54   0:00 /usr/sbin/kresd -c kresd0.conf -n
     root        19  0.0  0.3 2245908 28948 ?       S    20:54   0:00 /usr/sbin/kresd -c kresd1.conf -n
     root        51  0.0  0.0   3076  1340 pts/0    S+   21:19   0:00 grep kresd
     
     
     root@docker-desktop:/etc/knot-resolver# cat /etc/knot-resolver/kresd.conf 
     -- SPDX-License-Identifier: CC0-1.0
     -- vim:syntax=lua:set ts=4 sw=4:
     -- Refer to manual: https://knot-resolver.readthedocs.org/en/stable/
     
     -- Network interface configuration
     net.listen('127.0.0.1', 53, { kind = 'dns' })
     net.listen('127.0.0.1', 853, { kind = 'tls' })
     --net.listen('127.0.0.1', 443, { kind = 'doh2' })
     net.listen('::1', 53, { kind = 'dns', freebind = true })
     net.listen('::1', 853, { kind = 'tls', freebind = true })
     --net.listen('::1', 443, { kind = 'doh2' })
     
     -- Load useful modules
     modules = {
             'hints > iterate',  -- Allow loading /etc/hosts or custom root hints
             'stats',            -- Track internal statistics
             'predict',          -- Prefetch expiring/frequent records
     }
     
     -- Cache size
     cache.size = 100 * MB
     modules.load('policy')
     policy.add(policy.suffix(policy.DENY, {todname('google.com.')}))
          
     
        
<!--  docker pull cznic/knot-resolver     
          docker run --rm --network=host -v ~/knot-resolver/kresd.conf:/etc/knot-resolver/kresd.conf cznic/knot-resolver
          docker run -d --name knot-resolver --network host cznic/knot-resolver
               docker run -d --name knot-resolver --network host cznic/knot-resolver:6 -->
          
  
