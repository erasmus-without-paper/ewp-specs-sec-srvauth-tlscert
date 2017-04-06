Authenticating Servers with TLS Certificate
===========================================

This document describes how EWP server authentication can be accomplished with
the use of TLS Server Certificates, CAs, and the Registry.

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Introduction
------------

This is a pretty standard method of server authentication. It requires TLS
(HTTPS) to be used. The server's certificate MUST be signed by publicly trusted
CA.


Implementing a server
---------------------

You MUST acquire a CA-signed certificate for your domain(s), and install it on
your servers. These are just the "regular" domain-validated certificates.

Note, that your APIs can be spread across multiple domains. The number of
domains used to implement EWP does not matter, but all of them need to be
protected by proper certificates issued for these domains.


Implementing a client
---------------------

You MUST make sure that your HTTPS request-making library properly validates
server certificates. You MUST make sure that your trusted certificates come
from a safe source. If you cannot be 100% sure about these requirements, then
you SHOULD NOT use this method of server authentication.

Not much more to describe here. You just make the regular HTTPS request, with
all the standard methods of validation.


Security considerations
-----------------------

### Main security questions

The [Authentication and Security][sec-intro] document
[recommends][sec-method-rules] that each server authentication method
specification explicitly answers the following questions:

> How can the client verify the server's identity?

The client uses regular HTTPS server certificate validation to make sure that
it is communicating with the proper domain and URL.

This only works if the client configures his TLS properly (in particular, when
his certificate storage is safe).

> How can the client verify that the response has not been tampered with? Can
> it also verify that it was indeed generated for this particular request?

TLS prevents communication to be tampered with during the transport. The client
also **trusts** that the internal network of the server is safe - it trusts
that the server implementers wouldn't allow this method of authentication if it
*wasn't* safe.

> Does it provide non-repudiation? Can a client provide a solid proof later
> on, that the server sent a particular response (in response to a particular
> client's request)?

No. In theory, recording entire TLS session can provide this proof, but this is
hard to achieve. TLS has not been designed for non-repudiation.


[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management/blob/stable-v1/README.md#statuses
[sec-intro]: https://github.com/erasmus-without-paper/ewp-specs-sec-intro
[sec-method-rules]: https://github.com/erasmus-without-paper/ewp-specs-sec-intro#rules
