# Future work for Yeti DNS Project (draft) 

Yeti DNS Project was launched in 2015 with a goal to build an experimental, non-production root server testbed that provides an environment where technical and operational experiments can safely be performed without risk to production root server infrastructure. Thanks to the persistent effort of Yeti participants, activites in Yeti DNS Project during the past 3 years reached its goal and provided the community with expereince and better understanding on the capablity and limits of Yeti Root system. The framework of Yeti testbed, experiments performed and operational experiences are well documented in RFC8483. Along with that, intereting areas for future work on Root system are also indentified in RFC8483 which severs as bases for new Charter of Yeti DNS Project.

There are some proposals for future work collected from Yeti sponors and participants: 

## Issues on DNS large response in IPv6

In previous work in Yeti, IPv6 large packet issue still exists and has impact on Yeti root in many aspects [section5.1.1 of RFC8483](https://tools.ietf.org/html/rfc8483#section-5.1.1). KSK rollover produces large response with additional KSKs. large number of root servers will generate large response during priming process. Moreover, Multi-DM structure also put requirement for stable transmition of large DNS response in IPv6. One promission apporach to resolve this issue is to enable resolver and root server use connection-oriented transport potocol like TCP or HTTP for DNS transaction which generates large DNS response. 

There are two approaches:
* DNS Transport over TCP [RFC7766] is a Mandatory for Yeti resolver. All Root server adopt [ATR](https://tools.ietf.org/html/draft-song-atr-large-resp-01) to generate a small truncated response in case of fragement dropped in the middle of the path.
* Enable resolver send DNS queries over TCP or HTTP to allow large DNS response with any difficulty. There is one expired draft mentioned this idea: [song-dnsop-tcp-primingexchange](https://tools.ietf.org/html/draft-song-dnsop-tcp-primingexchange-00) 

With the property of supporting large DNS response, some limits of Root system can be relaxed. One notable exmaple is that the number of root server can be extended as many as the number of regions and countries.   

## Automatic Software Updates for DNS

One aspect of Yeti experiments shows that it is difficult to trace the status of existing deployed DNS. It is also difficult to update the software to adopt new DNS functions and adapt to new configuration (renubmering of hint). For example, people find it is hard to estimate the readiness of RFC5011 and roll the KSK with more confidence. It is a real notable issue in IoT era, because large scale of IoT sub-resolvers are out of maiantance in very near future.

Inspired by IETF working group of Software Updates for Internet of Things (suit), it is intereting to explore and develop some techniques and solutions to allow DNS (expecially DNS resolver) update itself automatically. The Self-updating resolver is able to send status periodically to a centrolized entity (its implementor for exmaple), check the latest version, download the latest patch, configure and build the code with the patch automatically without breaking the servcies. Surely it can be enlabed and disabled by local configuration. 

With that Self-updating property, it is expecyed that many issues around DNS software updating and rollover will be resolved,expecially in Root system level. 

## Data security of Root 

Yeti DNS as a system model has shown the capacity of independence of the root system against surveillance risk and external Dependency.  However, some concerns may be still there on the security and stability of data in case of ICANN failure. Some people want to be sure that their data was independent of ICANN and/or the other. Maybe RFC7706 is one example to start with. There’s substantial technical work to be done to make this public accessible, scalable and automatic, for example improving the update process.

More generally, it is known that DNS is a tree based hierarchical database. Mathematically It has a root node and links between parent-child nodes, referred as to a typical DAG(Directed Acyclic Graph). So any failures and instability of parent nodes will impacts all their child nodes in case of human mistake, malicious attack or even earthquake. The risk of parent-child dependence is inherent in the nature of DNS. DLV (RFC4431) is one example to weaken the parent-child dependency in DNSSEC use case. But maybe more general case should be consider as well. 

It has been  proposed to redefine Yeti as seeking to define technology and practices to allow any organization, from the smallest  company to nations to be self-sufficient in their DNS

## Fault-tolerant Distribution Master Achitecture

In RFC8483 it is proposed that in future work, it would be interesting to test some technical tools like blockchain to either remove the technical requirement for a central authority over the root or enhance the security and stability of the existing Root.

Return to the previous practice of Yeti Multi-DM, it received expected benefit due to its property of redundancy. However, root operation based on Multi-DM model exposed some issues as well. In a [Yeti blog post](http://yeti-dns.org/yeti/blog/2018/08/13/fault-tolerant-distribution-master-architecture.html), Yeti’s Multi-DM Architecture was revisited. It is inferred that a fault-tolerant property is desired for future Yeti DM architecture. Most specifically, a consensus should be achieved before any signed zone be published among a group of entities. The post introduces the requirement and provide some primitives function of new Yeti DM architecuture. It is proposed in conclusion that a Fault-tolerant Distribtion Master Architecuture (FDMA) is worth of doing as an experiment and important property in Yeti’s future agenda.

##  Yeti DNS software as a deliverable

Besides the intereting research items with deliverables like technical report, presentations, IETF document, it is desired that Yeti DNS Project can finally deliver some useful tools and open source DNS softwares which implement new functions deployed and tested in Yeti testbed. 

