## Data Model

## Contents
{:.no_toc}
* Contents
{:toc}

### Open Standards

The credentials data model uses the following standards for defining a credential:

*   Alignment with OpenBadges v2 vocabulary for defining accomplishments. The OpenBadges vocabulary is extended in some areas for 
specific use cases.
*   RDF 1.1 (Resource Description Framework) is used as the means for expressing the data contained in a credential.
*   The preferred RDF serialisation format is JSON-LD, however, consumers of a credential are free to use alternative serialisation 
formats such as RDFs or a triple expression language such as Turtle.
*   The credentials model uses (and in some places extends) the vocabulary of Classes and Properties described by schema.org and the 
WebPayments specification.
*   Additionally the credentials model defines some new classes of objects.
*   Each object class used in the model must be defined in terms of an RDF schema. Under the JSON-LD serialisation format, the schema 
needs to be published and made available at a specific web URL for validation and consumption of credentials (a hypothetical schema 
URL is used in the example below).


### Identifiers

Based on the above principles for identifying entities using strong identifiers the following apply when assigning identifiers for
objects.

*   Use URIs wherever possible for compatibility with web protocols
*   Since we represent data in JSON-LD, the preferred URI for an entity is a dereferenceable URL which points to the location where
the entity's JSON-LD representation can be found
*   If a URL is unavailable, use a URN. The id must be created within a well-known namespace with an established namespace identifier
(NID)[^1]
    *   URN: **`urn:{namespace-id}:{private-id}`**
*   If an established NID is unavailable to create a URN, the TAG URI scheme[^2] can be used when there is a web domain name for the 
creator of the ID.
    *   TAG:**`tag:{creator-domain},{domain-register-date}:{id-type}:{id}`**
*   Where URNs and TAGs cannot be derived, strong globally unique identifiers should be created via locally unique identifiers using 
`IdentityObject` where the `@type` is a namespace describing the type of identifier and the identity is the local ID (see an example 
in the certificate below).
    *   `@type` should be a string which contains two parts separated by a delimeter, the first part must be a well-known id for the
    creator of the local identifier, the second part can be any string which describes the id


#### Identifier Namespaces

Below, we propose some informal namespaces for commonly used identifiers types. These namespaces can be used as the NID for URNs. 
The format used for NIDs is **`in.<domain>.<id-creator>.<id-type>`**, where domains are .gov, .edu, .com & .org. 
This format can be used to construct new informal namespaces for NIDs.

Non-unique namespaces cannot be used as NIDs for URNs but may be utilised as the **`@type`** property for a 
component of a composite identity represented by an **`IdentityObject`**.

<table>
  <tr>
   <td><strong>Identifier Type</strong></td>
   <td><strong>Namespace</strong></td>
   <td><strong>Example</strong></td>
  </tr>
  <tr>
   <td>PAN</td>
   <td><code>in.gov.itd.pan</code></td>
   <td><code>urn:in.gov.itd.pan:ZZZZZ00000</code></td>
  </tr>
  <tr>
   <td>GSTN</td>
   <td><code>in.gov.gstn.gstn</code></td>
   <td><code>urn:in.gov.gstn.gstn:Z00000000000001</code></td>
  </tr>
  <tr>
   <td>Driver License (KA)</td>
   <td><code>in.gov.ka-dot.dl</code></td>
   <td><code>urn:in.gov.ka-dot.dl:ZAAAAAAAAAAAAB</code></td>
  </tr>
  <tr>
   <td>Driver License (MH)</td>
   <td><code>in.gov.mh-dot.dl</code></td>
   <td><code>urn:in.gov.mh-dot.dl:ZOOOOOOOOOOOAB</code></td>
  </tr>
  <tr>
   <td>Aadhaar</td>
   <td><code>in.gov.uidai.aadhaar</code></td>
   <td><code>urn:in.gov.uidai.aadhaar:11111111111</code></td>
  </tr>
  <tr>
   <td>Voter Identity</td>
   <td><code>in.gov.eci.voterid</code></td>
   <td><code>urn:in.gov.eci.voterid:X11111111X</code></td>
  </tr>
  <tr>
   <td>Passport</td>
   <td><code>in.gov.mea.psprt</code></td>
   <td><code>urn:in.gov.mea.psprt:XX99999999</code></td>
  </tr>
  <tr>
   <td>Roll Number</td>
   <td><code>in.<dom>.<iss>.rollno</code></td>
   <td><code>urn:in.gov.msde-dgt.rollno:999999999</code></td>
  </tr>
  <tr>
   <td>Name</td>
   <td><code>name</code></td>
   <td><code>Ram Singh</code></td>
  </tr>
  <tr>
   <td>Date of Birth</td>
   <td><code>dob</code></td>
   <td><code>Date of birth in YYYY-MM-DD format`</code></td>
  </tr>
  <tr>
   <td>Photo</td>
   <td><code>photo`</td>
   <td><code>data:image/png;base64,<base64 encoded></code></td>
  </tr>
</table>

**Table 1**:  Informal namespaces for commonly used identifiers


#### URN Identifiers

URNs are URIs which follow the Universal Resource Name (URN) scheme. A URN consists of three parts separated by colons (:)

**urn**  :		**{nid}**  :		**{nss}**

* nid: namespace id	
* nss: namespace specific string

The namespace id (nid) defines the type of identifier. The consumer of a URN can make processing decisions based on the nid. The 
consumer could use the nid to determine how to resolve the namespace specific string to an entity. For instance, the isbn namespace 
is registered for ISBN book codes.

The namespace specific string (nss) is the value of the ID within the nid. Continuing the above example of books, the nss would be 
the ISBN of a specific book such as 8120351312. 

Together, the combination of **`urn:isbn:8120351312`** forms a URN which uniquely identifies a book.


#### Institution Ids

Institutions are identified in two scenarios. The first of these is an institution is an awarding body of credentials or is an assessor 
of a subject (recipient). In this scenario, the institution should be identified using a URL which points to the institution's profile 
(in JSON-LD format). The profile must contain the awarding body/assessor properties defined in the model below. Additionally, the 
profile may also contain more information about the institution (e.g. rankings, institutional standards, authorisations etc) using the 
appropriate RDF schemas. The profile may also contain links to other tools where such information about the institution can be retrieved.

Second, as the recipient of credentials, institutions should also be identified using a URL which points to the institution's profile. 
The profile data may contain embedded objects detailing publicly available and well-known identifier types such as a GST number or a 
permanent account number (PAN). The would be represented using the RDF **`sameAs`**^3] property whose value is an 
**`IdentityObject`**. When using such identifiers the identity can be represented as a URN.


#### Individual Ids

Individuals are identified in two scenarios. First as recipients of credentials and second, as signatories to a credential. In both 
scenarios, the individuals should be identified by an **`CompositeIdentityObject`** which contains one or more identifying
attributes. If the individual can be identified by a HTTP URL, the **`IdentityObject`** should be of **`@type: "url"`**. In case of 
an identity which is comprised of multiple parts, an **`IdentityObject`** of **`@type: "composite"`** should be used containing 
components which are in turn **`IdentityObjects`** of a variety of types. 

Typically, an individual is identified by a combination of name, date of birth, gender and photo. Aside from this, other attributes 
like the name of a relative or a masked unique identifier may also be used. Agencies are encouraged to support the use of multiple 
modes of identity which may be available to recipients. 

If using unique identifiers, agencies should evaluate privacy concerns which may stem from embedding a unique identifier into the 
credential. In such cases, a masked identifier may serve the purpose of identifying the individual without compromising privacy.
For example, if Aadhaar number is used, it should only show the last 4 digits of the Aadhaar number.


#### Object Ids

Machine-readable objects such as **`Assertions`**, **`BadgeClasses`** & **`Evidence`** should be identified for the purpose of 
validation and comparison. 

**Assertions & Evidence**

Ideally, Assertions and Evidence should be identified via a UUID encoded as a URN. 

Example: **`urn:uuid:ec58b28e-a6ab-49c2-a24d-ebefa02476cd`**

If use of a UUID is not feasible, for instance if documents are numbered serially, the TAG URI scheme should be used where a document 
id is prefixed with a namespace consisting of the document creator's domain name, its registration date[^4] and the document type.

Example:**`tag:exampleinstitute.org,2010-09:marksheet:9871624`**

**BadgeClass**

BadgeClasses should ideally be identified via a HTTP URL which returns a JSON-LD representation of the class. If the BadgeClass is 
defined for a single ad-hoc usage and is not published at a URL, a UUID encoded as a URN is recommended.  


