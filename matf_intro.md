<a name="top"></a>

# Introduction to MATF – Mutually Authenticating TLS in the Context of Federations
As system-to-system communication between organisations is increasingly realised through APIs and backend integrations, 
establishing trust between systems becomes critical. A widely adopted approach to system authentication and trust establishment 
relies on the exchange of cryptographic material and the use of mutual TLS (mTLS), where both client and server authenticate 
each other.

While mTLS provides strong cryptographic authentication of communicating parties, it does not by itself answer a fundamental question: 
> Which systems should actually be trusted and allowed to connect?

A valid certificate proves possession of a key, but not necessarily that the system represents an authorised or governed organisation within a given context.

Consequently, it is not sufficient for a system to present a technically valid certificate. The organisation behind that system must be 
identifiable, explicitly approved, and subject to governance and follow-up in a controlled manner.

MATF addresses this challenge in environments where multiple independent organisations operate under shared trust rules. 
Such an environment is referred to here as a *federation*. Within a federation, there is an agreed set of participants and 
a structured description of their systems.

MATF connects this federated trust framework directly to API and backend traffic. Each connection is bound to a named federation member, 
and the counterpart is verified as an approved participant—not merely as a system presenting a valid certificate.

## What is MATF?
Mutually Authenticating TLS in the context of Federations (MATF) is a mechanism for combining cryptographic authentication with federated 
trust management in system-to-system communication between organisations.

It is designed for environments where multiple independent actors interact via APIs and backend systems. In such settings, it must be possible to 
determine which servers and clients belong to which organisations — and which of them are actually authorised to participate in a given trust context.

MATF builds on standard TLS with mutual authentication (mTLS). The TLS protocol itself is not modified. Instead, MATF introduces a federated layer that enables:

- The aggregation of information about members’ servers and clients into a shared metadata document.
- The binding of each server and client to one or more public keys used for authentication.
- The publication and cryptographic signing of this metadata by a federation operator, allowing all participants to trust its integrity and origin.

This allows systems to discover and verify counterparts based on a common, authoritative source—rather than requiring each organisation to 
build and maintain its own trust configuration.

## What are the benefits of MATF?
MATF provides three key outcomes: automation, predictability, and control.

- Federation metadata provides a shared and consistent view of participating organisations and the keys associated with their systems.
- Systems can verify counterparts using the same authoritative source of trust information, eliminating the need for local allow-lists or environment-specific configurations.
- When a connection is established, both client and server can validate each other’s keys against federation metadata before allowing traffic. This significantly reduces the risk of impersonation—even by actors presenting technically valid certificates.

MATF is a federated mechanism for how keys and connections are described, distributed, and verified in distributed environments where independent actors communicate directly. 
This makes it particularly valuable in environments requiring scalable and trustworthy digital collaboration.

## A step toward automated trust
With MATF, trusted organisations and their associated keys are defined in signed federation metadata rather than distributed across local configurations. 
Trust becomes part of the shared infrastructure, rather than something managed ad hoc within individual systems.

This simplifies the onboarding of new members, key rotation, and access governance. Organisations can collaborate more efficiently and securely, with reduced 
reliance on manual certificate exceptions and troubleshooting of trust chains.

<p>&nbsp;</p>

----

:arrow_backward: [Hem](README.md) &nbsp; &nbsp; | &nbsp; &nbsp; :arrow_up_small: [Tillbaka till toppen](#top)  
