# SECTION 6 | ROUTE53

## General Notes

- Will come up about 4-5 times in your exam
- If you ever work for Amazon, the origin of the term Route53 may be asked

## DNS

- Convert human friendly domain names into an IPv4 or IPv6 address
- IPv4 space is a 32 bit field and has over 5 billion different addresses
- IPv6 was created to solve this depletion issue and has address sapce of 128 bits and 340 undecillion addresses

## Top Level Domains

- The last word in a domain name represents the "top level domain" e.g. .com or .gov
- The second word is known as a second level domain name (optional) e.g. the co in .co.uk

## Domain Registrars

- All names in given domain name must be unique
- Registrars is an authority that can assign domain names directly under one or more TLDs
- These domains are registered with InterNIC, a service of ICANN which enforces uniqueness of domain names accross the Internet
- Each domain name becomes registered in a central database known as the WhoIS database
- Popular domian registrars include Amazon or GoDaddy

## State of Authority Record (SOA)

- The name of the server that supplied that data for the zone
- The administrator of the zone
- The current version of the data file
- The default number of seconds for the TTL file on resource records

## NS stands for Name Server Records

- Used by TLD servers to direct traffic to the Content DNS server which contains the authoritative DNS records
- Eg. - user enters test.com -> browser goes to the TLD server for the authoritative DNS server -> the TLD has the name server record -> we then query the NS record which will give us the SOA and inside the SOA will have the DNS record

## A Record

- "A" stands for address. Used by computer to translate the name of the domain to an IP address

## TTL 

- Length that a DNS record is cached on either the Resolving Server of the user's own PC
- The lower the TTL, the faster the changes to DNS records take the propogate throughout the internet 
- Most providers the default TTL is 48 hours

##  CName

- Used to resolve one domain name to another. For example, you have a mobile website with a domain name such as mobile.xxx.com for when they browse on their mobile devices and you may want m.xxxx.com to resolve to the same address

## Alias Records

- Used to map resource record sets in your hosted zone to ELB, CloudFront distributions or S3 buckets that are configued as websites
- Alias records work like a CNAME record in that you can map one DNS to another target name
- A CNAME can't be used for naked domain names (zone apex record) - that is one name that has no www in front of it 

## Routing Policies Available

- Simple Routing
	- You can only have one record with multiple IP addresses
	- Sent back randomly to the user
	- User makes DNS request to Route53 and we have two IP addresses -> Route53 picks these in random orders

- Weighted Routing
	- User types in domain name to Route53 -> 20% of traffic is sent to US East 1 and then rest is sent to 80% of US West 1

- Latency-based Routing
	- Allows you to route your traffic based on lowest network latency for your end user (i.e which region will give you the fastest response time)
	- Create a latency resource record set for Amazon EC2 resource in each region that hosts your website. When R53 receives a query for your site, it selects the latency resource record set for the region that gives the user the lowest latency.  I then responds with the value associated with that resource record set

- Failover Routing
	- Used when you want to create an active/passive setup
	- E.g. primary site to be in EU-WEST-2 and your secondary DR site in AP-SOUTHEAST-2
	- Route53 will monitor the health of your primary site using a health check 
	- Health check monitors the health of your end points

- Geolocation Routing
	- Lets you choose where your traffic will be sent based on the geographic location of your users (i.e. the location form which DNS queries originate). For example, you might want all queries from Europe to be routed to a fleet of EC2 instances that are specifically configured for your European customers. These servers may have the local language of your European customers and all prices are displayed in Euros

- Geoproximity Routing (Traffic FLow Only) [Goes beyond scope of the exam]
	- Lets R53 route traffic to your resources based on the location of your users and your resources
	- You can optionally choose to route more traffic or less to a given resource by specifying a value, known as a bias 

- Multivalue Answer Routing
	- Lets you configure R53 to retur multiple values, such as IP addresses for your web servers, in response to DNS queries. You can specify multiple values for almost any record, but multivalue answer routing also lets you check the health of each resource, so R53 returns only values for healthy resources 

# Exam Tips

## Route53

- ELBs do not have pre-defined IPv4 address, you resolve to them using a DNS name
- Understand the difference between an Alias Record and a CNAME
- Given the choice, always choose an Alias Record over a CNAME

## Common DNS Types

- SOA
- NS
- A
- CNAMES
- MX
- PTR

## Domain names

- You can buy domain names directly with AWS
- It can take up to 3 days to register depending on the circumstances

## Simple Routing Policy

- Only one record with multiple IP addresses
- If you specify multiple values in a record, Route 53 returns all the values to the user in a random order

## Weighted Routing

- Sends to different regions around the world based on the weights that are given
- Adds all the weights in the record set and portions it off accordingly
- You can set health checks on individual record sets
- If record fails, it will be removed from Route 53 until it passes the health check
- You can set SNS notifications to alert you if a health check has failed

## Latency Routing

- Allows you to route your traffic based on lowest network latency for your end user (i.e which region will give you the fastest response time)
- Create a latency resource record set for Amazon EC2 resource in each region that hosts your website. When R53 receives a query for your site, it selects the latency resource record set for the region that gives the user the lowest latency.  I then responds with the value associated with that resource record set

## Failover Routing

- Used when you want to create an active/passive setup
- E.g. primary site to be in EU-WEST-2 and your secondary DR site in AP-SOUTHEAST-2
- Route53 will monitor the health of your primary site using a health check 
- Health check monitors the health of your end points

## Geolocation Routing

- Lets you choose where your traffic will be sent based on the geographic location of your users (i.e. the location form which DNS queries originate). For example, you might want all queries from Europe to be routed to a fleet of EC2 instances that are specifically configured for your European customers. These servers may have the local language of your European customers and all prices are displayed in Euros
- Routes traffic based on customer's location