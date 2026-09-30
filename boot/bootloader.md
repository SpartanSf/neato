# NEATO Bootloader Specification

Written by SpSf

Revision 3 of September 29, 2026

---

A NEATO compatible bootloader must obtain the `boot.lua` file from `any:system:/boot/cfg/boot.lua`.

A NEATO compatible boot.lua might appear like this:

```lua
return {
  ["Config"] = {
    ["DefaultEntry"] = 1,
    ["Autoboot"] = "none",
  },
  ["Bootlist"] = {
    {
      ["OS Name"] = "NeetOS",
      ["OS Version"] = "0.2.4",
      ["OS Description"] = "The NeetComputers Operating System",
      ["OS Args"] = {"-v", "-f"},
      ["OS Boot Path"] = "0:bios:/boot.lua",
      ["OS Environment Variable Definition"] = {
        ["EXAMPLEVAR"] = 0,
        ["VAR2"] = "Hi",
      },
    },
    -- additional entries follow the same format
  },
}
```

### Bootlist

NEATO compatible bootloaders must support ALL fields defined, as well as supporting multiple operating systems defined
in `boot.lua`.

Each entry in `Bootlist` is a table with the following fields:

| Field                              | Type                       | Required | Description                                                                                                                         |
| ---------------------------------- | -------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| OS Name                            | string                     | yes      | The name of the operating system. Displayed by the bootloader to identify the entry.                                                |
| OS Version                         | string                     | no       | The version of the operating system, displayed next to the name. It is recommended to use [semver](https://semver.org/) versioning. |
| OS Description                     | string                     | no       | A short human-readable description of the entry, displayed by the bootloader.                                                       |
| OS Args                            | string or table of strings | no       | The arguments passed to the boot path. If absent, no arguments are passed.                                                          |
| OS Boot Path                       | string                     | yes      | The path, in the format defined in [paths.md](../common/paths.md), of the Lua file that is run to boot the entry.                   |
| OS Environment Variable Definition | table (string keys)        | no       | The environment variables made visible to the boot path. If absent, none are defined.                                               |

An entry that is missing a required field, or has a field of the wrong type, is invalid and must not be booted. A
bootloader must ignore fields it does not recognize, so that entries may carry extra information for the operating
system itself.

When an entry is booted, the bootloader runs the file at `OS Boot Path`, passing `OS Args` as its arguments and
defining `OS Environment Variable Definition` in its environment, as described below.

The `OS Args` field must take in either a string, e.g. "EXAMPLEARG=1" or a table (as shown).

Arguments must be passed into the boot path as provided, so a table must pass into the boot path as ("-v", "-f") for
example, or as a raw string.

The `OS Environment Variable Definition` field must create environment variables for the boot path, as provided. Values
must keep the type they were defined with, and bootloaders must support at least strings and numbers. This
can be done different ways, but the boot path MUST be able to see defined variables in \_ENV. So, for the provided example,
`0:bios:/boot.lua` would be able to see `_ENV.EXAMPLEVAR` as `0`, and `_ENV.VAR2` as `"Hi"`.

---

### Config

NEATO compatible bootloaders must respect the Config field.

`Config.DefaultEntry` is 1-indexed as how Lua tables are indexed. `Config.DefaultEntry` controls which boot entry is first
shown and selected initially when the bootloader is opened.

`Config.Autoboot` is 1-indexed as how Lua tables are indexed. `Config.Autoboot` if set to `"none"` or any value other
than a valid index into `Bootlist` disables autoboot. If set to an index of `Bootlist` then automatically boots into
it. NEATO does not define how long it must take, if any time, for `Config.Autoboot` to complete or confirm.
