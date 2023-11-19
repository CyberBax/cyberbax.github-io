---
layout: post
title: "1.2 Understand and Apply Security Concepts"
date: 2023-11-19
categories: [CISSP, Domain1 Security and Risk Management]
tags: [CISSP, Security Concepts]
description: "A comprehensive guide to understanding and applying key security concepts in CISSP, focusing on the CIA Triad: Confidentiality, Integrity, and Availability."
permalink: /cissp-understanding-security-concepts/
---

## Introduction

In the realm of cybersecurity, a grasp of foundational principles is vital for building a robust and resilient security infrastructure. This guide explores key security concepts, including the CIA Triad (Confidentiality, Integrity, and Availability), the DAD Triad, AAA Services, and essential protection mechanisms. Whether one is preparing for the CISSP exam or aiming to enhance their cybersecurity knowledge, this guide provides comprehensive insights into the core principles and practices of the field.

## The CIA Triad
Security management concepts and principles are key in policy and solution deployment, focussing on a secure environment. The primary goals of a security infrastructure are centred around the CIA Triad: Confidentiality, Integrity, and Availability.

![CIA Triad](/assets/img/CISSP/CIA.png "The CIA Triad")

Security controls are assessed based on their efficacy in upholding these three core principles. Vulnerabilities and risks are also evaluated in relation to the threat they pose to the CIA Triad.

### Confidentiality
**Confidentiality** is about ensuring the secrecy of data, objects, or resources. Its primary objective is to prevent unauthorised access while facilitating authorised access. Violations can occur due to attacks or human errors. Measures to ensure confidentiality include encryption, access control, authentication processes, data classification, and training.

#### Key Concepts of Confidentiality:
- **Sensitivity**: Refers to the potential harm or damage caused by unauthorised disclosure of information.
- **Discretion**: Involves decision-making to control or influence disclosure, minimising harm or damage.
- **Criticality**: Measures the importance of information in terms of mission criticality. Higher criticality necessitates greater confidentiality.
- **Concealment**: Involves hiding or preventing disclosure, often seen as cover, obfuscation, or distraction.
- **Secrecy**: The act of keeping something confidential.
- **Privacy**: Maintaining confidentiality of personal or potentially harmful information.
- **Seclusion**: Storing information in a secure, out-of-the-way location with strict access control.
- **Isolation**: Keeping information separate from other entities.

Organisations should tailor their confidentiality measures based on their specific needs and the types of confidentiality they wish to enforce.

### Integrity
**Integrity** involves protecting the accuracy and consistency of data. It focuses on preventing unauthorised data alterations, allowing only authorised changes. Integrity is crucial to protect against various threats like viruses, intrusions, and human errors.

#### Perspectives of Integrity:
- **Preventing unauthorised modifications**: Ensuring that only authorised subjects can alter data.
- **Preventing unauthorised modifications by authorised subjects**: Avoiding mistakes and unauthorised changes by authorised users.
- **Maintaining data consistency**: Ensuring data reflects the real world accurately and maintains valid relationships with other objects.

Integrity controls must restrict data access, and maintaining object integrity across storage, transport, and processing requires various controls and oversight.

#### Integrity Violations and Countermeasures:
- **Common threats**: Include viruses, logic bombs, unauthorised access, coding errors, malicious modification, and backdoors.
- **Human factors**: Errors, oversight, or ineptitude leading to unauthorised data alterations.
- **Countermeasures**: Include access control, authentication, intrusion detection systems, encryption, hash verifications, interface restrictions, input/function checks, and training.

Extra:
- **Hash Functions**: A cryptographic hash function is a mechanism to ensure data integrity. It takes an input and returns a fixed-size string of bytes, typically a hash value. The hash is designed to change significantly with even a small alteration in input, which is useful for detecting changes or alterations in data.

Confidentiality and integrity are interdependent; without integrity, confidentiality cannot be maintained, and vice versa.

#### Key Concepts of Integrity:
- **Accuracy**: Data being correct and precise.
- **Truthfulness**: Data accurately reflecting reality.
- **Validity**: Data being factually and logically sound.
- **Accountability**: Responsibility for actions and results.
- **Responsibility**: Control over something or someone.
- **Comprehensiveness**: Inclusion of all necessary elements for data integrity.

### Availability
**Availability** ensures that authorised subjects have timely and uninterrupted access to objects. It includes maintaining efficient access, preventing denial-of-service attacks, and ensuring the infrastructure's functionality.

#### Ensuring Availability:
- **Access and Performance**: Ensuring authorised access and acceptable performance levels.
- **Handling Interruptions**: Quickly addressing interruptions to service.
- **Redundancy**: Implementing redundant systems for critical components.
- **Backups**: Maintaining reliable backup systems and preventing data loss or destruction.

Extra:
- **Disaster Recovery Planning**: Part of a broader business continuity plan, this involves preparing for and recovering from events that cause significant disruption in availability, such as natural disasters, cyber-attacks, or system failures.

#### Threats to Availability:
- **Device Failures**: Breakdowns in hardware components.
- **Software Errors**: Bugs or glitches in software systems.
- **Environmental Issues**: Such as heat, static, flooding, power loss, etc.
- **Attacks Focused on Availability**: Including DoS attacks, destruction of objects, and communication interruptions.

#### Countermeasures for Availability:
- **Designing Delivery Systems**: Properly structured intermediary systems.
- **Effective Access Controls**: Monitoring performance and network traffic.
- **Preventing DoS Attacks**: Using firewalls and routers.
- **Redundancy**: For critical systems, to eliminate single points of failure.
- **Backup Systems**: Maintaining and testing backup systems regularly.

Availability is interlinked with both integrity and confidentiality; without these, availability cannot be maintained.

#### Key Concepts of Availability:
- **Usability**: The ease of use and learning capability of a system.
- **Accessibility**: Assuring wide interaction range with a resource.
- **Timeliness**: Promptness and low-latency response times.


## The DAD Triad

In addition to the CIA Triad, other critical security concepts must be considered when designing security policies and deploying solutions. These include the DAD Triad, the risks of overprotection, authenticity, non-repudiation, and AAA services.

The DAD Triad, contrasting the CIA Triad, includes Disclosure, Alteration, and Destruction. It represents failures in security protections of the CIA Triad.

- **Disclosure**: Unauthorized access to sensitive or confidential material, violating confidentiality.
- **Alteration**: Malicious or accidental changes to data, breaching integrity.
- **Destruction**: Damaging or rendering resources inaccessible (including denial of service), undermining availability.

![The DAD Triad](/assets/img/CISSP/DAD.png)

### Risks of Overprotection
Overprotection in one security aspect can inadvertently impact others:
- Overprotecting confidentiality or integrity might limit availability.
- Excessive emphasis on availability could lead to reduced confidentiality and integrity.

### Authenticity
Authenticity is about ensuring that data is genuine and originates from its alleged source, closely related to integrity but with a focus on source verification.

### Non-repudiation
Non-repudiation ensures that entities cannot deny their involvement in an event or action. It is crucial for maintaining accountability and is supported by identification, authentication, authorization, and auditing processes.

## AAA Concepts

AAA is a foundational concept in security, where missing any of these elements could lead to an incomplete security mechanism.

### AAA Services
AAA, standing for Authentication, Authorization, and Accounting (or sometimes Auditing), actually encompasses five elements: Identification, Authentication, Authorization, Auditing, and Accountability.

- **Identification**: Claiming an identity for system access.
- **Authentication**: Proving the claimed identity is accurate.
- **Authorization**: Granting or denying permissions to resources.
- **Auditing**: Recording events and activities related to the system and users.
- **Accountability**: Monitoring and reviewing logs for compliance and enforcing security policies.
  
![AAA Concepts](/assets/img/CISSP/aaa.jpg)

### Identification
Identification is the foundation upon which security measures are built, determining who is accessing the system and starting the process of securing resources.

- **What It Is**: The first step in AAA (Authentication, Authorization, Accountability).
- **How It Works**: Involves giving an identity, like a username or using a biometric scanner.
- **Importance**: A system uses this identity to know who's accessing it. It tracks actions under this identity.

### Authentication
Authentication is critical in verifying the accuracy of the claimed identity, serving as a gatekeeper to ensure that only legitimate users gain access.

- **What It Is**: Checking if the claimed identity is true.
- **How It Works**: Usually done with a password or other security checks.
- **Combination with Identification**: Both are needed to access a system. One without the other isn’t secure.

### Authorization
Authorization plays a crucial role in defining the scope and limits of what an authenticated user can do, thereby maintaining the security and integrity of the system.

- **What It Is**: Deciding what an authenticated person can do.
- **How It Works**: Checks if the person has the right to do a specific action or access certain data.
- **Key Point**: Just because someone is identified and authenticated doesn’t mean they can access everything.

### Auditing
Auditing is key to maintaining a secure environment by providing a detailed record of user activities, enabling oversight and detection of any unauthorized or abnormal actions.

- **What It Is**: Keeping track of what people do on a system.
- **Purpose**: Helps in finding unauthorized or strange actions. It’s like a detailed activity log.
- **Use of Logs**: Helps in understanding events, finding problems, or providing evidence.

### Accountability
Accountability ensures that all actions within the system are attributable to an individual, forming an essential component of a comprehensive security strategy.

- **What It Is**: Making sure people are responsible for their actions in the system.
- **Dependence**: Relies on strong identification, authentication, and auditing.
- **Legal Support**: Important for backing up security actions in legal situations.

### Visualizing Protection Mechanisms
In cybersecurity, various protection mechanisms are deployed to safeguard information and systems. These mechanisms, each with its unique approach and function, work together to create a comprehensive security strategy. Key concepts include:

#### Defense in Depth (Layering)
- **Idea**: Implementing multiple layers of security controls throughout an IT system.
- **Goal**: To provide redundancy in case one layer fails, ensuring that other layers continue to protect the system.

#### Abstraction
- **Idea**: Simplifying complex systems by grouping similar elements for more manageable security administration.
- **Application**: Widely used in both programming and setting up layered security systems.

#### Data Hiding
- **Idea**: Concealing data to prevent unauthorized access, ensuring that sensitive information is not visible or accessible to unapproved users.
- **Difference from Obscurity**: Unlike security through obscurity, data hiding involves active measures to make data inaccessible, not just unnoticed.

#### Encryption
- **What It Is**: The process of converting data into a coded format to prevent unauthorized access.
- **Application**: Essential in securing digital communications, data storage, and ensuring the privacy and integrity of sensitive information.

These mechanisms are integral to modern cybersecurity strategies, providing diverse layers of protection against a wide range of threats.

## Security Boundaries

A security boundary is like a line that separates different areas or networks with different security needs. Imagine it as a barrier between a super secure place and a not-so-secure one, like a local network and the internet. 

**Identifying Boundaries**: It's crucial to know where these security boundaries are, both in a network and the real world. Once the boundaries are found, rules are set up to control how information moves across them.

**Different Types**: Security boundaries can take different forms. For instance, some things might be more important than others. Each of these importance levels is a security boundary. 

**Physical vs. Logical**: Security boundaries exist both in the physical world (think locks and keys) and the digital world (like passwords and firewalls). Both are needed to be really secure, and there are rules for each.

**Clear Definitions**: It's super important to be clear about where these boundaries start and end, whether it's in the real world or online. Security rules should say exactly where the control begins and ends.

**Logical Security**: In the digital world, logical security is where electronic stuff meets responsibility. Unauthorized folks should know they can't get in. 

**Physical Security**: In the real world, responsibility usually determines the security boundaries. It could be the walls of an office, a building, or a campus. Signs often warn that getting in without permission means trouble.

**Matching Both**: When turning security rules into real controls, think about each world separately. Choose the security tools that make sense for each situation. But remember, don't spend more on security than the stuff being protected is worth.

In simple terms, security boundaries are like lines that separate safe places from not-so-safe ones. There are rules for both the online and offline worlds to keep things secure.



