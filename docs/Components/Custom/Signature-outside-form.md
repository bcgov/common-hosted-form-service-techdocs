[Home](index) > [Components](Components) > [Custom](Custom) > **Handling Signature Outside CHEFS**
***

## Examples

> Try a working example  
> [View example](https://submit.digital.gov.bc.ca/app/form/submit?f=fb3cdf23-4d83-4f94-80f4-78cea5e907cd)

> Download and [import](Importing-and-exporting-form-designs) this example file into your form design  
> [Digital Signature - Non-Disclosure Agreement](../examples/example_digital_signature_non_disclosure_agreement_schema.json){:download="example_digital_signature_non_disclosure_agreement_schema.json"}

***

## Working with the Signature Component

The [Signature](Advanced-Fields.md#Signature) component allows end-users to digitally sign using either their finger on a touch-enabled device or a mouse pointer.

In this article, we'll discuss how to use the Signature component outside the standard CHEFS Form submission view.

---

### Using the Signature Component with CDOGS (Common Document Generation Service)

CDOGS supports multiple template formats, including **HTML**, **DOCX**, and **Excel**. To include a signature in your generated document:

1. Prepare a template with a placeholder for the signature.
2. Ensure that the placeholder maps correctly to the corresponding input data field.

Refer to the [Guide to CDOGS](CDOGS-Template-Upload) for help creating CDOGS templates.

We use the [Digital Signature - Non-Disclosure Agreement](https://submit.digital.gov.bc.ca/app/form/submit?f=fb3cdf23-4d83-4f94-80f4-78cea5e907cd) form as a reference. This form includes:
- A signature field
- Supporting fields such as name, date, and contact information

In the CDOGS HTML template, use the `<img>` tag to render the Base64-encoded signature image, like so:

```html
<p>
    Signature: <img src="{d.simplesignatureadvanced}" alt="Disclosing Party Signature" style="max-width: 300px;">
</p>
```

- `{d.simplesignatureadvanced}`: This placeholder will be replaced with the Base64-encoded string of the signature image.
- The `src` attribute is dynamically populated.
- The `alt` attribute provides a description for accessibility.

Download the template example here:  
[Digital Signature - Non-Disclosure Agreement CDOGS Template](../examples/example_digital_signature_non_disclosure_agreement_CDOGS_template.html){:download="example_digital_signature_non_disclosure_agreement_CDOGS_template.html"}

***

[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)