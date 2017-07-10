# HOF: Helping to improve Accessibility

HOF is a framework designed to assist developers in creating form-based applications in a rapid, repeatable and secure way. It was developed with accessibility in mind. This means that when you build a form in HOF you get a set of accessibility patterns for free out of the box. You can [find out more about HOF](https://github.com/UKHomeOfficeForms/hof). In this post I will briefly explain how HOF helps developers and designers to improve accessibility and provide simple examples.

## Label controls

In HOF labels are associated to their corresponding form elements in all form controls such as text fields, checkboxes, radio buttons etc. Web Content Accessibility Guideline (WCAG) recommend this approach. It means labels are presented as a large clickable area to activate a control. This aids those with motor disabilities. It also ensures that assistive technology such as screen readers are able to refer to the correct label when presenting a form control.

It’s easy to add an input text in HOF:
```
{{#input-text}}registeredTravellerNumber{{/input-text}}
'registeredTravellerNumber': { label: ‘Registered Traveller Number’,}
```
HOF will convert the configuration into HTML like so:
```
<label for="registeredTravellerNumber">
        Registered Traveller Number
</label>
<input type="text" name="registeredTravellerNumber" id="registeredTravellerNumber">
```

![Example of HOF input box](../images/input-box.png)

Note: the matching ‘for’ and ‘id’ ensures that the text and form controls are explicitly linked.  As per the screenshot, when the user clicks the label ‘Registered Traveller Number”, the input text is selected as per WCAG and GDS guidelines.

## ARIA attributes

Accessible Rich Internet Applications (ARIA) attributes are used by assistive technology such as screen readers to describe content. They are especially useful for dynamic content on a website.  For example, if JavaScript is used to change a display on a website, a screen reader will use the ARIA attribute to describe the change to the user.

HOF comes with various aria-attributes out of the box. Attributes such as aria-expanded, aria-controls, aria-required and many others are all included.  For aria-required, WCAG explain that “using the aria-required attribute allows the author to explicitly convey to assistive technologies that a user must complete this field element.”

In HOF, you can easily set a valuation rule to ensure a user fills out a form-control.  If a user doesn’t fill out a part of a form, a message appears highlighting this part of the form is required.  HOF will also automatically generate the aria required attribute.

Before HOF a developer would have to do this manually typically with a bit of JavaScript, CSS and HTML.  The following configuration now demonstrates how simple it is using HOF: 

Example HOF code:  
```
'registeredTravellerNumber': {validate: ['required']}
```
The HTML output will be `aria-required="true"`


## Radio buttons and fieldsets

A common mistake when developing radio buttons is to omit a fieldset or/and a legend. Fieldsets are used to group radio buttons together. Screen readers read the legend element content when one of the radio buttons receives a keyboard focus. This is to provide context to the user. HOF prevents such mistakes

Example HOF code: 
```
{{#radio-group}}immigration{{/radio-group}}
'immigration': { options: [{value: 'Yes', label: 'Yes'}, {value: 'No',label: 'No'}]}
"immigration": { "legend": "Has your immigration status changed?"}
```

The HTML output will be 
```
<fieldset id="immigration-group">
    <legend> Has your immigration status changed?</span>
    </legend>
        <label class="block-label" for="immigration-Yes">
            <input type="radio" name="immigration" id="immigration-Yes" value="Yes" aria-required="true">
            Yes
        </label>
        <label class="block-label" for="immigration-No">
            <input type="radio" name="immigration" id="immigration-No" value="No" aria-required="true">
            No
        </label>
</fieldset>
```

# HOF Benefits

More and more teams are using HOF to deliver services. They are contributing to improving the framework, providing new features and improving areas around accessibility.

By using HOF, we can ensure that some fundamental elements of accessibility are always included. It prevents two common pitfalls (1) developers not being aware of these accessibility features (2) developers forgetting to include them when creating a form.

As a developer, I can testify to being guilty on both such scenarios. I can also attest to great improvements in accessibility as we move Registered Traveller and Global Entry to use HOF.  We’ve fixed various accessibility issues across our forms and have also tested the experience by using a screenreader on the old service and comparing it against the new HOF version. The HOF version trumps the previous versions in all areas.

Overall, HOF makes it easier to create forms. Crucially, HOF makes the forms more accessible!
