## Object Model

Objects and the properties as defined by this credentials specification are detailed here.

## Contents
{:toc}

### Credential

The base of the model is a Credential. The Credential class is an alias for the 
[Assertion](https://www.imsglobal.org/sites/default/files/Badges/OBv2p0Final/index.html#Assertion) class defined as part of the 
[OpenBadges v2.0](https://openbadgespec.org) specification. Some additional properties are added via `CertificateExtension.`

*   `Id` which uniquely identifies the assertion. If assertions are verified by signing, a UUID should be used from the 
`urn:uuid` namespace. If hosted verification is used, the Id should be a HTTP URL to a JSON-LD document containing the 
certificate data.
*   `Type` An array containing the strings Assertion, Extension and `CertificateExtension`
*   `AwardedOn` when the credential was awarded
*   `Recipient`(s) person(s) or organisation(s) who received the credential. 
    *   If the certificate contains signed evidence, the subject of the evidence can be assigned a relative IRI as an `@id` 
    and referenced as the recipient of the certificate.
        *   `"recipient": {"@id": "#/evidence/0/subject"}`
    *   If there are multiple recipients, the element should be a list of entities
*   `Badge` an embedded BadgeClass object which describes the type of certificate being awarded or a HTTP URL which contains a 
machine-readable representation of a BadgeClass
*   optional `Image` which is a HTTP URL to a <em>baked</em>[^5] PNG or SVG image
*   `Evidence` containing details of competencies assessed
*   optional `Expires` containing the date the certificate ends validity
*   `Verification` containing the property `LinkedDataSignature2015` for signed certificates
*   `Narrative` as text or markdown text which can be used to describe and connect multiple pieces of evidence


### CertificateExtension

The `Assertion` type from OpenBadges is extended by the `CertificateExtension` which adds the following field definitions.

*   optional `AwardedThrough` service or program through which the credential is awarded (eg: PMKVY)[^6]
*   optional list of `Signatory`(s) who signed the certificate
*   `PrintUri` a HTTP URL which points to a printable version of the certificate 
    *   For instance, this may be the digilocker URL where the certificate HTML is stored.
    *   The printable version of the certificate can be embedded into the machine-readable data using data URIs. The encoding 
    scheme is: `data:[mime-type][;base64],<base64-encoded-data>`
        *   A base64 encoded PDF document could be represented as a data URI: `data:application/pdf;base64,<base64 encoded binary PDF>`
        *   A base64 encoded image document can be represented as a data URI: `data:image/jpeg;base64,<base64 encoded binary JPG>`
    *   If there are multiple printable documents to be embedded, a list of URIs can be added.
*   optional `ValidFrom` containing the date the certificate begins validity[^7]
*   `Signature` added by the awarding body using its private key for signed verification


### CompositeIdentity

OpenBadges v2 uses IdentityObjects to represent the recipient of a certificate. We extend it to represent a composite identity 
which is composed of a sub `IdentityObject`(s). 

To facilitate composite identities, the specification introduces: 

*   a new `IdentityObject` `@type` identifier called `composite`
*   a new property `annotation` which can be used to qualify the identity type
*   a new property `components` for composite identities. This property will contain sub-fields of the identity

The fields of a composite `IdentityObject` will be
*   `Type` will be Composite
*   `Hashed` will be false
*   `Identity` will be omitted
*   `Components` will be an array of other `IdentityObjects`

Additionally, we define the following `IdentityObject` `@type` identifiers to extend the set of  profile identifier properties
defined by OpenBadges.

*   `composite`: the identity is expressed as a composite identity containing `components`
*   `name`: the identity is expressed as a name, often used in conjunction with `annotation `to represent a father's or a spouse's name. 
May be part of a composite identity
*   `photo`: the identity is expressed as a photo, either a HTTP URL for a image or a data URI containing the mime type and image data in 
base64 encoding. May be part of a composite identity
*   `dob`: the identity is expressed as the date of birth in YYYY-MM-DD format. May be part of a composite identity
*   `gender`: the identity is expressed as the gender of the individual. May be part of a composite identity.
*   `tag`: the identity is expressed as a Tag URI
*   `urn`: the identity is expressed as a Uniform Resource Name (urn) URI
*   `url`: the identity is expressed as a Universal Resource Location (url) URI which may be dereferenced 


### BadgeClass

*   `Id` which uniquely identifies the `BadgeClass`
*   If the credential is an instance of a larger category of certificates which may be awarded multiple times, it must be a HTTP URL 
where the JSON-LD description of the `BadgeClass` is available.
*   If the certificate is ad-hoc or short-lived and unlikely to be awarded repeatedly, a `urn:uuid` class identifier can be used
*   `Type` will be the string BadgeClass
*   `Name` The name of the credential represented by this `BadgeClass`
*   optional `Description` A short text description of the credential
*   optional `Version` describing the version of the `BadgeClass`, which can be updated as the credentials evolve over time.
*   optional `Image` an image representing the credential, may be a HTTP URL where the image can be found or a data URI including 
mime-type
*   optional `Criteria` an embedded object describing the criteria for achieving the credential or a HTTP URL of a JSON-LD object 
describing the criteria 
*   `AwardedBy` AwardingBody profile of person or organisation entity which awarded the credential. It is recommended that the 
complete JSON-LD object representing the awarding body is embedded into the BadgeClass. The set of fields to uniquely identify the 
awarding body and to verify the awarding body's signature on the credential <em>must</em> be embedded into the certificate. If the 
complete awarding body profile is not embedded into the BadgeClass, then the `@id` of the embedded object must be a HTTP URL from 
which a more complete JSON-LD object can be retrieved. 
*   optional `Alignment` which maps the `BadgeClass` to one or more academic standards.
*   optional `Related` an object or list of objects relating this `BadgeClass` to other `BadgeClasses`.
    *   If the `BadgeClass` is part of a series, for instance if a new class is created for each batch or semester, this may be 
    used to link to previous instances of the same class.


### Profile: AwardingBody/Assessor/Trainer

*   `Id` to identify the awarding body. Should be a HTTP URL where a JSON-LD object describing the awarding body can be retrieved.
*   `Type` will be `Profile`. If the profile is for an entity which will be providing digital signatures it should be an array 
containing `Profile` along with `Extension` and `SignatoryExtension`.
*   `Name` the name by which the awarding body is known
*   optional `Email` containing the address where this awarding body can be reached
*   optional `URL` pointing to a HTTP accessible profile page or homepage of the awarding body
*   optional `Description` short text describing the issuing person or organisation
*   `PublicKey` containing the public key of the awarding body/Assessor/Trainer which must be embedded inside the assertion if 
the credential is signed.
*   optional `RevocationList` containing a HTTP URL of the list of signed badges awarded by this body which have been revoked


### AlignmentObject

The OpenBadges v2 `AlignmentObject` is used to link a `BadgeClass` or an item of `Evidence` to an academic standard.

*   `targetName` which identifies the name of target standard
*   `targetUrl` a HTTP endpoint which uniquely identifies the standard where a description of the standard can be found. 
Ideally should be a JSON-LD object describing the standard.
*   `targetFramework` a string describing the name of the standards framework
*   `targetCode` a string containing a code within target framework for the aligned standard


### Evidence

The `Evidence` class from OpenBadges v2 spec is used to describe evidence in support of a credential.

*   `Id `which uniquely identifies the evidence from the `urn:uuid` namespace or a HTTP URL of a webpage which presents the evidence
*   `Type` containing the string Evidence. Additional types Extension and `AssessedEvidence` will be added when using `AssessedEvidence`
*   optional textual `Narrative` which describes the evidence
*   optional text `Name` of the evidence
*   optional longer text `Description` of the evidence
*   optional text `Genre` which describes the type of evidence, such as Certificate, Painting, Artefact, Medal, Video, Image. May be 
omitted in favour of the `assessment` property in the context of `AssessedEvidence`
*   optional text `Audience` detailing the audience for which the evidence is presented
*   optional `Alignment` containing details of alignment to educational standards.


### TrainingEvidence

The `TrainingEvidence` class is used to add training specific properties to an item of `Evidence.`

*   `Type` should an array containing `Evidence,` `Extension`, `TrainingEvidence`
*   `Subject`(s) the subject(s) of the evidence -- should be an `IdentityObject`
*   `TrainedBy(s)` HTTP URL identifier to a JSON-LD object or an embedded profile of the person or organisation entity(s) which provided 
training to the recipient of the credential. The `@id` of the profile should either be a URI which uniquely identifies the training 
entity or should be a HTTP URL from which a more complete JSON-LD object can be retrieved 
*   optional `Duration` containing `startDate` and `endDate` specifying the duration of the course
*   optional `Session` containing a string which describes which session of the course the recipient completed


### AssessedEvidence

The `AssessedEvidence` class is an extension to the evidence class which adds additional fields for assessors and signatures.

*   `Type` should an array containing `Evidence, Extension`, `AssessedEvidence`
*   `Subject`(s) the subject(s) of the evidence 
*   `Assessment` conducted which elicited the evidence
*   `AssessedBy` HTTP URL identifier to a JSON-LD object or an embedded profile of the individual(s) or organisation(s) who assessed the 
competency. The `@id` of the profile should either be a URI which uniquely identifies the training entity or should be a HTTP URL from 
which a more complete JSON-LD object can be retrieved
*   `AssessedOn` the date when the assessment was conducted
*   optional `Signature` of the assessor(s)

If assessors are not ready and able to submit individually signed evidence, the assessor's signature on the `AssessedEvidence` may be 
omitted. It is then the responsibility of the awarding body to ensure the authenticity of the evidence submitted by the assessor 
through other available channels. Over time, migrating the assessment ecosystem to standardise on individually signed items of evidence
will increase the overall level of trust in the certification process and will increase the utility of certificates in the employment 
process.


### Assessment

`Assessments` can vary based on the nature of the assessment carried out. The essential fields of an assessment are
*   `Type` of the assessment will be `marks`, `percentage`, `grade`, `rank` or some other means of assessing the subject
*   `Value` of the assessment based on the type indicated.

Specific types of assessments may add additional properties to the Assessment object. Each new property must be published via JSON-LD 
documents which describe the schema and means of validation for the property. 


#### MarksAssessment

To illustrate, a _schema for a marks-based assessment_ which adds additional properties to the Assessment schema is described:

*   `MinValue` The minimum score which could have been achieved
*   `MaxValue` The maximum score which could have been achieved
*   `PassValue` The passing score for the assessment


### SignatoryExtension

`SignatoryExtension` extends the OpenBadges v2 `IdentityObject` to add the following properties.

*   optional `Designation` of the signatory
*   optional `Image` containing a HTTP URL or a data URI for an image associated with the signatory
*   optional `PublicKey` object containing the public key of the signatory as defined by the LinkedDataSignatures specification[^8]. 
Required if the signatory will affix their digital signature to the credential.


## Additional Properties

Since the objects are modeled using RDF principles, additional properties may be added to the objects without affecting consumers. 
All properties and metadata not defined here which are used as extensions to the credential specification must follow or be compatible 
with the metadata standards defined by [egovstandards.gov.in](http://egovstandards.gov.in/).

*   All consumers of credential data must be able to accept objects containing additional properties beyond the ones described as part 
of the credentials standard. 
*   RDF properties define a set of classes which are in the domain of a property[^9]. When adding a new property to an object, the 
appropriate domain class must be included in the `@type` array.


<!-- Footnotes themselves at the bottom. -->
## Notes

[^1]: See the section on Identifier Namespaces

[^2]: The 'tag' URI scheme, https://tools.ietf.org/html/rfc4151

[^3]: https://www.w3.org/TR/owl-ref/#sameAs-def

[^4]: The registration date should be the date the domain was first registered by an entity in an unbroken spell to the present date.

[^5]: See the OpenBadges baking specification:
[https://www.imsglobal.org/sites/default/files/Badges/OBv2p0Final/baking/index.html](https://www.imsglobal.org/sites/default/files/Badges/OBv2p0Final/baking/index.html)

[^6]: https://schema.org/issuedThrough

[^7]: https://schema.org/validFrom

[^8]: https://w3c-dvcg.github.io/ld-signatures/#linked-data-signature-overview

[^9]: https://www.w3.org/TR/rdf-schema/#ch_properties
