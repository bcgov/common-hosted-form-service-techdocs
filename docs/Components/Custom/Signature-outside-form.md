[Home](index) > [Components](Components) > [Custom](Custom) > **Handling Signature Outside CHEFS**
***

## Examples

> Try a working example<br>
> [View example](https://submit.digital.gov.bc.ca/app/form/submit?f=fb3cdf23-4d83-4f94-80f4-78cea5e907cd)

> Download this example file and [import](Importing-and-exporting-form-designs) it into your design<br>
> [Digital Signature - Non-DisClosure Agreement](../examples/example_digital_signature_non_disclosure_agreement_schema.json){:download="example_digital_signature_non_disclosure_agreement_schema.json"}

***

## Working with the Signature Component

The [Signature](Advanced-Fields.md#Signature) component allows the end-user to digitally sign a signature pad with either their finger on a touch-enabled device or with the mouse pointer. In this atricle we will talk about how the discuss how to use the Signature outside a CHEFS Form submission view. 

### Using the Signature Component with CDOGS (Common Document Generation Service)
CDOGS supports multiple template formats, including HTML, DOCX, and Excel. To include a signature in your generated document, you need to prepare a template with placeholders for the signature and ensure that the placeholders map correctly to your input data.

For more details on creating CDOGS templates, refer to the [Guide to CDOGS](CDOGS-Template-Upload).

We will use the form [Digital Signature - Non-DisClosure Agreement](https://submit.digital.gov.bc.ca/app/form/submit?f=fb3cdf23-4d83-4f94-80f4-78cea5e907cd) as a reference. This form uses signature components alongside other fields like names, dates, and contact information. The HTML <img> tag is used to render the signature in an image format using Base64-encoded strings. Following shows how signature can be used in CDOGS template.

```
    <p>
        Signature: <img src="{d.simplesignatureadvanced}" alt="Disclosing Party Signature" style="max-width: 300px;">
    </p>
```

- `{d.simplesignatureadvanced}` This placeholder will be replaced with the Base64-encoded string of the signature image. The src attribute is dynamically populated with the Base64 string. The alt attribute provides a description for accessibility.

Refer to this example of how to include a signature as a CDOGS attribute in an HTML template - [Digital Signature - Non-DisClosure Agreement CDOGS template](../examples/example_digital_signature_non_disclosure_agreement_CDOGS_template.html){:download="example_digital_signature_non_disclosure_agreement_CDOGS_template.html"}

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)