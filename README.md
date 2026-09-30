# NEATO

(Norms Expressed As a Tool for Operating (S)ystems)

### Latest NEATO Spec Version: v0 Revision 3 of September 29, 2026

NEATO is a standard that defines APIs and standard conventions for NEET Computers operating systems and their method
of booting.

The standards are not meant to be a large, strict ruleset, but rather a shim for general program compatibility over
the already existing functions that NEET Computers offers, and to make API changes in NEET Computers an issue for OS
maintainers to resolve, rather than the programs themselves. NEATO aims to include basic APIs which most applications
would need, such as for terminal emulation or standards for how program arguments should work.

An OS may comply with these body of standards however the maintainer should desire to. In order to maintain NEATO
compatibility, an operating system must provide NEATO software an environment which complies with NEATO specifications.

---

### Reasoning

NEET Computers encourages users to write their own operating systems, which means that application compatibility
may not be guaranteed from one operating system to the next. It also raises a problem of writing the code itself,
as developers may need to ship different versions of software for every operating system which the software maintainer
would like to deploy it on. NEATO aims to solve this by providing a body of standards for an operating system to
provide to a program, or, how the operating system itself may boot, for compatibility.

---

### Versioning

The NEATO spec version (`v0`) and revision number above are what `sys.getNEATOCompat` reports. Every specification file
also carries its own `Revision N of <date>` line, which counts changes to that file. Any change to the meaning of a
file (as opposed to fixing a typo in it) must increase that file's revision number, update its date, and increase
the revision number of the whole spec above. The spec revision date is therefore always the date of the most recent
file revision.

---

NEATO program API definitions, like functions or events relating to the NEATO body of standards, are placed in the
`api` folder.

NEATO definitions about the NEATO compliant boot process are placed in the `boot` folder.

Common formats that are shared between NEATO program API definitions and the NEATO boot definitions are defined in
the `common` folder.

NEATO specifications for networking protocols are defined in the `network` folder.
