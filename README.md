# Proposal for future work of Yeti DNS Project (draft) 

Yeti DNS Project was launched in 2015 with a goal to build an experimental, non-production root server testbed that provides an environment where technical and operational experiments can safely be performed without risk to production root server infrastructure. Thanks to the persistent effort of Yeti participants, activities in Yeti DNS Project during the past 3 years reached its initial goal and provided the community with experience and better understanding on the capability and limits of Yeti Root system. The framework of Yeti testbed, experiments performed and operational experiences are well documented in RFC8483. Along with that, interesting areas for future work on Root system are also indentified in RFC8483 which severs as bases for new Charter of Yeti DNS Project.

There are some working items for future work collected from Yeti sponsors and participants: 

## Issues on DNS large response in IPv6

In previous work in Yeti, IPv6 large packet issue still exists and has impact on Yeti root in many aspects [section5.1.1 of RFC8483](https://tools.ietf.org/html/rfc8483#section-5.1.1). KSK rollover produces large response with additional KSKs. large number of root servers will generate large response during priming process. Moreover, Multi-DM structure also requires stable transmission of large DNS response in IPv6. 

Genearally there two approaches for this issue :
* Fall back later or sooner to TCP on either server side or client side. For resolver it is to set EDNS0 bufsize below a certain number
Server. For authoritative servers it is to set their maximum UDP response size small enough.
* Reduce the size of DNS response by using ECC (even try CSK-Combined Signing Key) for DNSSEC 

## Data resiliency and security of Root

Yeti DNS as a system model has shown the capacity of independence of the root system against surveillance risk and external Dependency.  However, some concerns may be still there on the security and resiliency of data in case of ICANN failure. Some people want to be sure that their data was independent of ICANN and/or the other. They also would like to have better data resiliency against some failures. There’s substantial technical work to be done to make this public accessible, scalable and automatic, for example improving the update process.

More generally, it is known that DNS is a tree based hierarchical database. Mathematically It has a root node and links between parent-child nodes, referred as to a typical DAG(Directed Acyclic Graph). So any failures and instability of parent nodes will impacts all their child nodes in case of human mistake, malicious attack or even earthquake. The risk of parent-child dependence is inherent in the nature of DNS. It has been  proposed to redefine Yeti as seeking to define technology and practices to allow any organization, from the smallest  company to nations to be self-sufficient in their DNS

There are some related works on this field for reference. For example, DLV (RFC4431) is one example to weaken the parent-child dependency in DNSSEC use case. RFC7706 provide a way to install a local root to reduce the dependency of Root sever system. And draft-ietf-dnsop-serve-stale enables recursive resolvers to use stale DNS data to avoid outages when authoritative nameservers cannot be reached to refresh expired data.

## Fault-tolerant Distributed Root (Distributed DNSSEC)

In RFC8483 it is proposed that it would be interesting to test some technical tools like blockchain to either remove the technical requirement for a central authority over the root or enhance the security and stability of the existing Root.

Return to the practice of Yeti Multi-DM, it received expected benefit due to its property of redundancy. However, root operation based on Multi-DM model exposed some issues as well. In a [Yeti blog post](http://yeti-dns.org/yeti/blog/2018/08/13/fault-tolerant-distribution-master-architecture.html), Yeti’s Multi-DM Architecture was revisited. It is inferred that a fault-tolerant property is desired for future Root architecture. Most specifically, a consensus should be achieved before any signed zone be published among a group of entities. It is proposed that a Fault-tolerant Distribution Master Architecture (FDMA) or Distributed Root (DR) is worth of doing as an important direction in Yeti’s future research agenda.

##  Yeti DNS software as a deliverable

Besides the interesting research items with deliverables like technical report, presentations, IETF document, it is desired that Yeti DNS Project can finally deliver some useful tools and open source DNS software which implement new functions deployed and tested in Yeti testbed. 

It is suggested new functions or protocol proposed in Yeti project should be firstly put in a IETF draft format. Peer reviews and Comments from technical community are important. When it is ready with enough consensus in Yeti community, resource is to be collected and put on the implemenation and experiment.

