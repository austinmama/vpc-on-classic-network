---

copyright:
  years: 2018, 2020
lastupdated: "2020-04-02"

keywords: load balancer, public, listener, back-end, front-end, pool, round-robin, weighted, connections, methods, policies, APIs, access, ports, vpc, vpc network, layer-7

subcollection: vpc-on-classic-network

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}
{:external: target="_blank" .external}

# FAQs
{: #load-balancer-faqs}

This section contains answers to some frequently asked questions about the **Load Balancer for VPC** service.

## Can I use a different DNS name for my load balancer?
{: #can-i-use-a-different-dns-name-for-my-load-balancer}
{: faq}	   

The auto-assigned DNS name for the load balancer is not customizable. However, you can add a CNAME (Canonical Name) record that points your preferred DNS name to the auto-assigned load balancer DNS name. For example, your load balancer in `us-south` has ID `dd754295-e9e0-4c9d-bf6c-58fbc59e5727`, the auto-assigned load balancer DNS name is `dd754295-us-south.lb.appdomain.cloud`. Your preferred DNS name is `www.myapp.com`. You can add a CNAME record (through the DNS provider that you use to manage `myapp.com`) pointing `www.myapp.com` to the load balancer DNS name `dd754295-us-south.lb.appdomain.cloud`.

## What's the maximum number of front-end listeners I can define with my load balancer?
{: #what-s-the-maximum-number-of-front-end-listeners-i-can-define-with-my-load-balancer}
{: faq}	   

10 is the maximum number of front-end listeners that I can define with my load balancer.

## What's the maximum number of server instances I can attach to my back-end pool?
{: #what-s-the-maximum-number-of-server-instances-i-can-attach-to-my-back-end-pool}
{: faq}	   

50 is the maximum number of server instances that I can attach to my back-end pool.

## Is the load balancer horizontally scalable?
{: #is-the-load-balancer-horizontally-scalable}
{: faq}	   

Yes. The load balancer automatically adjusts its capacity based on the load. When horizontal scaling takes place, the number of IP addresses associated with the load balancer's DNS name changes.

## What should I do if I am using ACLs or security groups on the subnets that are used to deploy the load balancer?
{: #what-should-i-do-if-i-am-using-acls-or-security-groups-on-the-subnets-that-are-used-to-deploy-the-load-balancer}
{: faq}

You must ensure that the proper ACL or security group rules are in place to allow VPC instance creation and allow incoming traffic for configured listener ports and management ports. Traffic between the load balancer and back-end instances also should be allowed.

For detailed information on the ACLs configuration required, refer to [Configuring ACLs for use with load balancers](/docs/vpc-on-classic-network?topic=vpc-on-classic-network---using-load-balancers-in-ibm-cloud-vpc#configuring-acls-for-use-with-load-balancers).

## Why am I receiving an error message: `certificate instance not found`?
{: #why-am-i-receiving-an-error-message}
{: faq}


* The certificate instance CRN may be invalid.
* You may not have granted **service-to-service authorization**. See the **SSL offloading** section of this document.

## Why am I receiving a `401 Unauthorized Error` code?
{: #why-am-i-receiving-a-401}
{: faq}

Check the following access policies for your user:

* The access policy for the load balancer resource type
* The access policy for the resource group
* If `HTTPS` listeners are used, also check the service-to-service authorization for the Certificate Manager instance.

## Why is my load balancer in `maintenance_pending` state?
{: #why-is-my-lb-in-maintenance-pending-state}
{: faq}

The load balancer will be in `maintenance_pending` state during various maintenance activities, such as:

* Horizontal scaling activities
* Recovery activities
* Rolling upgrade to address vulnerabilities and apply security patches

## Why do I need to choose multiple subnets during provisioning?
{: #why-do-I-need-to-choose-multiple-subnets-during-provisioning}
{: faq}

**Load Balancer for VPC** is Multi-Zone-Region (MZR) ready. Load balancer appliances are deployed to the subnets you've selected. It is highly recommended to choose subnets from different zones, to provide you with higher availability and redundancy.

## Do I need additional IPs in the subnet for load balancer operations?
{: #do-I-need-additional-ips-in-subnet-for-load-balancer-operations}
{: faq}

Yes, additional IPs in the subnet are needed for horizontal scaling and maintenance operations.

## Why is back-end member health under my pool `unknown
{: #why-is-back-end-member-health-under-my-pool-unknown}
{: faq}

* The pool is not associated with any listeners
* Configuration changes might have been made to the pool or its associated listener

## Why is back-end member health under my pool `faulted` ?
{: #back-end-member-health-failing}
{: faq}

Verify the following configurations:

* Does the port of the configured back-end protocol match the port the application is listening on?
* Does the configured health-check have the correct protocol (TCP or HTTP), port, and URL (for HTTP) information? For HTTP, ensure your application responds with 200 OK for the configured health check URL.
* Is security group configured on the back-end server instance? If so, ensure that the security group rules allow traffic between the load balancer and the virtual server.

For more information, see the [Health checks](#health-checks) section.

## Which TLS version is supported with SSL offload?
{: #which-tls-version-is-supported-with-ssl-offload}
{: faq}	   

The **Load Balancer for VPC** supports TLS 1.2 with SSL termination.

The following list details the supported ciphers (listed in order of precedence):												 

* ECDHE-RSA-AES256-GCM-SHA384
* ECDHE-RSA-AES256-SHA384
* AES256-GCM-SHA384
* AES256-SHA256
* ECDHE-RSA-AES128-GCM-SHA256
* ECDHE-RSA-AES128-SHA256
* AES128-GCM-SHA256
* AES128-SHA256

## What are the default settings and allowed values for health check parameters?
{: #what-are-the-default-settings-and-allowed-values-for-health-check-parameters}
{: faq}

The default settings and allowed values are listed:									   

* Health check interval: Default is 5 seconds, range is 2 to 60 seconds.
* Health check response timeout: Default is 2 seconds, range is 1 to 59 seconds.
* Maximum retry attempts: Default is 2 retry attempts, and the range is 1 to 10 retries.

The health check response timeout value must always be less than the health check interval value.
{:note}

## Are the load balancer IP addresses fixed?
{: #are-the-load-balancer-ip-addresses-fixed}
{: faq}

Load balancer IP addresses are not guaranteed to be fixed. During system maintenance or horizontal scaling, you can see changes in the available IPs associated with the FQDN of your load balancer.

Use FQDN, rather than cached IP addresses.
{:note}

## Does the load balancer support Layer-7 switching?
{: #does-the-load-balancer-support-layer-7-switching}
{: faq}

Yes, the load balancer supports Layer-7 switching.

## Why does HTTPS listener creation or update tell me that my certificate is invalid?
{: #why-does-https-listener-creation-or-update-tell-me-that-my-certificate-is-invalid}
{: faq}

Check for these possibilities:

* The provided certificate CRN might be invalid.
* The certificate instance given in the Certificate Manager might not have an associated private key.
