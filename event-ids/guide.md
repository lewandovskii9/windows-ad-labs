🔍 Event ID Analysis Guide (Active Directory Security)

_This guide serves as a practical reference for analyzing Windows Event Logs generated during Active Directory attack simulations. Each entry highlights critical fields, indicators of compromise (IoCs), and SOC detection logic._

---

Event ID 4662: An operation was performed on an object

    Category / Source: Security / Directory Service Access

    MITRE ATT&CK Mapping: Reconnaissance ➔ Domain Trust Discovery / Account Discovery (T1087.002)

    Real-World Analogy: A library patron asking to see the complete inventory catalog of every book in the building at once.

    Description: Active Directory generates this log when an account attempts to access or perform operations on an Active Directory object (such as Domain DNS, Organizational Units, or User objects) if DS Access auditing is enabled.

🔍 Key Fields for Analysis (IoCs)

    ObjectType: Look for GUID %{19195a5b-6da0-11d0-afd3-00c04fd930c9}. This specific GUID represents the domainDNS object (the root of the Active Directory domain). Requesting access to the root object usually signifies domain-wide enumeration.

    AccessMask: Look for 0x100 (Control Access / Read Property). In the context of the root domain object, this indicates an entity reading properties across the directory tree.

    SubjectUserName: Identifies the account initiating the request. Correlate this with recent network logons (Event ID 4624) to verify if the request came from an unexpected host or user.

⚠️ Detection & Anomaly Logic

Benign LDAP traffic typically accesses specific user objects, OUs, or computers during standard operation. Malicious activity (e.g., using ldapsearch or automated enumeration tools) generates Event 4662 with an AccessMask of 0x100 targeting the domain root (domainDNS), often triggered repeatedly in a short timeframe from a non-standard workstation IP.
Event ID 4769: A Kerberos service ticket was requested

    Category / Source: Security / Account Logon

    MITRE ATT&CK Mapping: Credential Access ➔ Steal or Forge Kerberos Tickets: Kerberoasting (T1558.003)

    Real-World Analogy: A moviegoer explicitly demanding a flimsy paper ticket instead of a secure digital QR code so they can easily copy it later.

    Description: Active Directory generates this event on Domain Controllers every time a user requests a Kerberos Service Ticket (TGS) to access a specific network service registered with a Service Principal Name (SPN).

🔍 Key Fields for Analysis (IoCs)

    TicketEncryptionType: Look for 0x17 (RC4-HMAC). Modern Windows environments default to AES encryption (0x12 / 0x0e). Requesting 0x17 indicates an intentional downgrade attack performed by tools like Impacket to extract weaker hashes for offline brute-forcing.

    ServiceName: Displays the target account/service. If this field points to a user account (e.g., sql-service) rather than a computer account (ending with $), it confirms a request for a vulnerable service account.

    IpAddress: Indicates the client IP requesting the TGS ticket (e.g., ::ffff:192.168.1.50). Compare this IP against inventory to determine if the host is a recognized domain machine or an unauthorized device.
