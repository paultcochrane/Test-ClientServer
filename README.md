Test::ClientServer
==================

This is a Perl 6 module to make tests involving network daemons and whatnot a bit easier to write
and understand. For working examples, check `t/*.t`.

It works by poorly emulating a fork using `shell()`, and then running server/client code blocks in
the child processes. Eventually this will fork correctly, but the user interface should remain
mostly the same. Extra effort has been taken to ensure it runs correctly on both Rakudo and Niecza,
and only use standard POSIX shell stuff.

Caveats
-------

* Synchronising the server and client startup is done by abusing shell pipes and stdio. If you
  intend to output test results from the server, you'll need to echo them via the client. This will
  be fixed in a future version.
* The shell-based fork means you'll be running three separate perl6 processes. It's entirely
  possible this module can cause unexpected crashes with out-of-memory errors.