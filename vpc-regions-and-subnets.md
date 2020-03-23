---

copyright:
  years: 2018, 2020
lastupdated: "2020-02-28"

keywords: vpc, address prefix, region, subnet, zone, reserved, IP, ranges, deleting, creating, CIDR, vpc network

subcollection: vpc-on-classic-network

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}
{:external: target="_blank" .external}

# Understanding IP address ranges, address prefixes, regions, and subnets
{: #working-with-ip-address-ranges-address-prefixes-regions-and-subnets}
[comment]: # (linked help topic)

This document discusses the relationships among regions, address prefixes, and subnets for {{site.data.keyword.vpc_full}}:

* A VPC is deployed and bound to a region.
* Within that one region, a VPC can span multiple zones.
* Address prefixes enable communication between the zones a VPC spans. Each VPC gets a short-cut default address prefix for each zone it spans.
* Subnets are created within the scope of an address prefix, meaning that a subnet must be contained completely within a single, existing address prefix.
* If you use an IP range outside of those ranges defined by [RFC 1918](https://tools.ietf.org/html/rfc1918){: external} (`10.0.0.0/8`, `172.16.0.0/12`, or `192.168.0.0/16`) for a subnet, the instances attached to that subnet may be unable to reach parts of the public Internet.

## IBM Cloud VPC and regions
{: #ibm-cloud-vpc-and-regions}

A VPC is deployed in a region, but it may span multiple zones. Each region contains multiple zones, which represent independent fault domains.

## IBM Cloud VPC and address prefixes
{: #ibm-cloud-vpc-and-address-prefixes}

Address prefixes enable communication between VPC instances in different zones. They provide routing information, which the _implicit router_ needs, for sending data to the zone in which the destination instance is located. Each subnet must be contained by an address prefix. {{site.data.keyword.vpc_short}} does not support the concept of "local" or "unreachable" subnets.

The _implicit router_ is the inherent network connectivity between all subnets created within a VPC.
{: note}

Each VPC can have up to five address prefixes for each zone. To help you get started, {{site.data.keyword.vpc_short}} defines a default address prefix for each zone (see the table that follows), however, as a best practice, you should [design a VPC addressing plan](/docs/vpc-on-classic-network?topic=vpc-on-classic-network-vpc-addressing-plan-design) before deploying one.

### VPC default address prefixes
{: #default-vpc-address-prefixes}

When a new VPC is created, the default address prefixes are assigned as follows, based on the region and zone.

[Classic Access
VPCs](/docs/vpc-on-classic?topic=vpc-on-classic-setting-up-access-to-your-classic-infrastructure-from-vpc#classic-access-default-address-prefixes) have a different set of default address prefixes.
{: important}

Zone         | Address Prefix
---------------|---------------
`us-south-1`   | `10.240.0.0/18`
`us-south-2`   | `10.240.64.0/18`
`us-south-3`   | `10.240.128.0/18`
`us-east-1`   | `10.241.0.0/18`
`us-east-2`   | `10.241.64.0/18`
`us-east-3`   | `10.241.128.0/18`
`eu-gb-1`      | `10.242.0.0/18`
`eu-gb-2`      | `10.242.64.0/18`
`eu-gb-3`      | `10.242.128.0/18`
`eu-de-1`      | `10.243.0.0/18`
`eu-de-2`      | `10.243.64.0/18`
`eu-de-3`      | `10.243.128.0/18`
`jp-tok-1`     | `10.244.0.0/18`
`jp-tok-2`     | `10.244.64.0/18`
`jp-tok-3`     | `10.244.128.0/18`
`au-syd-1`     | `10.245.0.0/18`
`au-syd-2`     | `10.245.64.0/18`
`au-syd-3`     | `10.245.128.0/18`

Different default prefixes will be assigned to new zones as they become available.

Starting with API version `2019-08-27`, a VPC can be created without a default address prefix using the [API](https://{DomainName}/apidocs/vpc-on-classic#create-a-vpc){: external} by specifying the option `address_prefix_management=manual` in the request.
{: note}

### Address prefixes and the IBM Cloud console UI
{: #address-prefixes-and-the-ibm-cloud-console-ui}

When you create a VPC using the IBM Cloud Console UI, the system selects your address prefix automatically and requires you to create a subnet within that default prefix. If this address scheme does not suit your requirements, you can customize the address prefixes after you create the VPC. You can then create subnets in your customized address prefixes, and delete the subnet you created with the default prefix.

This workaround is needed to use BYOIP through the IBM Cloud Console UI.
{:note}

<!-- TODO: Replace with this when UI is ready:
When you create a VPC using the IBM Cloud Console UI, the system gives you the option to select your address prefix automatically and create a subnet within that default prefix or delay creating address prefixes so you can create the specific prefixes that meet your requirements.
-->

## IBM Cloud VPC and subnets
{: #ibm-cloud-vpc-and-subnets}

You can divide a VPC into subnets. All the subnets in a VPC can reach one another through private L3 routing by an implicit router. You do not need to set up any routers or routes.

Handy facts about subnets in VPC:

* A subnet consists of an IP address range that you specify.
* A subnet is bound to a single zone, it cannot span multiple zones or regions.
* A subnet can span the entirety of the zone in a VPC.
* You must create your VPC before you create your subnet(s) within that VPC.
* IPv6 support is not available.
* You can associate or disassociate a Virtual Server Instance (VSI) to a subnet by adding a vNIC to the instance.
* Each subnet must be contained within an address prefix that belongs to the zone in which that subnet is bound.

You can bring your own public IPv4 address range (BYOIP) to your {{site.data.keyword.vpc_short}}. When you use BYOIP, {{site.data.keyword.cloud_notm}} must configure those IPv4 addresses on {{site.data.keyword.cloud_notm}} resources, which will send packets to and from the provided addresses. Therefore, as a result of using your supplied IPv4 range on {{site.data.keyword.cloud_notm}}, these IP addresses may be exposed to IBM's support staff and third parties as part of your use of this service.
{:important}

![IBM Cloud VPC Overview](images/vpc-experience.svg "IBM Cloud VPC Overview"){: caption="Figure: A graphical representation of a VPC showing zones, regions, and subnets." caption-side="top"}

### Using address prefixes for subnets
{: #using-address-prefixes-for-subnets}

Each subnet must exist within an address prefix.
 * For your new subnet, you can pick your range of IP addresses from the existing address prefixes.
 * If the zone's address prefixes are not suitable, one of the existing address prefixes can be edited, or a new address prefix can be added for the zone (using the API, CLI, or UI).

### Available IP addresses
{: #available-ip-addresses}

These are available IP addresses, as defined in **RFC 1918**:

 * 10.0.0.0 – 10.255.255.255
 * 172.16.0.0 – 172.31.255.255
 * 192.168.0.0 – 192.168.255.255

If you use an IP range that is outside of the allowable ranges for a subnet (given in previous sections), the instances attached to that subnet may be unable to reach parts of the public Internet.

### More about creating a subnet
{: #more-about-creating-a-subnet}

You can specify a subnet for your VPC in two ways:
  * You can create a subnet by providing the size of subnet you need, such as the number of addresses supported (for example, 1024).
  * You can create a subnet by providing a CIDR block (such as 10.0.0.8/29).

As an example of how to specify a 1024 block using CIDR, if you're specifying a CIDR block rather than a subnet size, the IPv4 block `192.168.100.0/22` represents the 1024 IPv4 addresses from `192.168.100.0` to `192.168.103.255`.
{:tip}
