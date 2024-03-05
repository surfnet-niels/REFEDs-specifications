Personalized Access Entity Label
-----------------------------------

**Version History**

[v.1 published 30th November 2021](https://zenodo.org/record/5741746)  
[v.2 published 13th February 2023](https://zenodo.org/record/7684449)    
v3. published XYZ (this version)

**Reference pdf**

[https://zenodo.org/record/7684449/files/ENTCAT-PER-v2.pdf](https://zenodo.org/record/7684449/files/ENTCAT-PER-v2.pdf)

**DOI**

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7684449.svg)](https://doi.org/10.5281/zenodo.7684449)

**License**

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/80x15.png)](http://creativecommons.org/licenses/by-sa/4.0/)  
This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

**Supporting Material**

[https://wiki.refeds.org/x/aQA2B](https://wiki.refeds.org/x/aQA2B)

### Overview

Research and Education Federations are invited to use the REFEDS Personalized Access Entity Label with their members to support the release of attributes to Service Providers meeting the requirements described below.

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119 \[BCP14\].

This specification includes reference to protocol-specific formulations as circumstances warrant in Chapter 6

An FAQ for the Entity Label has been made available to help deployments \[FAQ\].

**1\. Definition**
------------------

Candidates for the Personalized Access Entity Label are Services that have a proven need to receive a small set of personally identifiable information about their users in order to effectively provide their service to the user or to enable the user to signal their identity to other users within the service. The Service must be able to effectively demonstrate this need to the entity issueing the identifier for the label and demonstrate their compliance with regulatory requirements concerning personal data through a published Privacy Notice.
None of the attributes are specifically intended to provide authorization information. See section 7 for a discussion of this use case.
Depending on the implementation protocol used different requirements exist for the entity releasing the attributes towards the Services. See section 6 for a discussion of these cases.

**2\. Syntax**
--------------

The following URI is used as the identifier for the entity label:

    https://refeds.org/category/personalized

**3\. Semantics**
-----------------

By asserting a Service Provider to be a member of this Entity Label, a federation registrar claims that:

*   (SE1) The Service Provider requested assignment of the label and complies with this entity label’s registration criteria.
*   (SE2) The Service Provider’s request to be assigned the Personalized Access Entity Label has been reviewed against the provided REFEDS \[Guidelines\] and approved by the federation registrar.

By registering for this Entity Label, a Service Provider has agreed to the registration criteria as defined in Section 4.

~~By asserting support for this Entity Label, Identity Providers are indicating that they will release attributes to Service Providers that also assert this category.~~

**4\. Registration Criteria**
-----------------------------

When a Service federation registers the Service in the Entity Label, the federation registrar MUST perform at least the following checks:

*   (RC1) The service has a proven and documented need for the personally identifiable information that forms the attribute bundle for this entity label.
*   (RC2) The Service has committed to data minimisation and will not use the attributes for purposes other than as described in their request.
*   (RC3) Ensure that the service meets the following technical requirements:
    *   ~~(RC3.1) The Service Provider provides an <mdui:DisplayName>, <mdui:InformationURL>, and <mdui:PrivacyStatementURL> in metadata. Including an English language version (i.e., xml:lang=”en”) is RECOMMENDED.~~
    *   (RC3.1) To support enduser facing intercaes, the Service provides a descriptive name of the service, an information URL which points to a web page where you may further elaborate details about your service or organization and an URL points to a web page containing your service (organization)'s user privacy and data protection statement. Including an English language version (i.e., xml:lang=”en”) is RECOMMENDED.
    *   (RC3.2) The Service provides one or more contacts in metadata.
    The techical implementation for these criteria depend on the specific protocol used and are described in Chapter 6.

These are the requirements to assert this entity label; any change MUST be reported by the Service to the federation registrar. The federation registrar MUST remove the Entity Label if the Service indicates a change in conformance. The federation registrar MUST have other remediation procedures to address a lack of compliance with these requirements.

**5\. Attribute Bundle**
------------------------

The mechanism by which this entity label provides for consistent attribute release is through the definition of a set of commonly supported and consumed attributes. The attributes chosen represent a privacy baseline such that further minimization achieves no particular benefit for applicable services. Thus, the minimal disclosure principle is designed into the label.

The use of the <md:RequestedAttribute> mechanism supported by SAML metadata is outside the scope of this category, and may co-exist with it in deployments as desired, subject to this specification’s requirements being met.
`Do we have a similar ptoblem with OIDC?`

#### 5.1 Required Attributes

The _entity label attribute bundle_ consists (abstractly) of the following data elements:

*   _organization_
*   _user identifier_
*   _person name_
*   _email address_
*   _affiliation_
*   _assurance_

These abstract elements are bound to protocol-specific definitions in the following subsection(s) and additional bindings may be added in the future.

It is understood that not every subject can necessarily be associated with values for every attribute. For example, some users may have no formal affiliation with the issuing organization. In such cases, it is expected that those attribute(s) may not be provided. The designation that all these attributes are required is a general obligation and not specific to a given subject.

With regard to assurance, the REFEDS Assurance Framework \[RAF\] is REQUIRED as a source of values, but other frameworks and their values are permitted. The requirement to support the REFEDS Assurance Framework implies that at least one value, ‘[https://refeds.org/assurance](https://refeds.org/assurance)‘ MUST be supplied, 
`but no others are specifically required unless the IdP deems them to be applicable.`

Identity Providers are not expected or required to alter their business processes or to provide any particular assurance level for their subjects, but rather are required to communicate what they do provide, or other applicable information as appropriate.

**6\. Protocol specific implementation**
------------------------

##### 6.1 SAML 2.0
------------------

###### 6.1.1 Entity Category
To signal compliance when using SAML 2.0, the label is to be used as an Entity Category and Entity Category Support attribute. This definition is written in compliance with the Entity Category SAML Entity Metadata Attribute Types specification \[RFC8409\];

###### 6.1.2 Implementing the Registration Criteria
To technically implement the registration criteria as describe in Chapter 4 the Service should:
*   (RC3.1)  The Service Provider provides an <mdui:DisplayName>, <mdui:InformationURL>, and <mdui:PrivacyStatementURL> in metadata. 
Including an English language version (i.e., xml:lang=”en”) is RECOMMENDED.
*   (RC3.2) The Service provides one or more contacts in metadata.

###### 6.1.3 Attribute set

The following SAML Attributes make up the required attribute set defined abstractly above. In all cases, the defined NameFormat is urn:oasis:names:tc:SAML:2.0:attrname-format:uri

*   _organization_ is defined to be:
    *   schacHomeOrganization \[SCHAC\]
        *   Attribute Name: urn:oid:1.3.6.1.4.1.25178.1.2.9
*   _user identifier_ is defined to be:
    *   subject-id \[SAMLSubId\]
        *   Attribute Name: urn:oasis:names:tc:SAML:attribute:subject-id
*   _person name_ is defined to be all of:
    *   displayName \[eduPerson\]
        *   Attribute Name: urn:oid:2.16.840.1.113730.3.1.241
    *   givenName \[eduPerson\]
        *   Attribute Name: urn:oid:2.5.4.42
    *   sn \[eduPerson\]
        *   Attribute Name: urn:oid:2.5.4.4
*   _email address_ is defined to be:
    *   mail \[eduPerson\]
        *   Attribute Name: urn:oid:0.9.2342.19200300.100.1.3
*   _affiliation_ is defined to be:
    *   eduPersonScopedAffiliation \[eduPerson\]
        *   Attribute Name: urn:oid:1.3.6.1.4.1.5923.1.1.1.9
*   _assurance_ is defined to be:
    *   eduPersonAssurance \[eduPerson\]
        *   Attribute Name: urn:oid:1.3.6.1.4.1.5923.1.1.1.11

The specific naming and format of the attributes above is guided by the \[SAMLAttr\] and \[SAMLSubId\] profiles.
Identity Providers may indicate support for this Entity Category to facilitate discovery and improve the user experience at Service Providers. Self-assertion is the typical approach used but this is not the only acceptable method.

###### 6.1.4\. Deployment Guidance for Service Providers

Service Providers SHOULD rely on the bundle of attributes defined in Section 5 and 6.1.3, but MAY ask for, or even require, other information as needed for additional purposes, via mechanisms that are outside the scope of this specification.

A common example would be a requirement for indicating authorization to access a service (see Section 7).

A Service Provider that conforms to this entity category would exhibit the following entity attribute in SAML metadata:
```
<mdattr:EntityAttributes xmlns:mdattr="urn:oasis:names:tc:SAML:metadata:attribute">
   <saml:Attribute xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
      NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:uri"
      Name="http://macedir.org/entity-category">
   <saml:AttributeValue>https://refeds.org/category/personalized</saml:AttributeValue>
   </saml:Attribute>
</mdattr:EntityAttributes>
```

###### 6.1.5\. Deployment Guidance for Identity Providers

An Identity Provider indicates support for this entity category by exhibiting the entity attribute in its metadata. Such an Identity Provider MUST, for a significant subset of its user population, release all required attributes in the bundle defined in Section 5 to all tagged Service Providers, either automatically or subject to user consent or notification, without administrative involvement by any party.

An Identity Provider that supports this entity category would exhibit the following entity attribute in SAML metadata:
```
<mdattr:EntityAttributes xmlns:mdattr="urn:oasis:names:tc:SAML:metadata:attribute">
  <saml:Attribute
     xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
     NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:uri"
     Name="http://macedir.org/entity-category-support">
  <saml:AttributeValue>https://refeds.org/category/personalized</saml:AttributeValue>
  </saml:Attribute>
</mdattr:EntityAttributes>
```


##### 6.2 OpenIDConnect and OpenID Federation
--------------------------------------------

###### 6.2.1 Trustmark
To signal compliance when using OIDC and OpenID Federation the label is to be used as a Trustmark [Trustmark]. This definition is written in compliance with the Trustmark specification as described in the OpenID Federation specification [OpenID Federation specification]; In OpenID Connect Relying Parties (RP) are the data consumers and OpenID Providers (OP) are the data providers.

The Personalized Access Label has different semantics when it comes to OPs and RPS that are consuming identity information.
In the case of a service, a need must be confirmed for the personalized data, so that excessive or uncesessary personal data transfer can be prevented. This may be done for instance by a federation registrar. The services should not self-assert such a label.

In case of an OP, the source itself may signal its capability and willingness to release personal data. Since they are data controllers for their users, they may decide this internally. Therefore, personalized access release capability may be self-asserted. 

RPs can be holders of "Personalized Access RP" trust marks, which MUST NOT be self-asserted. They need to be issued by a trustmark issuer defined by the trust anchor according to OpenID Federation specifications. If a trustmark issuer issues this trust mark it MUST (SHOULD?) establish a mechanism to verify that the OP indeed has this capability.

OPs can be holders of "Personalized Access OP" trust marks, which MAY be self asserted. If a trustmark issuer issues this trust mark it MAY establish a mechanism to verify that the RP indeed has this need.

In order for an OP to release data to an RP according to the Personalized Access mechanism, it MUST establish a trust chain from the RP to the trust anchor and it MUST verify the Personalized Access RP trust mark. Both the establishment of the trust chain and the trust mark verification MUST be done according to the OpenID Federation specification. This check MUST be done periodically and MAY be done before each transaction.

RPs MAY rely on "Personalized Access OP" trust mark for discovery purposes.

The Trustmark issuer MUST validate the Trustmark Issuence Criteria before the Trustmark is issued

###### 6.2.2 Implementing the Trustmark Issuence Criteria
The client metadata requirements for recieving the Trustmark make use of the OpenID Connect Dynamic Client Registration specification [OpenID Connect Dynamic Client Registration]
To be allagable for the Trustmark as described in Chapter 4 the Service should:
*   (RC3.1)  The Service MUST provide an client_name, client_uri, and policy_uri in metadata. Including an English language version in accordance with the Metadata Languages and Scripts section 2.1 [Metadata Languages and Scripts] is RECOMMENDED.
*   (RC3.2) The Service provides one or more contacts in metadata, using the contacts parameter
` ToDo: This does not align well with the current best pratice in SAML to have a clear seperation of concerns (admin/technical/helpdesk/security) `


###### 6.2.3 Scope and claims

For the purpose of streamlined exchange of personal data, a scope named "personalized" is introduced. The OP and RP MUST implement the use of this scope if they claim compliance with the Personalized Access Entity Label. Requesting claims follows the pattern as described in the OpenID Connect specification, section 5.4 [Requesting Claims using Scope Values].

The claims for the scope are defined as following:

| Member | Type | Definition|
|---|---|---|
|_user identifier_|Subject-ID| 
|_name_|string| End-User's full name in displayable form including all name parts, possibly including titles and suffixes, ordered according to the End-User's locale and preferences. The equivelent of the eduPerson DisplayName attribute
|_given_name_|string| Given name(s) or first name(s) of the End-User. Note that in some cultures, people can have multiple given names; all can be present, with the names being separated by space characters. The equivelent of the eduPerson givenName attribute.
|_family_name_|string| Surname(s) or last name(s) of the End-User. Note that in some cultures, people can have multiple family names or no family name; all can be present, with the names being separated by space characters. The equivelent of the eduPerson sn attribute.
|_email_|string| End-User's e-mail address. Its value MUST conform to the RFC 5322 [RFC5322] addr-spec syntax. The RP MUST NOT rely upon this value being unique. If multiple email adresses are available, it is left to the implementer to choose which address needs to go into the single valued email claim
|_email_verified_|boolean| true if the End-User's email address has been verified; otherwise false. When this Claim Value is true, this means that the OP took affirmative steps to ensure that this email address was controlled by the End-User at the time the verification was performed. The means by which an e-mail address is verified is context-specific, and dependent upon the trust framework or contractual agreements within which the parties are operating.
|_eduperson_affiliation_|string| Specifies the person's relationship(s) to the institution in broad categories such as student, faculty, staff, alum, etc. Permissible values: faculty, student, staff, alum, member, affiliate, employee, library-walk-in. The equivelent of the  eduPersonScopedAffiliation attribute.
|_schac_home_organization_|string| A person's home organization using the domain name of the organization. The equivelent of the schacHomeOrganization attribute
|_eduperson_assurance_|string| Set of URIs that assert compliance with specific standards for identity assurance. The equivelent of the eduPersonAssurance attribute.

###### 6.2.4\. Deployment Guidance for Relying Parties
A Relying Parties that conforms to this entity label MUST exhibit the following Trustmark in metadata:
```

```

Relying Parties SHOULD rely on using the personalized scope for requesting the bundle of claim defined in Section 5 and 6.2.3, but MAY ask for, or even require, other information as needed for additional purposes, via mechanisms that are outside the scope of this specification. A common example would be a requirement for indicating authorization to access a service (see Section 7).
If individual claims are requested, e.g. by using the claims request paramater [Requesting Claims using the "claims" Request Parameter], and the OP is advertising the personalized Trustmark, the Relying Party may assume the semantics of the claims issued by the OP are consistent with section 6.2.3.

###### 6.2.5\. Deployment Guidance for OpenID Providers
An OpenID Provider indicates conformance to this entity label by exhibiting the Trustmark in its metadata. Such an OpenID Provider MUST, for a significant subset of its user population, release all required claims in the bundle defined in Section 5 to all tagged Relying Parties, either automatically or subject to user consent or notification, ```without administrative involvement by any party.```

An OpenID Provider that supports this entity label would exhibit the following entity attribute in SAML metadata:
```

```





**7\. Authorization**
---------------------

None of the attributes or claims defined in Section 5 are suitable for accurately signalling access authorization; signalling authorization is out of scope for this entity label. While they are often used as approximations, this inevitably denies access to authorized users and permits access to unauthorized users.

A companion document discussing the federated authorization problem and suggested practices can be found at \[FederatedAuthorization\].


**8\. References**
------------------

\[[BCP14](https://www.rfc-editor.org/info/bcp14)\] Bradner, S., “Key words for use in RFCs to Indicate Requirement Levels”, BCP 14, RFC 2119, March 1997; and Leiba, B., “Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words”, BCP 14, RFC 8174, May 2017, [https://www.rfc-editor.org/info/bcp14](https://www.rfc-editor.org/info/bcp14).

\[[eduPerson](https://refeds.org/eduperson.)\] REFEDS, “eduPerson”, [https://refeds.org/specifications/eduperson](https://refeds.org/specifications/eduperson).

\[[FAQ](https://wiki.refeds.org/x/aQA2B)\] REFEDS, “Anonymous , Pseudonymous, and Personalized Access FAQ,” wiki page, [https://wiki.refeds.org/x/aQA2B](https://wiki.refeds.org/x/aQA2B).

\[[FederatedAuthorization](https://wiki.refeds.org/x/qITNB)\] REFEDS, “Federated Authorization Best Practices,” wiki page, [https://wiki.refeds.org/x/qITNB](https://wiki.refeds.org/x/qITNB).

\[[Guidelines](https://wiki.refeds.org/x/AQCfC)\] REFEDS, “Requirements for Federations Operators Assessing Access-Related Entity Categories,” wiki page, [https://wiki.refeds.org/x/AQCfC](https://wiki.refeds.org/x/AQCfC).

\[[RAF](https://refeds.org/assurance)\] “REFEDS Assurance Framework,” REFEDS, [https://refeds.org/assurance](https://refeds.org/assurance).

\[[RFC8409](https://www.rfc-editor.org/info/rfc8409)\] Young, I., Ed., Johansson, L., and S. Cantor, “The Entity Category Security Assertion Markup Language (SAML) Attribute Types”, RFC 8409, DOI 10.17487/RFC8409, August 2018, <[https://www.rfc-editor.org/info/rfc8409](https://www.rfc-editor.org/info/rfc8409)\>.

\[[SAMLAttr](https://refeds.org/wp-content/uploads/2022/02/internet2-mace-dir-saml-attributes-200804.pdf)\] Internet2 MACE Directory Working Group, “MACE-Dir SAML Attribute Profiles”, April 2008, [https://refeds.org/wp-content/uploads/2022/02/internet2-mace-dir-saml-attributes-200804.pdf](https://refeds.org/wp-content/uploads/2022/02/internet2-mace-dir-saml-attributes-200804.pdf).

\[[SAMLSubId](https://docs.oasis-open.org/security/saml-subject-id-attr/v1.0/saml-subject-id-attr-v1.0.odt)\] OASIS Committee Specification, SAMLV2.0 Subject Identifier Attributes Profile Version 1.0, January 2019, [https://docs.oasis-open.org/security/saml-subject-id-attr/v1.0/saml-subject-id-attr-v1.0.odt](https://docs.oasis-open.org/security/saml-subject-id-attr/v1.0/saml-subject-id-attr-v1.0.odt).

\[[SCHAC](https://wiki.refeds.org/display/STAN/SCHAC)\] REFEDS, “Schema for ACademia,” [https://refeds.org/specifications/schac](https://refeds.org/specifications/schac)[.](https://wiki.refeds.org/display/STAN/SCHAC)

\[Trustmark](https://openid.net/specs/openid-federation-1_0.html#name-trust-marks) Trustmarks, OpenID Federation 1.0,[https://openid.net/specs/openid-federation-1_0.html#name-trust-marks] (https://openid.net/specs/openid-federation-1_0.html#name-trust-marks)

\[OpenID Federation specification](https://openid.net/specs/openid-federation-1_0.htm), OpenID Federation 1.0, [https://openid.net/specs/openid-federation-1_0.htm](https://openid.net/specs/openid-federation-1_0.htm)

\[OpenID Connect Dynamic Client Registration](https://openid.net/specs/openid-connect-registration-1_0.html), OpenID Connect Dynamic Client Registration, [https://openid.net/specs/openid-connect-registration-1_0.html](https://openid.net/specs/openid-connect-registration-1_0.html)

\[Metadata Languages and Scripts](https://openid.net/specs/openid-connect-registration-1_0.html#LanguagesAndScripts), Metadata Languages and Scripts, OpenID Connect Dynamic Client Registration, Section 2.1, [https://openid.net/specs/openid-connect-registration-1_0.html#LanguagesAndScripts](https://openid.net/specs/openid-connect-registration-1_0.html#LanguagesAndScripts)

\[Requesting Claims using Scope Values] OpenID Connect Core 1.0 incorporating errata set 2 [https://openid.net/specs/openid-connect-core-1_0.html#ScopeClaims]

\[White Paper for implementation of mappings between SAML 2.0 and OpenID Connect in Research and Education][https://docs.google.com/document/d/1b-Mlet3Lq7qKLEf1BnHJ4nL1fq-vMe7fzpXyrq2wp08/edit#heading=h.c4ib3eojk7el]

\[Requesting Claims using the "claims" Request Parameter] OpenID Connect Core 1.0 incorporating errata set 2 [https://openid.net/specs/openid-connect-core-1_0.html#ClaimsParameter]

