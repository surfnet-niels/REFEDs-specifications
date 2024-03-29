Pseudonymous Access Entity Category
-----------------------------------

**Version History**

[v.1 published 13 March 2021](https://zenodo.org/record/5113256)  
v.2 published 13 February 2023 (this version)

**Reference pdf**

[https://zenodo.org/record/7684488/files/ENTCAT-PSEUD-v2.pdf]("https://zenodo.org/record/7684488/files/ENTCAT-PSEUD-v2.pdf)

**DOI**

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7684488.svg)](https://doi.org/10.5281/zenodo.7684488)

**License**

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

**Supporting Material**

[https://wiki.refeds.org/x/aQA2B](https://wiki.refeds.org/x/aQA2B)

### Overview
Research and Education Federations are invited to use the REFEDS Pseudonymous Access Entity Category with their members to support the release of attributes to Service Providers meeting the requirements described below.

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119 \[BCP14\].

This definition is written in compliance with the Entity Category SAML Entity Metadata Attribute Types specification \[RFC8409\]; this specification may be extended to reference other protocol-specific formulations as circumstances warrant.

An FAQ for the Entity Category has been made available to help deployments \[FAQ\].

**1\. Definition**
------------------

Candidates for the Pseudonymous Access Entity Category are Service Providers that offer a level of service based on proof of successful authentication and offer personalization based on a pseudonymous user identifier. The Service Provider must be able to effectively demonstrate this need to their federation registrar (normally the Service Provider’s home federation) and demonstrate their compliance with regulatory requirements concerning personal data through a published Privacy Notice.

None of the attributes in this entity category are specifically intended to provide authorization information. See section 6 for a discussion of this use case.

Identity Providers may indicate support for this Entity Category to facilitate discovery and improve the user experience at Service Providers. Self-assertion is the typical approach used, but this is not the only acceptable method.

**2\. Syntax**
--------------

The following URI is used as the attribute value for the Entity Category and Entity Category Support attribute:

    https://refeds.org/category/pseudonymous

**3\. Semantics**
-------------

By asserting a Service Provider to be a member of this Entity Category, a federation registrar claims that:

*   (SE1) The Service Provider has requested assignment of the Category and complies with this entity category’s registration criteria.
*   (SE2) The Service Provider’s request to be assigned the Pseudonymous Access Entity Category has been reviewed against the provided REFEDS \[Guidelines\] and approved by the federation registrar.

By registering for this Entity Category, a Service Provider has agreed to the registration criteria as defined in Section 4.

By asserting support for this Entity Category, Identity Providers are indicating that they will release attributes to Service Providers that also assert this category.

**4\. Registration Criteria**
-------------------------

When a Service Provider’s federation registers the Service Provider in the Entity Category, the federation registrar MUST perform at least the following checks:

*   (RC1) The service has a proven and documented need for the pseudonymous information that forms the attribute bundle for this entity category.
*   (RC2) The Service Provider has committed to data minimisation and will not use the attributes for purposes other than as described in their request.
*   (RC3) Ensure that the service meets the following technical requirements:
    *   (RC3.1) The Service Provider provides an <mdui:DisplayName>, <mdui:InformationURL>, and <mdui:PrivacyStatementURL> in metadata. Including an English language version (i.e., xml:lang=”en”) is RECOMMENDED.
    *   (RC3.2) The Service Provider provides one or more contacts in metadata.

These are the requirements to assert this entity category; any change MUST be reported by the Service Provider to the federation registrar. The federation registrar MUST remove the Entity Category if the Service Provider indicates a change in conformance. The federation registrar MUST have other remediation procedures to address a lack of compliance with these requirements.

**5\. Service Provider Requirements**
---------------------------------

The mechanism by which this entity category provides for consistent attribute release is through the definition of a set of commonly supported and consumed attributes. The attributes chosen represent a privacy baseline such that further minimization achieves no particular benefit for applicable services. Thus, the minimal disclosure principle is designed into this category.

The use of the <md:RequestedAttribute> mechanism supported by SAML metadata is outside the scope of this category, and may co-exist with it in deployments as desired, subject to this specification’s requirements being met.

### 5.1 Required Attributes

The _entity category attribute bundle_ consists (abstractly) of the following data elements:

*   _organization_
*   _pseudonymous pairwise user identifier_
*   _affiliation_
*   _assurance_

These abstract elements are bound to protocol-specific definitions in the following subsection(s) and additional bindings may be added in the future.

It is understood that not every subject can necessarily be associated with values for every attribute. For example, some users may have no formal affiliation with the issuing organization. In such cases, it is expected that those attribute(s) may not be provided. The designation that all these attributes are required is a general obligation and not specific to a given subject.

With regard to assurance, the REFEDS Assurance Framework \[RAF\] is REQUIRED as a source of values, but other frameworks and their values are permitted. The requirement to support the REFEDS Assurance Framework implies that at least one value, ‘[https://refeds.org/assurance](https://refeds.org/assurance)‘ MUST be supplied, but no others are specifically required unless the IdP deems them to be applicable.

Identity Providers are not expected or required to alter their business processes or to provide any particular assurance level for their subjects, but rather are required to communicate what they do provide or other applicable information as appropriate.

#### 5.1.1 SAML 2.0

When the SAML 2.0 protocol is used, the following SAML attributes make up the required attribute set defined abstractly above. In all cases, the defined NameFormat is urn:oasis:names:tc:SAML:2.0:attrname-format:uri

*   _organization_ is defined to be:
    *   schacHomeOrganization \[SCHAC\]
        *   Attribute Name: urn:oid:1.3.6.1.4.1.25178.1.2.9
*   _pseudonymous pairwise user identifier_ is defined to be:
    *   pairwise-id \[SAMLSubId\]
        *   Attribute Name: urn:oasis:names:tc:SAML:attribute:pairwise-id
*   _affiliation_ is defined to be:
    *   *   eduPersonScopedAffiliation \[eduPerson\]
            *   Attribute Name: urn:oid:1.3.6.1.4.1.5923.1.1.1.9
*   _assurance_ is defined to be:
    *   *   eduPersonAssurance \[eduPerson\]
            *   Attribute Name: urn:oid:1.3.6.1.4.1.5923.1.1.1.11

The specific naming and format of the attributes above is guided by the \[SAMLAttr\] and \[SAMLSubId\] profiles.

6.Authorization
---------------

None of the attributes defined in Section 5 are suitable for accurately signaling access authorization; signaling authorization is out of scope for this entity category. While they are often used as approximations, this inevitably denies access to authorized users and permits access to unauthorized users.

A companion document discussing the federated authorization problem and suggested practices can be found at \[FederatedAuthorization\].

**7\. Deployment Guidance for Service Providers**
---------------------------------------------

Service Providers SHOULD rely on the bundle of attributes defined in Section 5, but MAY ask for, or even require, other information as needed for additional purposes, via mechanisms that are outside the scope of this specification.

A common example would be a requirement for indicating authorization to access a service (see Section 6).

A Service Provider that conforms to this entity category would exhibit the following entity attribute in SAML metadata:
```
<mdattr:EntityAttributes xmlns:mdattr="urn:oasis:names:tc:SAML:metadata:attribute">  
  <saml:Attribute  
      xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"  
      NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:uri"  
      Name="[http://macedir.org/entity-category"](http://macedir.org/entity-category)\>  
    <saml:AttributeValue>https://refeds.org/category/pseudonymous</saml:AttributeValue>  
  </saml:Attribute>  
</mdattr:EntityAttributes>
```
**8\. Deployment Guidance for Identity Providers**
--------------------------------------------

An Identity Provider indicates support for this entity category by exhibiting the entity attribute in its metadata. Such an Identity Provider MUST, for a significant subset of its user population, release all required attributes in the bundle defined in Section 5 to all Service Providers registered for this entity category, either automatically or subject to user consent or notification, without administrative involvement by any party.

An Identity Provider that supports this entity category would exhibit the following entity attribute in SAML metadata:
```
<mdattr:EntityAttributes xmlns:mdattr="urn:oasis:names:tc:SAML:metadata:attribute">  
  <saml:Attribute  
      xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"  
      NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:uri"  
      Name="[http://macedir.org/entity-category-support"](http://macedir.org/entity-category-support)\>  
  <saml:AttributeValue>https://refeds.org/category/pseudonymous</saml:AttributeValue>  
  </saml:Attribute>  
</mdattr:EntityAttributes>
```
**9\. References**
--------------

\[[BCP14](https://www.rfc-editor.org/info/rfc2119)\] Bradner, S., “Key words for use in RFCs to Indicate Requirement Levels”, BCP 14, RFC 2119, March 1997. Leiba, B., “Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words”, BCP 14, RFC 8174, May 2017, [https://www.rfc-editor.org/info/bcp14](https://www.rfc-editor.org/info/bcp14).

\[[eduPerson](https://refeds.org/eduperson.)\] REFEDS, “eduPerson,” [https://refeds.org/specifications/eduperson](https://refeds.org/specifications/eduperson).

\[[FAQ](https://wiki.refeds.org/x/aQA2B)\] REFEDS, “Anonymous, Pseudonymous, and Personalized Access FAQ,” wiki page, [https://wiki.refeds.org/x/aQA2B](https://wiki.refeds.org/x/aQA2B).

\[[FederatedAuthorization](https://wiki.refeds.org/x/qITNB)\] REFEDS, “Federated Authorization Best Practices,” wiki page, [https://wiki.refeds.org/x/qITNB](https://wiki.refeds.org/x/qITNB).

\[[Guidelines](https://wiki.refeds.org/x/AQCfC)\] REFEDS, “Requirements for Federations Operators Assessing Access-Related Entity Categories”, wiki page, [https://wiki.refeds.org/x/AQCfC](https://wiki.refeds.org/x/AQCfC).

\[[RFC8409](https://www.rfc-editor.org/info/rfc8409)\] Young, I., Ed., Johansson, L., and S. Cantor, “The Entity Category Security Assertion Markup Language (SAML) Attribute Types”, RFC 8409, DOI 10.17487/RFC8409, August 2018, [https://www.rfc-editor.org/info/rfc8409](https://www.rfc-editor.org/info/rfc8409).

\[[SAMLAttr](https://refeds.org/wp-content/uploads/2022/02/internet2-mace-dir-saml-attributes-200804.pdf)\] Internet2 MACE Directory Working Group, “MACE-Dir SAML Attribute Profiles”, April 2008, [https://refeds.org/wp-content/uploads/2022/02/internet2-mace-dir-saml-attributes-200804.pdf](https://refeds.org/wp-content/uploads/2022/02/internet2-mace-dir-saml-attributes-200804.pdf).

\[[SAMLSubId](https://docs.oasis-open.org/security/saml-subject-id-attr/v1.0/saml-subject-id-attr-v1.0.odt)\] OASIS Committee Specification, “SAMLV2.0 Subject Identifier Attributes Profile Version 1.0, January 2019”, [https://docs.oasis-open.org/security/saml-subject-id-attr/v1.0/saml-subject-id-attr-v1.0.odt](https://docs.oasis-open.org/security/saml-subject-id-attr/v1.0/saml-subject-id-attr-v1.0.odt).

\[[SCHAC](https://wiki.refeds.org/display/STAN/SCHAC)\] REFEDS, “Schema for ACademia”, [https://refeds.org/specifications/schac](https://refeds.org/specifications/schac)[.](https://wiki.refeds.org/display/STAN/SCHAC)