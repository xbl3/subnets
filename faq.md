---

copyright:
  years: 1994, 2017-2019
lastupdated: "2019-02-28"

keywords: Primary IP, IP address, subnet's IP

subcollection: subnets

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}
{:faq: data-hd-content-type='faq'}

# FAQ
{:#subnets-faq}

## What does `Primary IP for future server only` when I look at a subnet's IP addresses mean?
{:#subnets-faq-primary-ip-future-server-only}
{: faq}

Primary Subnets are assigned and removed as needed by {{site.data.keyword.BluSoftlayer_notm}} for other resources you've ordered, such as Bare Metal Servers or Virtual Server Instances. We don't simply assign one IP address at a time, we assign a subnet. This means there is sometimes additional room for future resources. This designation is stating that these addresses will be used by future resources. Please see the question, "**Can I use the other IP addresses defined by the Primary Subnets I see?**" for why you should not consider these IP addresses as usable.


## Can I use the other IP addresses defined by the Primary Subnets I see?
{:#subnets-faq-use-other-ip-addresses-primary-subnets}
{: faq}

No! We realize you see the Primary Subnets assigned by {{site.data.keyword.BluSoftlayer_notm}} as any other subnet, but as described in [About Subnets](/docs/infrastructure/subnets?topic=subnets-about-subnets-and-ips), Primary Subnets are what provide IP addresses to resources on demand. We assign and remove Primary Subnets as we require to fulfill other products. If you attempt to use unassigned IP addresses from
Primary Subnets, we will inevitably assign them to another resource at some point. This leads to IP conflicts on the network and general service disruption. We reserve the right to block or otherwise make unusable any IP address on a Primary Subnet which is not specifically assigned during fulfillment of other products. You should use **Secondary Subnets** for all additional IP address needs, and we strongly encourage you to use them for your application/service address needs. Secondary Subnets are much more flexible and are maintained on your account for as long as you own them.


## Is there a way to specify which subnet I want to use for my device when I order it?
{:#subnets-faq-specify-which-subnet-on-order}
{: faq}

Yes, a specific subnet may be specified during the ordering process. When ordering a device, this option is available at the end of the order form. After selection of a private VLAN, a list of Primary Subnets routed to that VLAN is presented. You may select a desired subnet. The same process can be repeated for the public VLAN and subnet.

It is important to note that submission of the order **does not guarantee** that an IP address is available in the requested subnet. If no addresses are available, you will be contacted in order to determine a coarse of action. For the best {{site.data.keyword.BluSoftlayer_notm}} experience, selection of a subnet is discouraged for typical uses.


## I ran out of IP addresses, now what?
{:#subnets-faq-ran-out-of-addresses}
{: faq}

This won't happen! We automatically assign Primary Subnets to make more IP addresses available to fulfill your compute purchases. You don't need to manage a thing. However, if you mean that you need more IP addresses for say local virtual machines or segregating applications, then read up on **Secondary Subnets** in [About Subnets](/docs/infrastructure/subnets?topic=subnets-about-subnets-and-ips).


## How do I assign more IP addresses to a compute resource?
{:#subnets-faq-assign-more-ip-addresses-to-compute-resource}
{: faq}

First, you'll want to purchase a **Secondary Subnet**, there are multiple types, so review [About Subnets](/docs/infrastructure/subnets?topic=subnets-about-subnets-and-ips). Once you have a subnet routed to the IP address or VLAN desired, you'll want to refer to the specific compute documentation for how to setup your new IP addresses:

  * [Bare Metal Server IP address assignment](/docs/bare-metal?topic=bare-metal-assigning-server-ip-addresses)
  * [Virtual Server Instance IP address assignment](/docs/vsi?topic=virtual-servers-assigning-server-ip-addresses)


## What does `Reserved for HSRP` when I look at a subnet's IP addresses mean?
{:#subnets-faq-reserved-hsrp-meaning}
{: faq}

In a decreasing number of locations, {{site.data.keyword.BluSoftlayer_notm}} has routers utilizing a technique known as Hot Router Standby Protocol or HSRP. Specifically, the way it is used impacts the IP addresses available to ***Portable Secondary Subnets***; meaning you will lose access to two additional addresses in these locations. As the designation, "Reserved for HSRP", indicates, these IP addresses are reserved to fulfill the needs of HSRP. You may even have subnets on the same router, some with and some without, such reservations. As with any IP conflict, please do not attempt to use these
addresses or you risk affecting traffic on the entire subnet.
