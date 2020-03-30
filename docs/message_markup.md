---
id: message_markup
title: Message Markup
sidebar_label: Message Markup
---

OpenDialog uses a custom XML style mark up language for describing message templates. The message mark up is platform agnostic meaning it will compile to the correct message format for all supported message platforms.
Not all message platforms support all message types, so in some cases the resulting message will differ between platforms. This page describes what is currently supported in the message template language with an example together with the resulting message on the webchat platform.

## Common to all messages

Each message template must be contained within a message block as follows:

```xml
<message>
</message>
```

### Disabling Text Input
The message element can optionally contain a `disable_text` property to turn off text responses from the user (for platforms that support this feature).

```xml
<message disable_text="1">
</message>
```
Example message with user text disabled and bot avatar turned off:
![Disable Text](assets/messages/disable-text.png "Disable Text")

### Disabling Bot Avatar
Another option on messages is to hide the bot avatar. When this is set on a message no bot avatar is shown, even if it is turn on in the webchat settings

```xml
<message disable_avatar="1">
</message>
```

## Supported Message Types

We currently support 12 message types in the message builder:

### Text Message

A plain message with only text. Specially formatted links can also be included in the text body 

```
<text-message>{message-text}</text-message>
```

Where message text can contain links in the following format:

```xml
<link new_tab="true|false">
    <url>{url}</url>
    <text>{text}</text>
</link>
```

There is no support at the moment for any other formatting such as bold, italics etc

Example text message
![Text Message](assets/messages/text-message.png "Text Message")

### Image Messages

Displays an image message. Optionally, the image can also be a link that can optionally open in a new tab if the `url` property is included.

```xml
<image-message>
    <src>{img_src}</src>
    <url new_tab="{true|false}">{url}</url>
</image-message>
```
![Image Message](assets/messages/image-message.png "Image Message")

### Button Messages

Button messages allow you to provide the user a number of options to select as a response. The basic mark up is:

```xml
<button-message>
	<text>{button message text}</text>
    <external>true|false</external>
    <clear_after_interaction>true|false</clear_after_interaction>
</button-message>
```

Setting the `external` property to true results in a the message buttons appearing outside of the button message (this defaults to false if not set)

Setting the `clear_after_interaction` property to false means that the buttons will remain visible to the user after being interacted with

#### Buttons
A button message can contain 1 or more buttons for the user to interact with (some platforms have different restrictions on the number of buttons per message)
Each button must define a `text` element to specify the text that should be shown to the user.

OpenDialog has built in support for 4 types of message:

##### Callback buttons

Callback buttons will send  a `callback_id` (and optionally a `value`) when interacted with by the user that will move the conversation forward.
Make sure that any `callback_id` you use in a button response is mapped to an intent in the interpreter engine config!

```xml
    <button>
        <text>Callback Button</text>
        <callback>callback id</callback>
        <value>attribute_name.attribute_value</value>
    </button>
```

Values can be optionally set on callback buttons to add some extra context to the button response. The format of button values is:

        attribute_name.attribute_value
        
where `attribute_name` should be the ID of an attribute that has already been defined in the system.

When passing through the Callback Interpreter, button values will be parsed and an attribute will be returned with the value set as per the button value

##### Link buttons

Links buttons are used to create links to other web pages. The `link_new_tab` element can be set to true to force the links to open in a new tab. If not set, links default to opening in the same tab

```xml
    <button>
        <text>Link Button</text>
        <link>http://example.com</link>
        <link_new_tab>true|false</link_new_tab>
    </button>
```

##### Click to Call buttons

Click to call buttons are used to create buttons for telephone numbers. They created a standard format `tel:` link that depending on the user's current device and platform will start a phone call to the number given 

```xml
    <button>
        <text>CLick to Call</text>
        <click_to_call>02079460000</click_to_call>
    </button>
```

##### Tab Switch buttons

Tab Switch buttons should only be used for the OD Webchat platform in conjunction with comments and indicates that the button should switch the user to the 'comments' tab

```xml
<button>
   <text>Tab Switch</text> 
   <tab_switch>true</tab_switch>
</button>
```
Example button message
![Button Message](assets/messages/button-message.png "Button Message")

### Rich messages

Rich messages allow for more control around message content and how it is displayed to the user. They can be thought of like 'card' style messages and contain any of the following elements in combination:

* Title
* Subtitle
* Text
* Image
* Buttons

Where buttons can be any of the buttons described above. 

```xml
<rich-message>
    <title>Title</title>
    <subtitle>Subtitle</subtitle>
    <text>Text</text>
    <image>
        <src>image_src</src>
        <url new_tab="true|false">www.example.com</url>
    </image>
</rich-message>
```

### Form messages

Form messages allow for user to input data in standard web form rather than text entry. When submitted, the values of the entered by the user are sent back along with the defined `callback` 
All form messages must contain the following elements:

```xml
    <form-message>
       <text>Text</text>
       <submit_text>Submit Text</submit_text>
       <callback>Callback</callback>
       <auto_submit>true|false</auto_submit>
    </form-message>
```

Here, the `text` value is shown at the top of the form message and the `submit_text` value is shown on the form submit button.
When `auto_submit` is set to true, the form will automatically be submitted when the user selects a value. This works best when just 1 element is added to the form
 
Optionally, the form message can contain a cancel button. This allows the user to tell the bot they do not want to submit the form. When clicked, the value of `cancel_callback` is sent. The cancel button can be added to a form message with the following mark up:

```xml
<form-message>
    <cancel_text>Text</cancel_text>
    <cancel_callback>Callback</cancel_callback>
</form-message>
```  

#### Elements

Form messages have support for a number of different elements (matching what is possible in a standard HTML form). All elements are defined in the same way, and there is no limit to how many can appear on a form message.

Each element must define a `type` and `display`, and can optionally define `required` and `default_value`. If required is set to true, the form cannot be submitted unless the field has a value.

```xml
<element>
    <element_type>textarea|text|number|email|select|auto_complete_select|radio</element_type>
    <display>Display Name</display>
    <required>true|false</required>
    <default_value>Default Value</default_value>
</element>
```

When using `radio` or `select` elements, you must define an `options` block giving the options to be presented in the radio list or select element:

```xml
<element>
    <options>
      <option>
        <key>Key</key>
        <value>Value</value>
      </option>
    </options>
</element>
```

The `email` element type acts just like a `text` element, but on submission, is validated to ensure it is formatted like an email address

![Form Message](assets/messages/form-message.png "Form Message")

This form message example was created with the following XML:
```xml
<message>
    <form-message>
        <text>Text</text>
        <submit_text>Submit Text</submit_text>
        <callback>Callback</callback>
        <auto_submit>false</auto_submit>

        <element>
            <element_type>select</element_type>
            <name>title</name>
            <display>Title</display>
            <options>
                <option>
                    <key>mr</key>
                    <value>Mr.</value>
                </option>
                <option>
                    <key>mrs</key>
                    <value>Mrs.</value>
                </option>
                <option>
                    <key>other</key>
                    <value>Other</value>
                </option>
            </options>
        </element>

        <element>
            <element_type>text</element_type>
            <name>name</name>
            <display>Name</display>
        </element>

    </form-message>
</message>
```

### Empty Messages

This is needed so an intent can have a matching template that doesn't result in a message being sent to the user. This may not be supported on all platforms.
Empty messages can be useful to add to intents that we want to match for a user, but only send a message if certain conditions are met - for example using the standard `intent.core.welcome` to only send a message if the user was seen more than 

```xml
<empty-message/>
```

### List messages

List messages allow for multiple messages be be combined into a single message for the user that is displayed as a carousel that users can scroll between. These are good for displaying multiple search results or related items.

List messages work well together with rich messages, but can be used as a wrapper for any messages types.

The only option available for list messages is `view-type`. This can either be `vertical` (default) or `horizontal`

Note - messages with very different sizes may not display well in a horizontal carousel

```xml
<list-message list_type="horizontal">
    <text-message>{text_message}</text-message>
    <image-message>{image_message}</image-message>
    <rich-message>{rich_message}</rich-message>
</list-message>
```

![List Message](assets/messages/list-message.png "List Message")

### Full page messages

Rich and Form messages can also be presented as 'full page' messages. When full page messages are received, they will take over the entire chatbot screen (depending on what is supported by each platform). For webchat full page messages, the user input is also taken over.

#### Long Text messages

These messages are for a special case where a user is expected to enter more long form text and gives a larger space to do this.
In the case of OD webchat, a Long Text message will hide the current message list and display a large input space with the message text displayed above.

On submission, the user's input is sent as text along with the defined `callback`

Long text messages also allow for custom submit button text, confirmation text that is displayed to the user after submission and an optional character limit to limit what the user can enter

```xml
<long-text-message>
    <submit_text>Submit Text</submit_text>
    <callback>callback</callback>
    <initial_text>$this->initialText</initial_text>
    <placeholder>$this->placeholder</placeholder>
    <confirmation_text>$this->confirmationText</confirmation_text>
    <character_limit>$this->characterLimit</character_limit>
</long-text-message>
```

![Longtext Message](assets/messages/longtext-message.png "Longtext Message")

#### Full Page Rich messages

Full page rich messages are defined in exactly the same way as standard rich messages, but can optionally define a cancel button to allow the user to move on without interacting.

```xml
<fp-rich-message>
    <title>Title</title>
    <subtitle>Subtitle</subtitle>
    <text>Text</text>
    <image>
        <src>image_src</src>
        <url new_tab="true|false">www.example.com</url>
    </image>
    <cancel_text>Text</cancel_text>
    <cancel_callback>callback</cancel_callback>
</fp-rich-message>
```

#### Full Page Form messages

Full Page Form messages are defined in exactly the same way as form messages, but with a different element name:

```xml
    <fp-form-message>
       <text>Text</text>
       <submit_text>Submit Text</submit_text>
       <callback>Callback</callback>
       <auto_submit>true|false</auto_submit>
    </fp-form-message>    
```

### Special Messages

The messages below do not act like standard messages that appear in a message list and history, but perform 

### CTA messages

CTA messages are used to display content in the minimized chatbot and will only work with the OpenDialog webchat platform. Each time a CTA message is sent, the CTA text in the minimized chatbot header is updated. 

CTA messages can only contain text

```xml
<cta-messsage>
    {text}
</cta-messsaeg>
```

![CTA Message](assets/messages/cta-message.png "CTA Message")

### Hand to Human messages

Hand to human messages are intended to be used to inform OpenDialog that the handling of chat has been taken over by a live human. In OpenDialog webchat, this means that new messages sent by the user are not sent to the `incoming/webchat` endpoint, but are handled by an external system.

The hand to human process and how to handle this within OpenDialog is documented separately.

Hand to human messages contain a number of `data` elements that have a unique name specifying what they are for. This way, any custom data payload can bve sent with hand to human messages

```xml
<hand-to-human-message>
    <data name="{name_attribute}">{value}</data>
</hand-to-human-message>
```

## Example

This is an example messages template

```xml
<message disable_text="true">

    <text-message>

        Click the link

        <link new_tab="true">

            <url>www.opendialog.ai</url>

            <text>OpenDialog</text>

        </link>

    </text-message>

    <button-message>

        <text>Did you like that link?</text>

        <button>

            <text>Yes!</text>

            <callback>link_response</callback>

            <value>link_answer.yes</value>

        </button>

        <button>

            <text>No!</text>

            <callback>link_response</callback>

            <value>link_answer.no</value>

        </button>

    </button-message>

</message>

```

When rendered in the webchat widget, it would look like this:

![Example Message](assets/example_message_template.png "Example Message")