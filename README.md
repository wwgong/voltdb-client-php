PHP VoltDB Client Library
=========================

The PHP VoltDB client library allows connecting to a VoltDB cluster, invoking
stored procedures and reading responses from a PHP 5.3 application.

# Supported Platforms

* 64-bit Linux
* 64-bit SmartOS
* Mac OS X

# Installation

Requirements:
  * VoltDB C++ client library source ("noexceptions" branch)
  * PHP 5.3

The C++ client libray must be compiled WITHOUT compiler optimization. To do
this, you have to modify the makefile in the C++ client library to remove "-O3"
from the compiler flags.

To prepare the PHP extension for building, first execute the following command,

    phpize

It will generate the script for configuration. Then you can configure using the
command,

    ./configure --with-voltdb=CXX_LIB_PATH

replace CXX_LIB_PATH with the path to the C++ client library source.

Note: If you are building on 64-bit SmartOS, you have to append CXXFLAGS="-m64"
and LDFLAGS="-m64" to ./configure so that it will generate 64-bit binary.

Once configure finishes successfully, type

    make

The compiled binary will be in the "modules" sub-directory. Copy the VoltDB PHP
extension (voltdb.so) to your PHP extension library (specified in your php.ini
file).

Edit your php.ini file to load the VoltDB extension:

    extension=voltdb.so

Note that if you are running PHP through a web server such as Apache
(instead of command line), you will have to restart/reload the server
for the new php.ini changes to take effect.

# Running

To make sure that the extension is loaded successfully, you can run the
following command if you are using PHP CLI,

    php -m | grep voltdb

If the command returns a single row saying "voltdb", then it's
loaded.

If you are using PHP on a web server, you can check if the output of php_info()
contains "voltdb".

Please see the examples directory for how to use the client.

# Known Issues

This wrapper is still in its development phase, so a few features are
not fully supported. This includes:

* Parameters arrays
* Varbinary type