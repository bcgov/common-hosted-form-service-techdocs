[Home](index) > [Components](Components) > [Custom](Custom) > **Digital signature**
***

## What is purpose of digital signature

To reference the Govt of canada [article](https://www.canada.ca/en/government/system/digital-government/online-security-privacy/government-canada-guidance-using-electronic-signatures.html) the fundamental purpose of the signature links a person to a document (or transaction) and typically provides evidence of that person’s intent to approve or to be legally bound by its contents. The primary function of a signature is to provide evidence of the signatory’s:

- identity
- intent to sign
- agreement to be bound by the contents of the document

## Guidance on implementing good digital signature form

- The signer's identity must be verified.
- Disclosure and consent are required.
- The signer must be aware that the signature is legally binding.
- The document must be protected from tampering.
- All signers should have access to the document.
- All actions taken should be recorded.

## How can CHEFS help to meet requirements for digital signature?
- CHEFS providers [different types of authentication](https://developer.gov.bc.ca/docs/default/component/chefs-techdocs/Capabilities/Form-Management/Accessing-forms/) which helps verify the user's identity. Please refer to the instructions on setting up those authentication methods on your form and what they entail. Business BCeID or IDIR providers confirm verified identities.
- [Signature component](https://dev.developer.gov.bc.ca/docs/default/component/chefs-techdocs/Components/Form-Builder/Advanced-Fields/#signature), The advanced field of the CHEFS component can be utilized to accept and store signatures. Additionally, a text field can be added to record the full name along with the date and time for record-keeping purposes.
- the reason or context for the digital signature must is clear. Please leverage various [form builder](https://dev.developer.gov.bc.ca/docs/default/component/chefs-techdocs/Components/Form-Builder/) components to express the context for the digital signature. This will help clear that the individual(s) understand that they are signing the electronic data.
The reason or context for the digital signature must be clear. Use various [form builder](https://dev.developer.gov.bc.ca/docs/default/component/chefs-techdocs/Components/Form-Builder/) components to convey the context of the digital signature. This will ensure that individuals understand they are signing the electronic data.
- CHEFS stores all the form data with its supporting metadata, including:
    - The date and time when the electronic data was signed.
    - Evidence that the signature was valid at the time it was signed.
    - The ability to store the data securely to prevent tampering.



## Example
> This example demonstrates a sample form designed to collect information from a logged-in user. It illustrates how to provide a clear context for the information being gathered, obtain the user's consent, and capture their signature. The form ensures that the user understands the purpose of the data collection and agrees to the terms by providing their signature.  
> Try a working example<br>
> [View example](https://chefs-dev.apps.silver.devops.gov.bc.ca/app/form/submit?f=9c75749a-affe-41ee-ab11-ef66e89be9a2)

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)
