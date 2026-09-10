# plumbing

- **Event:** picoCTF 2019
- **Author:** Alex Fulton / Danny Tunitis
- **Category:** General Skills
- **Difficulty:** Medium
- **Challenge:** Keep the output from a network program and search it for the flag.

## Problem Statement

The challenge provides a network service that prints many lines of output. The goal is to search that output for the flag without manually reading every line.

## Connecting to the Service

I first connected to the service with netcat:

```bash
nc fickle-tempest.picoctf.net 65383
```

This printed a large amount of data.

## Filtering the Output

Instead of saving and inspecting all of the output manually, I piped the netcat output directly into `grep` and searched for the `pico` flag prefix:

```bash
nc fickle-tempest.picoctf.net 65383 | grep "pico"
```

The command returned the flag immediately.

## Flag

```text
picoCTF{digital_plumb3r_11fffFE5}
```

## Takeaways

- A pipe (`|`) sends the output of one command to the input of another command.
- `grep` searches streamed text for a matching pattern.
- Piping network output directly into a filter is useful when a service produces many lines.