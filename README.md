# GDPR.txt

The GDPR.txt file is a proposed standard which informs hosting providers about
the personal data collected by softwares. **It aims to simplify the compliance
to the [General Data Protection Regulation](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
(<abbr>GDPR</abbr>) of hosting providers.** Note that a GDPR.txt file is not
enough to make your project <abbr>GDPR</abbr> compliant (but it will help).

A GDPR.txt file must be written and maintained by the developers of the
corresponding software. Hosting providers should use this file to create their
own records of processing activities.

The current document is intended to developers and hosting providers. It
describes the syntax of the GDPR.txt file and covers the principal questions
that you might have.

[GDPR.txt](https://github.com/flusio/gdpr-txt) is licensed under [CC BY-SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/?ref=chooser-v1).

_Disclaimer: the format has not been reviewed by any legal authority and it is
very new. Use it at your own risks._

## Format

A GDPR.txt file is a simple `key: value` system organized in blocks. A block
covers a purpose of processing, or a specific data. Each block is separated
from the others by a blank line.

There is an example [at the end of this document](#can-i-have-an-example).

### Purpose block

A purpose of processing tells the users why it is useful for your software to
collect data. For instance, you may ask an email address to notify users, or a
biography to customise a public profile. Note that purposes are not tied to any
specific data. In these examples, purposes could be: “Notify users about
mentions from other users” or “Customise public profiles”.

A GDPR.txt file MUST contain at least one purpose block, except if no data are
collected.

A purpose block has two required keys:

- `purpose`: a free string value used to describe the purpose of the data
  processing.
- `lawfulness`: a string value giving the legal basis for the processing. Its
  value MUST be one of the following: consent, contract, legal, public
  interest, legitimate interest, vital.

### Data block

It is important to list the data you’re collecting to inform the final users of
your software. You should list only personal data, but if you’re not sure if a
data is considered as personal, it’s better to list it anyway.

A GDPR.txt file CAN contain one or more data blocks.

A data block has 4 required and 1 optional keys:

- `data`: a free string value giving the name of the collected data.
- `required`: a boolean value (true or false) indicating if the data is
  required to use the software.
- `visibility`: a free string value indicating who can access the data (e.g.
  private, public, administrators).
- `description`: a free multiline string value describing how and why the data
  is used.
- `mitigation` (optional): a free multiline string value to detail the
  mechanisms that make data less vulnerable (e.g. data deleted after X days,
  pseudonym authorized).

### Comments

A GDPR.txt file can contain comments. A comment is a line starting by a `#`.

### Multilines

You may want to write data description and mitigation on several lines. This
two fields accept multiline strings. A multiline string can contain `\n`
characters. A multiline string stops when a line starts with one of the
existing key, or at the next empty line.

For instance:

```txt
# Valid
description:
    This is a valid
    multiline string

# Valid
description: This is also a valid
             multiline string

# Invalid
# description contains "This is not a" and mitigation contains "valid multiline
# string"
description: This is not a
mitigation: valid multiline string

# Invalid
# description contains "This is still not a", and the rest is considered as not
# parsable
description:
    This is still not a

    valid multiline string
```

## Frequently Asked Questions (<abbr>FAQ</abbr>)

### Why a GDPR.txt file?

I am a volunteer at [Framasoft](https://framasoft.org), a French non-profit
organisation which provides more than 15 Web services (after closing some of
them). Starting to work on the GDPR compliance of Framasoft, I realized it
would saved a lot of my time if developers provided the information I was
searching manually for each service.

The GDPR.txt file would bring big advantages if it was widely adopted:

- developers know best which data are collected;
- it avoids to duplicate work;
- it is less error-prone for hosting providers;
- it communicates clearly the personal data collected by a software.

### I am a developer and I’ve written a GDPR.txt file, is my project GDPR compliant?

No. You must check that all the purposes and collected data are legitimate. For
instance, if you use the email address only to login the users, you should
consider to collect a username instead.

Also, you should consider to allow users to update, export and delete their
personal data.

### I am a hosting provider and I shared the GDPR.txt file to my users, am I <abbr>GDPR</abbr> compliant?

No. Being compliant to <abbr>GDPR</abbr> is more complex than providing a
single file. For instance, this file is probably incomplete about the data
you’re collecting: a web server generates logs about your users, including
their IP address. This is not to the developers of the software to worry about
it (except if the software collects IPs itself).

GDPR.txt is not a magic file, it can only help you to establish your records of processing activities.

### Where should I put the file?

The GDPR.txt file SHOULD be placed in the root folder of your project,
alongside your README.

### I don’t collect any data, should I write a GDPR.txt?

It’s up to you, but it’s better if you do create a GDPR.txt file with a comment
telling that no data are collected (and congratulations by the way!)

### Can I have an example?

Sure!

```txt
# This file lists processing purposes and the personal data gathered by <your software>.
# It is intended to hosting providers who want to provide a service based on
# <your software>, to help them to comply to GDPR requirements. Note that the
# services powered by <your software> may collect more data, HTTP logs in
# particular. As a hosting provider, you must inform your users of their rights
# and how their data are used and protected.

purpose: Connect users to their accounts
lawfulness: legitimate interest

data: username
required: true
visibility: private
description:
    The username is used to identify users during the login process.
mitigation:
    Username does not have to be a real or known identity.

data: password
required: true
visibility: private
description:
    The password is used to check identity of users during the login process.
mitigation:
    Only hashes of the passwords are stored in database (but they transit over
    the network). It uses bcrypt to create the hashes.
```

## Contributing

If you have any questions, if you want to discuss about the format, or if you
intend to use a GDPR.txt file in your own project, don’t hesitate to [open an
issue](https://github.com/flusio/gdpr-txt/issues).

If you want to fix a typo in the document, you can directly [open a Pull
Request](https://github.com/flusio/gdpr-txt/pulls).

If you’re a hosting provider and you’re looking for help to comply to the
<abbr>GDPR</abbr>, this is NOT the place to ask your questions. I am not an
expert and I don’t want to provide any legal advice.
