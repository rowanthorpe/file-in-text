file-in-text
============

A tool to encrypt (with password or gpg-key hidden recipient), conditionally
compress if beneficial, and steganographically hide a file in the trailing
whitespaces of a text-file, with 72-column wrap-protection for
email-suitability. It can also reverse the process to get the original
message.

It is a simple portable shellscript which wraps the [gpg](https://www.gnupg.org)
and [snow](http://www.darkside.com.au/snow) tools.

With it you could e.g. send a file "hidden in plain sight" within a
plain-text email's trailing spaces rather than as an attachment (if the
email-text is too short to accomodate it the remainder is appended in blank
lines at the end, which is more obvious). Of course any serious cryptanalyst
who knows to look for it will find and recognise the strange pattern of
trailing spaces as a red-flag, and may even extract the still-encrypted file
(so this should not be seen as a bulletproof technique for plausible
deniability) but even then the encryption is provided by gpg, so is still
as safe as any normally encrypted email. The main usefulness could be:

* As a fun toy
* To send a payload within a plain-text email to a public mailing-list which
  an intended recipient can extract but most casual viewers will never
  realise was even there (similarly to how spies use [dead drops](https://en.wikipedia.org/wiki/Dead_drop)).

It handles input/output-files, and/or stdin/stdout, uses a crude algorithm
to disable compression if not useful (for small size), leverages gpg's
options to accomodate both symmetric (password) and asymmetric (keypair)
encryption, and uses "hidden recipient" for added paranoia-value with
asymmetric encryption.

Quick Start
-----------

* Install dependencies (e.g. `apt-get install gpg stegsnow` on Debian-based
  systems)
* Copy `file-in-text` to somewhere in your `$PATH`
* Run `file-in-text --help` for details

License
-------

Copyright © 2017 Rowan Thorpe <rowan@rowanthorpe.com>

file-in-text uses the GPLv3 license, check the COPYING file.

Any additional contributions are noted in the AUTHORS.md file.

Rationale
---------

I loved the idea & implementation of [snow](http://www.darkside.com.au/snow), but the embedded
encryption [ICE](http://www.darkside.com.au/ice/index.html) is a
small library written by its author, which hasn't undergone any
third-party cryptanalysis, and appears to have not seen an update
since 1999(?). I was curious how feasible it would be to let gpg do
the encrypting (which obviously comes with the cost of being less
efficient for encrypting tiny text messages though), so for fun I
wrote this as a tool for doing that in both directions. It was more
effective and efficient than I expected, so I added some small bits
of functionality too.
