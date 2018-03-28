---
feature: nixos_templates
start-date: 2018-03-28
author: Florent Becker
co-authors: (find a buddy later to help our with the RFC)
related-issues: (will contain links to implementation PRs)
---

# Summary
[summary]: #summary

Include several less barebones versions of configuration.nix in the installer. Let the user use `nixos-generate-config --template office_work` to get a reasonable configuration for an office machine.

# Motivation
[motivation]: #motivation

Currently, a machine installed by `nixos-install` without manual edition of configuration.nix is bare-bones. Moreover, as the number of available options in configuration.nix grows, their discoverability decreases further. The manuals and man pages do a good job of documenting the available features and options, but they are not very efficient at directing users towards a reasonable starting point for their use-case.

Hopefully, the templates can be made visible on the desktop of the installer's live environment, and users can go faster from zero to a nixos system which fits their needs in the most idiomatic way possible.

In particular, splitting the default `configuration.nix` according to the intended use of the machine allows to showcase more features in each of the templates.

Nixos succeeded in turning configuration tutorials and stack-overflow questions into programmatic, community-maintained options in `configuration.nix`. The ambition here is to have a formal, well-maintained version of people publishing their `configuration.nix` somewhere on github.

# Detailed design
[design]: #detailed-design

A set of templates for `configuration.nix` are added within the installation image. `nixos-generate-config` is given a `--template` which copies the given template as the host's `configuration.nix`. Each template can be copied as-is, or it could contain a series of variables, together with interactive questions. Then `nixos-generate-config` would ask the user these questions to fill the variables (the user can still edit the file afterwards).

From there on, installation proceeds as currently with `nixos-install`.

Templates to provide include:
[TBD]

# Drawbacks
[drawbacks]: #drawbacks

This moves nixos closer to usual distros and, if done carelessly, might hide the simplicity of the model (edit `configuration.nix` -> run `nixos-install` / `nixos-rebuild`).

# Alternatives
[alternatives]: #alternatives

## Repository of configuration files
[Details to be added]

## Meta-packages / attributes
[Details to be added]

## Status quo
[Details to be added]

# Unresolved questions
[unresolved]: #unresolved-questions

What format to use for the template files? Which kind of interaction do we want to add between the boot of the install media and `nixos-install`?

# Future work
[future]: #future-work

`nixos-generate-config` needs to be extended to support templates / interaction.
The templates need to be created and maintained. This is a new burden for the nixos community, but it should alleviate the bitrot of published personnal snippets of `configuration.nix` and the amount of folklore needed to successfully use / install nixos.
