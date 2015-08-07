# pelican-mboxreader

This pelican plugin adds a generator that can load a Unix style mbox file and
generate articles from all the entries in the mailbox.

This was written to support easy interoperation between pelican and mailman
(which creates mbox archives).

## Does this work?

Yes, mostly! Although:

* Nothing is done if there is a potential conflict between authors from email and authors
posting regularly-- there will be an issue because both MboxGenerator and ArticlesGenerator
will try to create author pages. Easy solution is to add a "via email" to the author names;
a more complicated solution is... well... more complicated.

* As a similar issue, index.html will not have any posts from email because both article
generators try to write it, I am *not* sure how to fix this.

* Dependencies on e.g. python-dateutil to parse email dates should be imported better.

* Right now we only support *one* input mbox. Obviously, it'd be trivial to support more.

* Unit testing... somehow.

* Code quality cleanup, before submitting upstream. Mainly tabs -> spaces and enforcement
of the PEP8 80 characters a line rule.

## How does it work?

Install the plugin like any other pelican plugin.

Then add the following settings to the configuration:

```
MBOX_PATH = '/path/to/mail.box'
MBOX_CATEGORY = 'Name of Mbox Category'
```

```MBOX_PATH``` defaults to "input.mbox" in the current directory. If it is not present,
Pelican should behave gracefully. ```MBOX_CATEGORY`` defaults to "Mailbox".

## Is support for other mailbox types (maildir, etc.) possible?

Yes. It would need to be programmed in and made configurable, however it would
be trivial if the mailbox type is implemented by [python's mailbox module](https://docs.python.org/2/library/mailbox.html)
(which is what this uses).

## Is this pointless?

Maybe. See the above note about mailman; it was written for a reason but may not
be something that anyone in the real world actually needs.

## Credits

Ben Rosser <rosser.bjr@gmail.com>

Written for use by the [JHUACM](https://www.acm.jhu.edu/).
