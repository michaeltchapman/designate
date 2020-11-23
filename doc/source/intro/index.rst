..
      Copyright 2020 OpenStack Foundation
      All Rights Reserved.

      Licensed under the Apache License, Version 2.0 (the "License"); you may
      not use this file except in compliance with the License. You may obtain
      a copy of the License at

          http://www.apache.org/licenses/LICENSE-2.0

      Unless required by applicable law or agreed to in writing, software
      distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
      WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
      License for the specific language governing permissions and limitations
      under the License.

.. _introduction:

What is DNS?
=============================

The Domain Name System (DNS) is a system for naming resources connected to a network, and works by
storing various types of *record*, such as an IP adress associated with a domain name.
In practice, this is implemented by *authoritative name servers* which contain these records and *resolvers* which query
name servers for records. Names are divided up into a hierarchy of zones, allowing different name servers to
be responsible for separate groups of zones by delegating responsibility using records.

The root zone, which is simply ".", is comprised entirely of records delegating various top level domains (TLDs)
to other nameservers. The TLD name servers will the contain records for domains within their TLD, such as
the *.com* nameserver having an *example.com* record, as well as records that delegate domains to other
nameservers, for example *openstack.org* might have their own nameserver so that they can then create
*cloud.openstack.org*.

TODO Diagram showing nameservers

*Resolvers* are often formed in two parts: a *stub* resolver which is often merely a library on a 
user's computer, and a *recursive resolver* that will perform queries against nameservers before returning
the result to the user. When searching for a domain, the resolver will start at the end of the domain and
work its way back to the beginning. For example when searching for cloud.openstack.org, it will start
with the root nameserver ".", which will reply with the location of the ".org" nameserver. The resolver
can then contact the ".org" nameserver to get the "openstack.org" nameserver and from there finally get
the "cloud.openstack.org" record and return it to the user. In order to make this more efficient, the results
are cached on the resolver, so after the first user has requested "cloud.openstack.org", the resolver can
return the cached result for subsequent requests. 

TODO Diagram showing resolvers querying nameservers

TODO external links / further reading
  - https://en.wikipedia.org/wiki/Domain_Name_System 
  - https://www.cloudflare.com/learning/dns/what-is-dns/ perhaps?

Introducing Designate
=============================

Designate is an Openstack service allows users and operators to manage DNS records, names and zones via a
REST API and can configure existing DNS name servers to contain those records. Designate can also be configured by an operator
to integrate with both the Openstack Network Service (Neutron) and the Compute Service (Nova) so that records
are automatically created when floating IPs and compute instances are created respectively, and uses the Openstack
Identity Service (Keystone) for user management. Since there are a multitude of software implementations of
the DNS name server, Designate has a pluggable backend that can be configured to manage many of them, most
notably Bind9 and PowerDNS. 

TODO DNS Diagram with Designate to the side showing which parts it interacts with

Designate Architecture
=============================

TODO Describe the components within designate

TODO Pull in diagram from dev section or otherwise expand diagram

Using Designate
=============================

TODO
 - HTTP API
 - Openstack client
 - Horizon

TODO Things users can do + link to API reference
