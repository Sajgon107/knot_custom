# Task details

**Run Knot Resolver (https://www.knot-resolver.cz/) in Docker with networking in "host" mode**

**Configure Knot Resolver to return NXDOMAIN when querying for A record of "google.com"**

**Collect tcpdump of you sending the DNS query for google.com and getting a NXDOMAIN response and prove that the response was returned to the client**

**Prepare a short presentation that can be used as a guide by anyone else to achieve the same what you did**
______________________________
     docker pull cznic/knot-resolver     
     docker run --rm --network=host -v ~/knot-resolver/kresd.conf:/etc/knot-resolver/kresd.conf cznic/knot-resolver
     docker run -d --name knot-resolver --network host cznic/knot-resolver
          docker run -d --name knot-resolver --network host cznic/knot-resolver:6

          
  
