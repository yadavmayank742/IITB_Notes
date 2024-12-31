## Course Syllabus 

In this course, we will explore the latest research on identifying and countering these threats, covering topics such as
    systems for firewall detection and circumvention,
    web tracking and traffic analysis countermeasures,
    anonymous communication networks like Tor, and
    other privacy-enhancing technologies (PETS).

Traffic filtering:
    Introduction :
        what is traffic,
        how it is different from standard firewall operations,
        different levels in different ISPs?
    Triggers :
        What type of content is filtered?
        Technical mechanisms to identify what type of content blocking.
        This involves
            studying IP tables,
            constructing packets using Raw Sockets to bypass protocol stack in the kernel etc.

Measurement Techniques to detect firewalls :
    How to assess blocking,
    different detection approaches with limitations etc.
    Studying SSL and TLS protocols in detail,
    identifying information leak in DNS, HTTP and TLS protocol.
    Use of traceroutes to learn about the network paths,
    identifying the network hop of the firewall etc.

Great Firewall of China (GFC) :
    One of the most sophisticated content blocking apparatus deployed at the country scale.
    Studying how network security researchers remotely characterize the filtering capability of the GFW for more than two decades.
    This involves studying creation of Transmission Control Block (TCB), how custom packets can break the TCB etc.

Identifying loopholes in firewalls :
    Characterizing sophisticated middleboxes (modified firewalls) deployed by different ISPs,
    measuring end-to-end delays using HTTP Ping, Iperf etc., caused by these middleboxes

Privacy:
    Overview :
        Different definitions and expectations of privacy;
        notions of Privacy at different network layers
    Web tracking:
        How a user is tracked over the web;
        tracking cookies;
        browser fingerprinting etc.
        Can firewalls help in user tracking?
    Anti-tracking techniques:
        Tracker list,
        ad-blockers,
        cookie partitioning etc
    Privacy Law:
        High-level idea of GDPR, CCPA and DPDPA etc., and
        detailed know how of their technical implementation
    Anonymity over Internet:
        Definitions of anonymity, why anonymity etc
    Anonymity Solutions:
        Proxies,
        Tor,
        Mixnets (intro)


## Course Modalities

Combination of in-class lectures, paper reading, hands-on components--programming assignments, projects.

## Course References


(1) Research papers from conferences and journals - e.g., NDSS, IMC, Usenix Security, CCS, PETS etc.
(2) Kurose, James F., and Keith W. Ross. Computer Networks: A Top-Down Approach. 6th ed., Pearson, 2.
(3) Stallings, W., & Brown, L. Computer security: Principles and practice 3rd ed., Pearson, 2
(4) Stallings, W., Cryptography and Network Security: Principles and Practice, 8th ed., Pearson, 2022
(5) Viega, John, Messier, Matt, and Chandra, Pravir. Network Security with OpenSSL: Cryptography for Secure Communications. O`Reilly Media, 2002.
(6) Forouzan, Behrouz A. Data Communications and Networking. 5th ed., McGraw-Hill Education, 2013.