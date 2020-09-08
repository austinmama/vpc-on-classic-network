---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-07-22"

keywords:

subcollection: vpc-on-classic-network

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Getting started with networking for VPC (Gen 1 compute)
{: #getting-started}
{: help} 
{: support}

As IBM continues to invest and innovate on the IBM Cloud Virtual Private Cloud (gen 2 compute) infrastructure, we're focusing on delivering maximum value in a single VPC Infrastructure platform. To support this effort, generation 1 compute infrastructure is being deprecated. The end of service date is 26 February 2021. For more information, see the [Start your migration](https://www.ibm.com/cloud/blog/announcements/start-your-vpc-gen1-to-vpc-gen2-migration){:external} blog.
{:deprecated}

To get started with networking for {{site.data.keyword.vpc_full}} (Gen 1 compute):

1. Create a Virtual Private Cloud.
2. Create one or more subnets in the Virtual Private Cloud in one or more zones.
3. Create a public gateway (PGW) on a subnet if you want resources on your subnet to have access to the internet or vice-versa.

Newer generation available. For more information, see [Getting started with Virtual Private Cloud](/docs/vpc?topic=vpc-getting-started) for generation 2 compute resources.
{:important}

## Before you begin

 * **User permissions**: Be sure that your user has sufficient permissions to create and manage resources in your VPC. For a list of required permissions, see [Granting permissions needed for VPC users](/docs/vpc-on-classic?topic=vpc-on-classic-managing-user-permissions-for-vpc-resources).

## Use the UI, CLI, or REST API to provision VPC Network Resources

The provisioning and managing of VPC network resources can be done through the UI, CLI or REST API.

* For access through the user interface, log into the [IBM Cloud Console](https://{DomainName}/vpc){: external}. Follow the steps in [Creating a VPC using the IBM Cloud console](/docs/vpc-on-classic?topic=vpc-on-classic-creating-a-vpc-using-the-ibm-cloud-console) if you need help.
* To use the command line interface, follow the [Hello World](/docs/vpc-on-classic?topic=vpc-on-classic-creating-a-vpc-using-the-ibm-cloud-cli) example.
* For more advanced users, you can call the [REST APIs](https://{DomainName}/apidocs/vpc-on-classic){: external} directly. Follow the [example code](/docs/vpc-on-classic?topic=vpc-on-classic-creating-a-vpc-using-the-rest-apis) tutorial to get started with the REST APIs.

## Next steps

After your Virtual Private Cloud networking has been provisioned, explore more.

* [Creating and managing virtual server instances](/docs/vpc-on-classic?topic=vpc-on-classic-creating-and-managing-virtual-server-instances)
* [Creating block storage volumes](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-creating-block-storage)
* [Using Security Groups](/docs/vpc-on-classic-network?topic=vpc-on-classic-network-setting-up-security-groups-using-the-cli)
* [Using Network ACLs](/docs/vpc-on-classic-network?topic=vpc-on-classic-network-setting-up-network-acls)
* [Using VPN](/docs/vpc-on-classic-network?topic=vpc-on-classic-network---using-vpn-with-your-vpc)
* [Using load balancers](/docs/vpc-on-classic-network?topic=vpc-on-classic-network---using-load-balancers-in-ibm-cloud-vpc)
