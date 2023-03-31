---
title: "Multipath QUIC Path Failover Mechanism"
abbrev: "QUIC failover"
category: info

docname: draft-kozuka-quic-failover-latest
submissiontype: IETF  # also: "independent", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Transport"
workgroup: "QUIC"
keyword:
 - QUIC
 - failover
 - multipath
venue:
  group: "QUIC"
  type: "Working Group"
  mail: "quic@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/quic/"
  github: "masa-koz/quic-failover"
  latest: "https://masa-koz.github.io/quic-failover/draft-kozuka-quic-failover.html"

author:
 -
    fullname: Masahiro Kozuka
    organization: Okayama University
    email: "masa.koz@kozuka.jp"

normative:

informative:


--- abstract

The proposed path failover mechanism provides a seamless way to recover from path failures in Multipath QUIC. It allows the protocol to take advantage of multiple paths while maintaining reliability and security. The implementation and deployment of this mechanism should be done with careful consideration of security and performance.

--- middle

# Introduction

Multipath QUIC provides improved network performance and reliability by using multiple network paths concurrently. However, if one of the paths fails, it can cause a disruption in the communication. This document proposes a path failover mechanism for Multipath QUIC, which allows it to recover from path failures seamlessly.


# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Path Failover Mechanism
Multipath QUIC uses multiple paths to transfer data concurrently. Each path has its own metrics, such as RTT, available bandwidth, and congestion level. These metrics are monitored by the sender using the Path Quality Estimation (PQE) framework. When a path failure is detected, the sender chooses a new path to transfer data.
The sender detects a path failure when the path metrics show a significant degradation. This can be caused by a network outage or congestion. If the path metrics remain degraded for a certain duration, the sender assumes the path has failed and triggers the failover mechanism.
When the failover mechanism is triggered, the sender selects a new path to transfer data from a list of available paths. The selection criteria can be based on various factors, such as available bandwidth, RTT, and congestion level. The sender also considers the path diversity to choose a path that is different from the failed path.
After selecting a new path, the sender checks whether it is valid by sending a connectivity check packet. If the path is valid, it starts sending data on the new path. If the new path also fails, the sender repeats the failover mechanism with a different path.

# Security Considerations

The failover mechanism should not compromise the security of the communication. The selection of a new path should not leak information about the failed path or the communication itself. Therefore, the selection criteria should not depend on any information that can be obtained by an eavesdropper.
The connectivity check packet should be authenticated to prevent spoofing attacks. The sender should verify the authenticity of the packet before deciding to use the new path. The sender should also limit the number of failover attempts to prevent denial-of-service attacks.
The failover mechanism should not introduce any new vulnerabilities to the Multipath QUIC protocol. Therefore, it should be thoroughly tested and reviewed before being deployed.

# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
