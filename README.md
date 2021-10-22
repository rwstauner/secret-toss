# secret-toss

A small clojure script for tossing secrets between commands.

## Usage

### read / write

Store a secret named "foo" encrypted:

    secret-toss write foo

It will prompt you for the secret
and print the key to stdout.

To decrypt the secret pass the name and the key
printed from the write command:

    secret-toss read foo $key_from_write_command

### wrap / unwrap

For single use secrets you can avoid tracking the encryption key
by wrapping the command and then having the subsequent command
call unwrap:

    secret-toss wrap bar sh -c 'secret-toss unwrap bar'

This calls `write` and `read` and stores the key in the environment
that is passed to the wrapped commands.

Multiple secrets can be wrapped to allow for nesting commands:

    secret-toss wrap foo secret-toss wrap bar sh -c 'secret-toss unwrap bar; secret-toss unwrap foo'

# License

Copyright © 2021 Randy Stauner

Distributed under the Eclipse Public License version 1.0.
