**Project inCredible**

[https://github.com/sunbird-specs/inCredible](https://github.com/sunbird-specs/inCredible)

**Technical Specification - Version 1.0**

March 2019

**Table of Contents**
* [Introduction](#introduction)
      * [Principles](#principles)
   * [Proposed Specifications](#proposed-specifications)
      * [Conceptual Model](#conceptual-model)
      * [Data Modelling Principles](#data-modelling-principles)
      * [Visual Representation](#visual-representation)
         * [<strong>QR Codes</strong>](#qr-codes)
      * [Entity Identity](#entity-identity)
      * [Structural Model](#structural-model)
         * [<strong>Assertion</strong>](#assertion)
         * [<strong>Recipient</strong>](#recipient)
         * [<strong>BadgeClass</strong>](#badgeclass)
         * [<strong>AwardingBody</strong>](#awardingbody)
         * [<strong>Competency Standard</strong>](#competency-standard)
         * [<strong>Evidence</strong>](#evidence)
         * [<strong>Assessor</strong>](#assessor)
      * [Data Model](#data-model)
         * [<strong>Open Standards</strong>](#open-standards)
         * [<strong>Identifiers</strong>](#identifiers)
            * [<strong>Identifier Namespaces</strong>](#identifier-namespaces)
            * [<strong>URN Identifiers</strong>](#urn-identifiers)
            * [<strong>Institution Ids</strong>](#institution-ids)
            * [<strong>Individual Ids</strong>](#individual-ids)
            * [<strong>Object Ids</strong>](#object-ids)
      * [Object Model](#object-model)
         * [<strong>Assertion</strong>](#assertion-1)
         * [<strong>CertificateExtension</strong>](#certificateextension)
         * [<strong>CompositeIdentity Object</strong>](#compositeidentity-object)
         * [<strong>BadgeClass</strong>](#badgeclass-1)
         * [<strong>Profile: AwardingBody/Assessor/Trainer</strong>](#profile-awardingbodyassessortrainer)
         * [<strong>Alignment Object</strong>](#alignment-object)
         * [<strong>Evidence</strong>](#evidence-1)
         * [<strong>TrainingEvidence</strong>](#trainingevidence)
         * [<strong>AssessedEvidence</strong>](#assessedevidence)
         * [<strong>Assessment</strong>](#assessment)
            * [<strong>MarksAssessment</strong>](#marksassessment)
         * [<strong>Signatory Extension</strong>](#signatory-extension)
      * [Additional Properties](#additional-properties)
      * [Examples](#examples)
         * [<strong>Ecosystem</strong>](#ecosystem)
      * [Issuing Credentials](#issuing-credentials)
         * [<strong>Signing Procedure for Assertions and Evidence</strong>](#signing-procedure-for-assertions-and-evidence)
      * [Usage](#usage)
         * [<strong>Delivery and Storage of Credentials</strong>](#delivery-and-storage-of-credentials)
            * [<strong>Email</strong>](#email)
            * [<strong>Web</strong>](#web)
            * [<strong>DigiLocker and other National Repositories</strong>](#digilocker-and-other-national-repositories)
            * [<strong>Blockchain</strong>](#blockchain)
            * [<strong>Wallet</strong>](#wallet)
            * [<strong>uPort</strong>](#uport)
         * [<strong>Verifying Authenticity of a Certificate</strong>](#verifying-authenticity-of-a-certificate)
            * [<strong>Key Management</strong>](#key-management)
   * [References](#references)

# Introduction

The jobs and skilling ecosystem is a complex arena with a number of frictions preventing an optimal supply and demand equilibrium, resulting in not only underemployment but also significant wage gaps. These frictions include low trust, information asymmetry, low ability to compare, and portability amongst others.

A core issue in the jobs and skills arena is the difficulty an individual faces in showcasing their skills and exchanging credentials in a trusted manner. This document proposes a set of electronic standards for machine-readable data to represent various credentials in the skilling ecosystem across industry verticals. An electronic standard for data representing credentials allows certificates to be awarded in digital, machine-readable formats. Machine-readable formats in-turn make it possible for an individual to freely transfer credentials in a trusted manner and apply for jobs remotely.

Currently, skills certificates are issued in paper form, meaning they are neither verifiable digitally nor machine readable. In contrast, digital credentials are freely portable and easily verifiable at scale and speed by employers and job matching platforms, whilst continuing to allow print and other visual forms for human consumption.

This document presents an open specification which can be incorporated into the information management systems of skill training providers, apprenticeships, employers, testing agencies, or others in the ecosystem. It is targeted towards technology and implementation teams within organisations who award certificates.

In this document the terms _credential _and _credentials_ are used to mean a _qualification or achievement of a person or entity used to indicate their suitability for something_. A certificate or other form of attestation is typically issued to award such a qualification.


```
NOTE: This specification is based on Open Badges 2.0 with necessary extensions.
```



## Principles

**Verifiability: **Authenticity of a credential should be digitally verifiable by any application to which it is presented. This verification need not require the physical presence of the credential holder.

**Portability**: The credentials should be digitally portable across systems participating in the ecosystem. Physical certificates are unrestricted -- the recipient can present the certificate to any party of her choice. The same property should be preserved. This includes easy digital storage in the control of the recipient of the credentials and easy consented transfer & sharing by the recipient for various purposes.

**Permanence:** The credentials should continue to exist and be valid beyond the lifetime of the institution where it was awarded. That is, if an organisation which has awarded a credential subsequently ceases to exist, the credentials remain verifiable and portable across the ecosystem.

**Self Describing:** The credential model should be self-describing in a manner that the consumer of the credential does not require private sources of information to validate or understand it. In practice, this means that any declaration of skill level or reference to an awarding institution links to a publicly accessible and unencumbered source of further information. This makes the credential truly portable across the ecosystem, since anyone to whom it is presented can make sense of the information contained within and have enough context to compare the accreditation with another certificate.

**Privacy Protecting: **The agencies adopting these specifications must give paramount importance to the principles of privacy preservation including data protection and consented sharing.


# Proposed Specifications


## Conceptual Model

A certificate captures a relationship between the following entities



*   Awarding body
*   Recipient
*   Domain
*   Standard(s) accomplished
*   Assessor
*   Evaluation
*   Time

The **awarding body** certifies that the **recipient** has **accomplished **specified** standard(s)** in a **domain** based on an **evaluation** conducted by the **assessor **at a** particular time**.

Note that a single certificate may be issued for the recipient's accomplishment of multiple standards.


<p align=”center”>

![alt_text](spec_images/actors.png "The actors in the certificate ecosystem")

**Fig 1** The actors in the certificate ecosystem
</p>


## Data Modelling Principles



1. All entities in the certificate issuance transaction must be represented using machine-readable objects
2. Each object in the data-model is a representation of an entity
3. Assign strong identifiers to all entities where some other party might reasonably want say something about an entity or do something with the representation of the entity. The strong identifiers for the entities should never be altered.


## Visual Representation

A visual representation of the credential (rendering) can be generated using data from the JSON-LD representation and subsequently embedded into the JSON-LD object. Applications issuing credentials can apply business-specific rules for rendering certificates. In some contexts, it may be preferable to create multiple renderings -- the granularity of the details presented can be tuned according to the needs outlined by the use case.

Applications are also open to using format of choice when embedding the rendered certificate. Formats such as PDF documents or images are well-suited for long-term survivability and compatibility. PDF documents may also carry metadata inside them. Other formats such as HTML are attractive as they are easier to generate. One must note, however, that HTML standards evolve over time. To ensure that embedded HTML will render well twenty or thirty years in the future, a very minimal and high-compatibility subset of HTML should be used.


### **QR Codes**

Printable representations of the credential may also carry QR codes as an offline-to-online bridge. If a QR code is part of the printable representation then the QR code may contain credential metadata in its payload which aid in the verification of the credential. There are two broad means of verifying a credential, either by verifying the digital signature of a hosted representation or by verifying the digital signature offline.



1. If the credential is cloud-hosted,
    1. the QR code should contain the HTTP URI from where the signed JSON-LD document describing the credential can be retrieved.
    2. Once retrieved, this JSON-LD data may be passed to downstream digital systems for signature verification.
    3. It may also be stored offline for further sharing or for other needs including visual comparison against the printed credential.
2. If the credential is not hosted in the cloud,
    4. If the credential JSON document is small enough, the JSON payload may be encoded as a string and embedded into the QR code. To reduce the size of the JSON, the payload may be compressed using the GZIP compression algorithm.
    5. If the credential JSON document is larger than 2900 bytes, the QR code should contain essential information to verify the digital signature offline. The following items required for signature verification should be inserted into a JSON object and encoded as a string then embedded into the QR code.
        1. **<code>@id</code></strong>: @id of the document
        2. <strong><code>hash</code></strong>: hash of the document without the <strong><code>ocd:signature</code></strong> element
        3. <strong><code>key_id</code></strong>: HTTP URI of the key used to sign the credential
        4. <strong><code>signatureValue</code></strong>: bytes of the digital signature generated using (a) and (b)


## Entity Identity

An important part of issuing credentials is to identify the entities involved in the process. To issue the credential a few different types of entities participate: institutions, individuals, documents and standards. Since a credential is a permanent document by nature which may be used and remain valid over a long period of time, two broad principles apply for all identifiers:



*   **Singularity**: An identifier should resolve to a single entity, for example a person or an institution are single entities.
*   **Permanence**: An identifier should not be reassigned to a different entity at a future point.

For example, a phone number is not a good means of identifying a person for the purpose of issuing a credential. A credential must be valid for many years, it may be presented for validation 10, 20 or even 50 years later. A person's phone number may change in the intervening time-period and the number given up by that person may be re-allocated to another different person. Hence an ID, such as a phone number, which does not provide the guarantee of resolving to the same person for the duration of use of the credential is not well-suited for identifying the recipient.

Conversely, a document such as a passport or a voter identity card (which will eventually expire) is a better candidate for identifying a person since the passport number or voter id number is not reused and will always continue to represent the same person over time.


## Structural Model

The structural model of a credential aligns with the OpenBadges v2.0 schema and adds extensions where necessary.

<p align=”center”>
<img align="center" width="440" height="540" src=spec_images/structural_model.png alt="The credential structural model" />

**Fig 2**: The Credential Structural Model
</p>


### **Assertion**

An assertion is a statement of fact. The credentials issued are statements of fact about recipient's accomplishments. Hence, the root object of the credential is called an assertion. The assertion object is a container object for sub-objects representing the awarding body, recipient and the recipient's credentials being certified. The assertion object described in this specification extends the OpenBadges v2 **<code>Assertion</code></strong> object with a few additional properties via the <strong><code>CertificateExtension</code></strong> class.


### **Recipient**

The recipient of the certificate may be an individual or an organisation. The recipient of the certificate is identified by an **<code>IdentityObject.</code></strong>


### **BadgeClass**

The **<code>BadgeClass</code></strong> describes a category of credentials that is awarded. The badge class contains details of the awarding body of the credential, the skill domain & standard achieved. For instance, one category of of credentials may be a School Leaving Certificate awarded by a school board, another could be a Bachelor's Degree certificate awarded by a University.


### **AwardingBody**

The awarding body of the credential will be an organisation or institution which is a competent authority to certify recipients. Note that the awarding body is different from the signatory (i.e. the individual(s) who applies his/her signature to the credential).


### **Competency Standard**

Standard is a skill definition or a competency defined by a certified standards body for the domain. Any given standard must be uniquely identifiable and will also commonly be part of a framework which defines relationships between standards in a domain. **<code>BadgeClass</code></strong> descriptions link to defined standards via <strong><code>AlignmentObjects</code></strong>.


### **Evidence**

The credential may contain one more list items of evidence which have been assessed in support of the credential. Each item of evidence may contain an assessment performed by the assessor. The evidence may link to standards criteria and a level of mastery which the recipient displays for the given criterion.


### **Assessor**

The assessor evaluates a trainee's competencies. The assessor is an organisation or institution which has been certified as a competent authority to assess skills for a given domain standard(s).


## Data Model


### **Open Standards**

The credentials data model uses the following standards for defining a credential:



*   Alignment with OpenBadges v2 vocabulary for defining accomplishments. The OpenBadges vocabulary is extended in some areas for specific use cases.
*   RDF 1.1 (Resource Description Framework) is used as the means for expressing the data contained in a credential.
*   The preferred RDF serialisation format is JSON-LD, however, consumers of a credential are free to use alternative serialisation formats such as RDFs or a triple expression language such as Turtle.
*   The credentials model uses (and in some places extends) the vocabulary of Classes and Properties described by schema.org and the WebPayments specification.
*   Additionally the credentials model defines some new classes of objects.
*   Each object class used in the model must be defined in terms of an RDF schema. Under the JSON-LD serialisation format, the schema needs to be published and made available at a specific web URL for validation and consumption of credentials (a hypothetical schema URL is used in the example below).


### **Identifiers**

Based on the above principles for identifying entities using strong identifiers the following apply when assigning identifiers for objects.



*   Use URIs wherever possible for compatibility with web protocols
*   Since we represent data in JSON-LD, the preferred URI for an entity is a dereferenceable URL which points to the location where the entity's JSON-LD representation can be found
*   If a URL is unavailable, use a URN. The id must be created within a well-known namespace with an established namespace identifier (NID)
    *   URN: **<code>urn:{namespace-id}:{private-id}</code></strong>
*   If an established NID is unavailable to create a URN, the TAG URI scheme can be used when there is a web domain name for the creator of the ID.
    *   TAG:<strong><code> tag:{creator-domain},{domain-register-date}:{id-type}:{id}</code></strong>
*   Where URNs and TAGs cannot be derived, strong globally unique identifiers should be created via locally unique identifiers using <strong><code>IdentityObject </code></strong>where the <strong><code>@type</code></strong> is a namespace describing the type of identifier and the identity is the local ID (see an example in the certificate below).
    *   <strong><code>@type</code></strong> should be a string which contains two parts separated by a delimer, the first part must be a well-known id for the creator of the local identifier, the second part can be any string which describes the id


#### <strong>Identifier Namespaces</strong>

Below, we propose some informal namespaces for commonly used identifiers types. These namespaces can be used as the NID for URNs. The format used for NIDs is **<code>in.<domain>.<id-creator>.<id-type></code></strong>, where domains are .gov, .edu, .com & .org. This format can be used to construct new informal namespaces for NIDs.

Non-unique namespaces cannot be used as NIDs for URNs but may be utilised as the @type property for a component of a composite identity represented by an **<code>IdentityObject</code></strong>.

Following identifier types are used commonly in India.


<table>
  <tr>
   <td><strong>Identifier Type</strong>
   </td>
   <td><strong>Namespace</strong>
   </td>
   <td><strong>Example</strong>
   </td>
  </tr>
  <tr>
   <td>PAN
   </td>
   <td><strong><code>in.gov.itd.pan</code></strong>
   </td>
   <td><strong><code>urn:in.gov.itd.pan:ZZZZZ00000</code></strong>
   </td>
  </tr>
  <tr>
   <td>GSTN
   </td>
   <td><strong><code>in.gov.gstn.gstn</code></strong>
   </td>
   <td><strong><code>urn:in.gov.gstn.gstn:Z00000000000001</code></strong>
   </td>
  </tr>
  <tr>
   <td>Driver License (KA)
   </td>
   <td><strong><code>in.gov.ka-dot.dl</code></strong>
   </td>
   <td><strong><code>urn:in.gov.ka-dot.dl:ZAAAAAAAAAAAAB</code></strong>
   </td>
  </tr>
  <tr>
   <td>Driver License (MH)
   </td>
   <td><strong><code>in.gov.mh-dot.dl</code></strong>
   </td>
   <td><strong><code>urn:in.gov.mh-dot.dl:ZOOOOOOOOOOOAB</code></strong>
   </td>
  </tr>
  <tr>
   <td>Aadhaar
   </td>
   <td><strong><code>in.gov.uidai.aadhaar</code></strong>
   </td>
   <td><strong><code>urn:in.gov.uidai.aadhaar:11111111111</code></strong>
   </td>
  </tr>
  <tr>
   <td>Voter Identity
   </td>
   <td><strong><code>in.gov.eci.voterid</code></strong>
   </td>
   <td><strong><code>urn:in.gov.eci.voterid:X11111111X</code></strong>
   </td>
  </tr>
  <tr>
   <td>Passport
   </td>
   <td><strong><code>in.gov.mea.psprt</code></strong>
   </td>
   <td><strong><code>urn:in.gov.mea.psprt:XX99999999</code></strong>
   </td>
  </tr>
  <tr>
   <td>Roll Number
   </td>
   <td><strong><code>in.<dom>.<iss>.rollno</code></strong>
   </td>
   <td><strong><code>urn:in.gov.cbse.rollno:999999999</code></strong>
   </td>
  </tr>
  <tr>
   <td>Name
   </td>
   <td><strong><code>name</code></strong>
   </td>
   <td><strong><code>Ram Singh</code></strong>
   </td>
  </tr>
  <tr>
   <td>Date of Birth
   </td>
   <td><strong><code>dob</code></strong>
   </td>
   <td><strong><code>Date of birth in YYYY-MM-DD format</code></strong>
   </td>
  </tr>
  <tr>
   <td>Photo
   </td>
   <td><strong><code>photo</code></strong>
   </td>
   <td><strong><code>data:image/png;base64,<base64 encoded></code></strong>
   </td>
  </tr>
</table>


Table 1:  Informal namespaces for commonly used identifiers


#### **URN Identifiers**

URNs are URIs which follow the Universal Resource Name (URN) scheme. A URN consists of three parts separated by colons (:)

**urn        **:        **{nid}        **:        **{nss}**

**    **namespace id    namespace specific string

The namespace id (nid) defines the type of identifier. The consumer of a URN can make processing decisions based on the nid. The consumer could use the nid to determine how to resolve the namespace specific string to an entity. For instance, the isbn namespace is registered for ISBN book codes.

The namespace specific string (nss) is the value of the ID within the nid. Continuing the above example of books, the nss would be the ISBN of a specific book such as 8120351312.

Together, the combination of **<code>urn:isbn:8120351312</code></strong> forms a URN which uniquely identifies a book.


#### **Institution Ids**

Institutions are identified in two scenarios. The first of these is an institution is an awarding body of credentials or is an assessor of a subject (recipient). In this scenario, the institution should be identified using a URL which points to the institution's profile (in JSON-LD format). The profile must contain the awarding body/assessor properties defined in the model below. Additionally, the profile may also contain more information about the institution (e.g. rankings, institutional standards, authorisations etc) using the appropriate RDF schemas. The profile may also contain links to other tools where such information about the institution can be retrieved.

Second, as the recipient of credentials, institutions should also be identified using a URL which points to the institution's profile. The profile data may contain embedded objects detailing publicly available and well-known identifier types. The would be represented using the RDF **<code>sameAs</code></strong> property whose value is an <strong><code>IdentityObject</code></strong>. When using such identifiers the identity can be represented as a URN.


#### **Individual Ids**

Individuals are identified in two scenarios. First as recipients of credentials and second, as signatories to a credential. In both scenarios, the individuals should be identified by an **<code>IdentityObject </code></strong>which contains one or more identifying attributes. If the individual can be identified by a HTTP URL, the <strong><code>IdentityObject</code></strong> should be of <strong><code>@type: "url"</code></strong>. In case of an identity which is comprised of multiple parts, an <strong><code>IdentityObject</code></strong> of <strong><code>@type: "composite"</code></strong> should be used containing components which are in turn <strong><code>IdentityObjects</code></strong> of a variety of types.

Typically, an individual is identified by a combination of name, date of birth, gender and photo. Aside from this, other attributes like the name of a relative or a masked unique identifier may also be used. Agencies are encouraged to support the use of multiple modes of identity which may be available to recipients.

If using unique identifiers, agencies should evaluate privacy concerns which may stem from embedding a unique identifier into the credential. In such cases, a masked identifier may serve the purpose of identifying the individual without compromising privacy.


#### **Object Ids**

Machine-readable objects such as **<code>Assertions</code></strong>, <strong><code>BadgeClasses</code></strong> & <strong><code>Evidence</code></strong> should be identified for the purpose of validation and comparison.

**Assertions & Evidence**

Ideally, Assertions and Evidence should be identified via a UUID encoded as a URN.

Example: **<code>urn:uuid:ec58b28e-a6ab-49c2-a24d-ebefa02476cd</code></strong>

If use of a UUID is not feasible, for instance if documents are numbered serially, the TAG URI scheme should be used where a document id is prefixed with a namespace consisting of the document creator's domain name, its registration date and the document type.

Example:**<code> tag:exampleinstitute.org,2010-09:marksheet:9871624</code></strong>

**BadgeClass**

BadgeClasses should ideally be identified via a HTTP URL which returns a JSON-LD representation of the class. If the BadgeClass is defined for a single ad-hoc usage and is not published at a URL, a UUID encoded as a URN is recommended.  


## Object Model

Objects and the properties as defined by this credentials specification are detailed here.


### **Assertion**

The base of the model is an assertion. The assertion class is defined as part of the **<code>OpenBadges</code></strong> v2.0 specification. Some additional properties are added via <strong><code>CertificateExtension.</code></strong>



*   **<code>Id </code></strong>which uniquely identifies the assertion. If assertions are verified by signing, a UUID should be used from the<strong><code> urn:uuid</code></strong> namespace. If hosted verification is used, the Id should be a HTTP URL to a JSON-LD document containing the certificate data.
*   <strong><code>Type </code></strong>An array containing the strings Assertion, Extension and <strong><code>CertificateExtension</code></strong>
*   <strong><code>AwardedOn </code></strong>when the credential was awarded
*   <strong><code>Recipient</code>(s) </strong>person(s) or organisation(s) who received the credential.
    *   If the certificate contains signed evidence, the subject of the evidence can be assigned a relative IRI as an @id and referenced as the recipient of the certificate.
        *   <strong><code>"recipient": {"@id": "#/evidence/0/subject"}</code></strong>
    *   If there are multiple recipients, the element should be a list of entities
*   <strong><code>Badge</code></strong> an embedded BadgeClass object which describes the type of certificate being awarded or a HTTP URL which contains a machine-readable representation of a BadgeClass
*   optional <strong><code>Image</code></strong> which is a HTTP URL to a <em>baked</em> PNG or SVG image
*   <strong><code>Evidence</code> </strong>containing details of competencies assessed
*   optional <strong><code>Expires</code></strong> containing the date the certificate ends validity
*   <strong><code>Verification</code></strong> containing the string <strong><code>LinkedDataSignatures</code></strong> for signed certificates
*   <strong><code>Narrative</code></strong> as text or markdown text which can be used to describe and connect multiple pieces of evidence


### <strong>CertificateExtension</strong>

The Assertion type from OpenBadges is extended by the **<code>CertificateExtension</code></strong> which adds the following field definitions.



*   optional **<code>AwardedThrough</code></strong> service or program through which the credential is awarded (eg: PMKVY)
*   optional list of <strong><code>Signatory(s)</code></strong> who signed the certificate
*   <strong><code>PrintUri</code> </strong>a HTTP URL which points to a printable version of the certificate (for instance the digilocker URL where the certificate HTML is stored).
    *   The printable version of the certificate can be embedded into the machine-readable data using data URIs. The encoding scheme is: <strong><code>data:[mime-type][;base64],<base64-encoded-data></code></strong>
        *   A base64 encoded PDF document could be represented as a data URI: <strong><code>data:application/pdf;base64,<base64 encoded binary PDF></code></strong>
        *   A base64 encoded image document can be represented as a data URI: <strong><code>data:image/jpeg;base64,<base64 encoded binary JPG></code></strong>
    *   If there are multiple printable documents to be embedded, a list of URIs can be added.
*   optional <strong><code>ValidFrom</code> </strong>containing the date the certificate begins validity
*   <strong><code>Signature</code></strong> added by the awarding body using its private key for signed verification


### <strong>CompositeIdentity Object</strong>

OpenBadges v2 uses IdentityObjects to represent the recipient of a certificate. We extend it to represent a composite identity which is composed of a sub component **<code>IdentityObjects</code></strong>.

To facilitate composite identities, the specification introduces:



*   a new **<code>IdentityObject</code></strong> <strong><code>@type</code></strong> identifier called <strong><code>composite</code></strong>
*   a new property <strong><code>annotation</code></strong> which can be used to qualify the identity type
*   a new property <strong><code>components</code></strong> for composite identities. This property will contain sub-fields of the identity

The fields of a composite <strong><code>IdentityObject</code></strong> will be



*   **<code>Type</code></strong> will be Composite
*   <strong><code>Hashed</code></strong> will be false
*   <strong><code>Identity</code></strong> will be omitted
*   <strong><code>Components</code></strong> will be an array of other <strong><code>IdentityObjects</code></strong>

Additionally, we define the following <strong><code>IdentityObject</code></strong> <strong><code>type</code></strong> identifiers to extend the set of  profile identifier properties defined by OpenBadges.



*   **<code>composite</code></strong>: the identity is expressed as a composite identity containing <strong><code>components</code></strong>
*   <strong><code>name</code></strong>: the identity is expressed as a name, often used in conjunction with <strong><code>annotation </code></strong>to represent a father's or a spouse's name. May be part of a composite identity
*   <strong><code>photo</code></strong>: the identity is expressed as a photo, either a HTTP URL for a image or a data URI containing the mime type and image data in base64 encoding. May be part of a composite identity
*   <strong><code>dob</code></strong>: the identity is expressed as the date of birth in YYYY-MM-DD format. May be part of a composite identity
*   <strong><code>gender</code></strong>: the identity is expressed as the gender of the individual. May be part of a composite identity.
*   <strong><code>tag</code></strong>: the identity is expressed as a Tag URI
*   <strong><code>urn</code></strong>: the identity is expressed as a Uniform Resource Name (urn) URI
*   <strong><code>url</code></strong>: the identity is expressed as a Universal Resource Location (url) URI which may be dereferenced


### <strong>BadgeClass</strong>



*   **<code>Id</code></strong> which uniquely identifies the <strong><code>BadgeClass</code></strong>
    *   If the credential is an instance of a larger category of certificates which may be awarded multiple times, it must be a HTTP URL where the JSON-LD description of the <strong><code>BadgeClass</code></strong> is available.
    *   If the certificate is ad-hoc or short-lived and unlikely to be awarded repeatedly, a <strong><code>urn:uuid</code></strong> class identifier can be used
*   <strong><code>Type</code></strong> will be the string BadgeClass
*   <strong><code>Name</code></strong> The name of the credential represented by this <strong><code>BadgeClass</code></strong>
*   optional <strong><code>Description</code></strong> A short text description of the credential
*   optional <strong><code>Version</code></strong> describing the version of the <strong><code>BadgeClass</code></strong>, which can be updated as the credentials evolve over time.
*   optional <strong><code>Image</code></strong> an image representing the credential, may be a HTTP URL where the image can be found or a data URI including mime-type
*   optional <strong><code>Criteria</code></strong> an embedded object describing the criteria for achieving the credential or a HTTP URL of a JSON-LD object describing the criteria
*   <strong><code>AwardedBy</code></strong> AwardingBody profile of person or organisation entity which awarded the credential. It is recommended that the complete JSON-LD object representing the awarding body is embedded into the BadgeClass. The set of fields to uniquely identify the awarding body and to verify the awarding body's signature on the credential <em>must</em> be embedded into the certificate. If the complete awarding body profile is not embedded into the BadgeClass, then the <strong><code>@id</code></strong> of the embedded object must be a HTTP URL from which a more complete JSON-LD object can be retrieved.
*   optional <strong><code>Alignment</code></strong> which maps the <strong><code>BadgeClass</code></strong> to one or more academic standards.
*   optional <strong><code>Related</code></strong> an object or list of objects relating this <strong><code>BadgeClass</code></strong> to other <strong><code>BadgeClasses</code></strong>.
    *   If the <strong><code>BadgeClass</code></strong> is part of a series, for instance if a new class is created for each batch or semester, this may be used to link to previous instances of the same class.


### <strong>Profile: AwardingBody/Assessor/Trainer</strong>



*   **<code>Identifier</code> or<code> ID</code> </strong>to identify the awarding body. Should be a HTTP URL where a JSON-LD object describing the awarding body can be retrieved.
*   <strong><code>Type</code></strong> will be the array <strong><code>Profile</code></strong> along with <strong><code>Extension</code></strong> and <strong><code>SignatoryExtension</code></strong> if the profile is for an entity which will be providing digital signatures.
*   <strong><code>Name</code></strong> the name by which the awarding body is known
*   optional <strong><code>Email</code></strong> containing the address where this awarding body can be reached
*   optional <strong><code>URL</code></strong> pointing to a HTTP accessible profile page or homepage of the awarding body
*   optional <strong><code>Description</code></strong> short text describing the issuing person or organisation
*   <strong><code>PublicKey</code></strong> containing the public key of the awarding body/Assessor/Trainer which must be embedded inside the assertion if the credential is signed.
*   optional <strong><code>RevocationList</code></strong> containing a HTTP URL of the list of signed badges awarded by this body which have been revoked


### <strong>Alignment Object</strong>

The OpenBadges v2 **<code>AlignmentObject</code></strong> is used to link a <strong><code>BadgeClass</code></strong> or an item of <strong><code>Evidence</code></strong> to an academic standard.



*   **<code>targetName</code></strong> which identifies the name of target standard
*   <strong><code>targetURL</code></strong> a HTTP endpoint which uniquely identifies the standard where a description of the standard can be found. Ideally should be a JSON-LD object describing the standard.
*   <strong><code>targetFramework</code></strong> a string describing the name of the standards framework
*   <strong><code>targetCode</code></strong> a string containing a code within target framework for the aligned standard


### <strong>Evidence</strong>

The **<code>Evidence</code></strong> class from OpenBadges v2 spec is used to describe evidence in support of a credential.



*   **<code>Id </code></strong>which uniquely identifies the evidence from the <strong><code>urn:uuid</code></strong> namespace or a HTTP URL of a webpage which presents the evidence
*   <strong><code>Type</code></strong> containing the string Evidence. Additional types Extension and <strong><code>AssessedEvidence</code></strong> will be added when using <strong><code>AssessedEvidence</code></strong>
*   optional textual <strong><code>Narrative</code></strong> which describes the evidence
*   optional text <strong><code>Name</code></strong> of the evidence
*   optional longer text <strong><code>Description</code></strong> of the evidence
*   optional text <strong><code>Genre</code></strong> which describes the type of evidence, such as Certificate, Painting, Artefact, Medal, Video, Image. May be omitted in favour of the <strong><code>assessment</code></strong> property in the context of <strong><code>AssessedEvidence</code></strong>
*   optional text <strong><code>Audience</code></strong> detailing the audience for which the evidence is presented
*   optional <strong><code>Alignment</code></strong> containing details of alignment to educational standards.


### <strong>TrainingEvidence</strong>

The **<code>TrainingEvidence</code></strong> class is used to add training specific properties to an item of <strong><code>Evidence.</code></strong>



*   **<code>Type</code></strong> should an array containing <strong><code>Evidence,</code></strong> <strong><code>Extension</code></strong>, <strong><code>TrainingEvidence</code></strong>
*   <strong><code>Subject</code>(s)</strong> the subject(s) of the evidence
*   <strong><code>TrainedBy(s)</code></strong>HTTP URL identifier to a JSON-LD object or an embedded profile of the person or organisation entity(s) which provided training to the recipient of the credential. The <strong><code>@id</code></strong> of the profile should either be a URI which uniquely identifies the training entity or should be a HTTP URL from which a more complete JSON-LD object can be retrieved
*   optional <strong><code>Duration</code></strong> containing <strong><code>startDate</code></strong> and <strong><code>endDate</code></strong> specifying the duration of the course
*   optional <strong><code>Session</code></strong> containing a string which describes which session of the course the recipient completed


### <strong>AssessedEvidence</strong>

The **<code>AssessedEvidence</code></strong> class is an extension to the evidence class which adds additional fields for assessors and signatures.



*   **<code>Type</code></strong> should an array containing <strong><code>Evidence, Extension</code></strong>, <strong><code>AssessedEvidence</code></strong>
*   <strong><code>Subject</code>(s)</strong> the subject(s) of the evidence
*   <strong><code>Assessment</code></strong> conducted which elicited the evidence
*   <strong><code>AssessedBy</code> </strong>HTTP URL identifier to a JSON-LD object or an embedded profile of the individual(s) or organisation(s) who assessed the competency. The <strong><code>@id</code></strong> of the profile should either be a URI which uniquely identifies the training entity or should be a HTTP URL from which a more complete JSON-LD object can be retrieved
*   <strong><code>AssessedOn</code> </strong>the date when the assessment was conducted
*   optional <strong><code>Signature</code></strong> of the assessor(s)

If assessors are not ready and able to submit individually signed evidence, the assessor's signature on the <strong><code>AssessedEvidence</code></strong> may be omitted. It is then the responsibility of the awarding body to ensure the authenticity of the evidence submitted by the assessor through other available channels. Over time, migrating the assessment ecosystem to standardise on individually signed items of evidence will increase the overall level of trust in the certification process and will increase the utility of certificates in the employment process.


### **Assessment**

**<code>Assessments</code></strong> can vary based on the nature of the assessment carried out. The essential fields of an assessment are



*   **<code>Type</code></strong> of the assessment will be <strong><code>marks</code></strong>, <strong><code>percentage</code></strong>, <strong><code>grade</code></strong>, <strong><code>rank</code></strong> or some other means of assessing the subject
*   <strong><code>Value</code></strong> of the assessment based on the type indicated.

Specific types of assessments may add additional properties to the Assessment object. Each new property must be published via JSON-LD documents which describe the schema and means of validation for the property.


#### **MarksAssessment**

To illustrate, a _schema for a marks-based assessment_ which adds additional properties to the Assessment schema is described:



*   **<code>MinValue</code> </strong>The minimum score which could have been achieved
*   <strong><code>MaxValue</code></strong> The maximum score which could have been achieved
*   <strong><code>PassValue</code></strong> The passing score for the assessment


### <strong>Signatory Extension</strong>

**<code>SignatoryExtension</code></strong> extends the OpenBadges v2 <strong><code>IdentityObject</code></strong> to add the following properties.



*   optional **<code>Designation</code></strong> of the signatory
*   optional <strong><code>Image</code></strong> containing a HTTP URL or a data URI for an image associated with the signatory
*   optional <strong><code>PublicKey</code></strong> object containing the public key of the signatory as defined by the LinkedDataSignatures specification. Required if the signatory will affix their digital signature to the credential.


## Additional Properties

Since the objects are modeled using RDF principles, additional properties may be added to the objects without affecting consumers. All properties and metadata not defined here which are used as extensions to the credential specification must follow or be compatible with available metadata standards.



*   All consumers of credential data must be able to accept objects containing additional properties beyond the ones described as part of the credentials standard.
*   RDF properties define a set of classes which are in the domain of a property. When adding a new property to an object, the appropriate domain class must be included in the** <code>@type</code></strong> array.


## Examples


### **Ecosystem**

The examples below are based on a proposed ecosystem of awarding bodies and assessors whose electronic profiles are available for consumption and validation. The ecosystem comprises:



1. A federated system of credential awarding bodies where each body maintains its independent profile at HTTPS endpoints. When an awarding body commences issuing certificates, the awarding body's profile JSON-LD document is published to the web in a publicly accessible manner. This profile is accessed via HTTPS protocol and _must_ be protected by a Class II or Class III X.509 SSL certificate under the control of the awarding body. Hence all information about awarding bodies which is retrieved from their self-hosted profile  is trusted.
2. A federated system of credential awarding bodies where each body maintains its independent public keys and certificate metadata at HTTPS endpoints. The public keys of the awarding bodies MUST be referenced from their self-hosted profile.
3. Assessors in the ecosystem publish their own profiles, which are accessed via HTTPS endpoints.
    1. In the examples below, we assume an assessor which maintains its profile at **<code>https://example.assessor.org/opencreds/profile.json</code></strong>
4. Assessors also publish public keys and records of assessments conducted at HTTPS endpoints. The public keys of the assessors must be referenced from their published profile.
    2. In the examples below, we assume the assessor publishes keys at <strong><code>https://example.assessor.org/keys/...</code></strong>


## Issuing Credentials

Credentials are issued by creating an assertion using the items of data described below. They reference the structure of the assertions in the examples described above



1. **Assertion ID**: Each assertion must be given a unique id. In the example above, the unique id is a web URL where JSON-LD representation of the certificate can be retrieved. Where URLs cannot be generated to store representations of the certificate, a URI in the**<code> urn:uuid</code></strong> namespace can be generated.
2. <strong>Awarding body ID</strong>: In the first example given above, the awarding body's identity (<strong><code>badge.awardedBy.@id</code></strong>) is represented using a tag URI. This shows an example of adding an identifier to a resource object where a HTTP URI is not available. The remaining examples identify the BadgeClass's awarding body with an <strong><code>@id</code></strong> field which is a HTTP URI to a JSON-LD object containing the awarding body's profile.
3. <strong>Awarding body Public Key</strong>: the awarding body's public key from the cryptographic key pair (<strong><code>badge.awardedBy.publicKey</code></strong>) is embedded into the certificate for verifiability.
4. <strong>Recipient ID</strong>: in the first example given above, the recipient is identified by a hash of the recipients email address (<strong><code>recipient.identity</code></strong>). The recipient may be identified by other strong identifiers. Where the information in the identifier is sensitive, the identifier can be salted and hashed for security
5. <strong>Evidence</strong>: The awarding body collects evidence from the assessors of the trainee. The evidence may optionally be signed. The awarding body must ensure that
    1. The subject of the evaluation conducted is the same person to whom the credentials are being issued. The awarding body can do this by comparing the id of the evidence's subject (<strong><code>evidence[i].subject.identity</code></strong>) with the id of the recipient (<strong><code>recipient.identity</code></strong>).
    2. If the evidence is signed by the assessors, each evidence's signature can be verified by using the assessor's publicKey embedded in the evidence (<strong><code>evidence.assessedBy.publicKey</code></strong>).
6. <strong>Signature</strong>: Finally, the awarding body uses their own private key to generate a signature for the assertion data and inserts that signature to the assertion. In the event that there is a signatory to the certificate who is also applying a digital signature, the unsigned assertion is signed using the signatory's private key as well. Both signatures are then included in the list of signatures for the certificate.
    3. The signing algorithm to be followed is the LinkedDataSignatures 1.0 algorithm, described here:[ https://w3c-dvcg.github.io/ld-signatures/#signature-algorithm](https://w3c-dvcg.github.io/ld-signatures/#signature-algorithm)
    4. The signature suite to be used to sign the credential is RsaSignature2018


### <strong>Signing Procedure for Assertions and Evidence</strong>

Signing a certificate is a process by which a one-way digest of the assertion object is computed and is then cryptographically signed (encryption) using the awarding body's private key. The signature suite used will specify the digest and the cryptographic functions which are to be applied (suggestion is to use LinkedDataSignature2015).

The private key used for signing must be maintained in a secure repository and should be transferred only via secure channels. During application usage the keys should be maintained in the secure area such as an HSM. The data to be signed using the private key should be sent for signing and the signed value returned.


## Usage


### **Delivery and Storage of Credentials**

Delivery mechanisms for credential documents can vary based on the context where they are awarded. A certificate for an online course may be awarded immediately in the browser, while an offline course with written exams may have an alternate method to deliver certificates. Furthermore, these mechanisms are dynamic and change over time. New modes of delivery may be developed and present methods may become obsolete. Similar considerations apply to the means of storing the certificate; the recipient may choose from multiple options available for securely storing the digital document.

To empower recipients with a choice of delivery and storage mechanisms and to ensure compatibility with future methods, delivery and storage is independent of the data in the credential. Thus we may use any means to identify the recipient of the credential and independently choose the way it is delivered and stored. Below we consider some well-established delivery and storage options as well as a few emerging technology options such as Blockcerts and uPort.


#### **Email**

One mode of delivery may be email. If the recipient's email address is known, and the recipient elects for email delivery, the certificate can be sent to the recipient's email address as an attachment. The recipient is then free to store using any solution available such as a cloud drive, offline storage etc.


#### **Web**

An alternate mode of delivery can be via a private URL which allows the recipient to download the JSON-LD credential. The recipient is then free to store using any solution available such as a cloud drive, thumb drive, offline storage etc. The private URL can be sent to the recipient via an SMS message to a mobile device, an email or any other communication channel available to the awarding body and the recipient.


#### **DigiLocker and other National Repositories**

Certificates can be stored in the cloud using services such as India's DigiLocker or any other National Academic Repositories. The machine-readable format has a printable representation embedded in it which can be used by client applications to render previews of the credential.


#### **Blockchain**

Blockchain applications may also be used to deliver the certificate to the recipient. The awarding body can use a blockchain certificate publishing protocol such as Blockcerts which is also compatible with OpenBadges to store certificates on a blockchain as part of transaction metadata. Recipients can then retrieve the certificate from the blockchain and store as per their choice.


#### **Wallet**

Application developers can create mobile wallets for storing credentials. The JSON-LD document containing the certificate can be imported into any number of such applications to manage accomplishments and credentials. The embedded printable representation may be used by wallet applications to render previews of the credential.


#### **uPort**

uPort is a toolkit for building distributed applications on top of the Ethereum blockchain. uPort applications can issue credentials to a user which are then attached to the user's profile. The certificate spec described above can be linked into a uPort message which is transported a JSON Web Token (JWT). The JWT contains signed-data as a **<code>claim</code></strong> which can be the assertion JSON object.


### **Verifying Authenticity of a Certificate**

A certificate is authenticated along three dimensions.

First, verify that the certificate has been awarded by the awarding body.



1. The certificate contains one or more signatures in the signature field. The signature should be encrypted using the awarding body's private key.
2. Decrypt the signature using the awarding body's public key which returns the digest of the message.
    1. The awarding body's public key details are available in **<code>badge.awardedBy.publicKey</code></strong>
3. The digest of the message is computed and compared with the decrypted digest.  
4. If the two digests match, the signature is verified.
5. The specifics of the signature verification algorithm are described at:[ https://w3c-dvcg.github.io/ld-signatures/#signature-verification-algorithm](https://w3c-dvcg.github.io/ld-signatures/#signature-verification-algorithm)

Second, verify that the certificate is optionally digitally signed by the signatory



1. The certificate may also contain the signatory's digital signature in the signature field. The signature is encrypted using the signatory's private key.
2. The signature can be verified as above using **<code>assertion.signatory.publicKey</code></strong>

Finally, if the certificate contains signed evidence, verify the assessor's signature in each item of evidence in certificate.



1. The credential contains one or more items of evidence which contain signatures in the **<code>evidence.signature</code></strong> field encrypted using the assessor's private key.
2. The signature can be verified as above using the assessor's public key available from <strong><code>evidence.assessedBy.publicKey</code></strong>
3. The subject of the evidence must be the same as the recipient of the certificate.

Note that when authenticating the physical certificate, downloading the machine readable version from the URL contained in it's QR code is a first step. If the URL resolution fails, it cannot be assumed that the certificate is invalid, the URL may be unavailable for many reasons. In this scenario, the authenticity of the physical certificate must be verified via other means.


#### **Key Management**

Public keys for the awarding bodies could be cloud-hosted by each signing body. For instance, each Sector Skill Council (SSC) could maintain its own public keys in the cloud where they can be accessed by anyone trying to verify a certificate awarded by the SSC. However, if signing keys are cloud-hosted and the cloud location is embedded inside the certificate then any change in the location of the key will invalidate certificates. Awarding bodies may or may not be able to maintain a permanent location for their keys metadata. This could be worked around by either employing a key broker service which enables keys to be discovered after an awarding body has changed its location or alternatively by a capable entity providing a secure repository of public keys for all awarding bodies as an ecosystem service.


# References



1. Project inCredible -[ https://github.com/sunbird-specs/inCredible](https://github.com/sunbird-specs/inCredible)
2. OpenBadges v2:[ https://www.imsglobal.org/sites/default/files/Badges/OBv2p0Final/](https://www.imsglobal.org/sites/default/files/Badges/OBv2p0Final/index.html)
    1. examples:[ https://www.imsglobal.org/sites/default/files/Badges/OBv2p0Final/examples/](https://www.imsglobal.org/sites/default/files/Badges/OBv2p0Final/examples/)
3. JSON-LD Syntax:[ https://w3c.github.io/json-ld-syntax/#introduction](https://w3c.github.io/json-ld-syntax/#introduction)
4. JSON-LD:[ https://www.w3.org/TR/json-ld/](https://www.w3.org/TR/json-ld/)
5. RDF:[ https://www.w3.org/RDF/](https://www.w3.org/RDF/)
6. RDF Schema:  [https://www.w3.org/TR/rdf-schema](https://www.w3.org/TR/rdf-schema)
7. RDFa:[ https://www.w3.org/TR/rdfa-primer/](https://www.w3.org/TR/rdfa-primer/)
8. Turtle:[ https://www.w3.org/TR/turtle/](https://www.w3.org/TR/turtle/)
9. Uniform Resource Names:[ https://tools.ietf.org/html/rfc8141](https://tools.ietf.org/html/rfc8141)
10. The Tag URI scheme:[ https://tools.ietf.org/html/rfc4151](https://tools.ietf.org/html/rfc4151)
11. Schema.org Full Vocabulary:[ https://schema.org/docs/full.html](https://schema.org/docs/full.html)
12. Use of '@id' vs 'identifier':[ https://schema.org/docs/datamodel.html#identifierBg](https://schema.org/docs/datamodel.html#identifierBg)
13. Linked Data Signatures:[ https://w3c-dvcg.github.io/ld-signatures/](https://w3c-dvcg.github.io/ld-signatures/)
14. Rsa Signature Suite 2018:[ https://w3c-dvcg.github.io/lds-rsa2018/](https://w3c-dvcg.github.io/lds-rsa2018/)
15. Digilocker:[ https://digilocker.gov.in/](https://digilocker.gov.in/)
16. National Academic Depository:[ http://nad.gov.in/](http://nad.gov.in/)
17. Blockcerts:[ https://www.blockcerts.org](https://www.blockcerts.org)
18. uPort application development kit:[ https://www.uport.me/](https://www.uport.me/)
19. Linked Data Platform:[ https://www.w3.org/TR/ldp/](https://www.w3.org/TR/ldp/)
20. Architecture of the Web:[ https://www.w3.org/TR/webarch](https://www.w3.org/TR/webarch)
21. Web Payments Vocabulary: [https://web-payments.org/vocabs/security](https://web-payments.org/vocabs/security)





