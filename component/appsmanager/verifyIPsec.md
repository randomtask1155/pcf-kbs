---
title: How to verify that IPsec works with PCF
template: how-to
id: 
locale: en-us
---

# How to verify that IPsec works with PCF

**Environment**

Pivotal Cloud Foundry 

**Purpose**

This topic provides instructions to verify that strongSwan-based IPsec works with your Pivotal Cloud Foundry (PCF) deployment and general recommendations for troubleshooting IPsec
Users are having excessive loss of memory.

**Resolution**

To verify that IPsec works between two hosts, you can check that traffic is encrypted in the deployment with ``tcpdump``, perform the ping test, and check the logs with the steps below.

1. Check traffic encryption and perform the ping test. Select two hosts in your deployment with IPsec enabled and note their IP addresses. These are referenced below as ``IP-ADDRESS-1`` and ``IP-ADDRESS-2``.
    1. SSH into IP-ADDRESS-1
``$ ssh IP-ADDRESS-1``
    2. On the first host, run the following, and allow it to continue running.
``$ tcpdump host IP-ADDRESS-2``
    3. From a separate command line, run the following:
``$ ssh IP-ADDRESS-2``
    4. On the second host, run the following:
``$ ping IP-ADDRESS-1``
    5. Verify that the packet type is ESP. If the traffic shows ``ESP`` as the packet type, traffic is successfully encrypted. The output from ``tcpdump`` will look similar to the following:
``03:01:15.242731 IP IP-ADDRESS-2 > IP-ADDRESS-1: ESP(spi=0xcfdbb261,seq=0x3), length 100``
2. Open the ``/var/log/daemon.log`` file to obtain a detailed report, including information pertaining to the type of certificates you are using, and to verify that there is an established connection.
3. Navigate to your Installation Dashboard, and click Recent Install Logs to view information regarding your most recent deployment. Search for “ipsec” and the status of the IPsec job.
4. Run ```ipsec statusall``` to return a detailed status report regarding your connections. The typical path for this binary: ``/var/vcap/packages/strongswan-x.x.x/sbin``. ``x.x.x`` represents the version of strongSwan packaged into the IPsec.
If you experience symptoms that IPsec does not establish a secure connection, return to the Installing IPsec topic and review your installation.
