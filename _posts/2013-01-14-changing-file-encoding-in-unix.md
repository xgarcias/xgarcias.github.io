---
layout: post
title: Changing the File Encoding in Unix
date: '2013-01-14T13:52:00.002+01:00'
author: Xavier Garcia
tags:
- encoding
- ascii
- utf
- unix
- commands
modified_time: '2013-01-14T13:52:38.935+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-3788900225820775843
blogger_orig_url: http://www.shellguardians.com/2013/01/changing-file-encoding-in-unix.html
---
From time to time, Unix users have to deal with files sent by colleagues that are not properly encoded and this may cause a bit of a trouble.

You may find your self trying to write a shell script around a file, but a cat only spits gibberish. Or, if you try to work with something a bit more elaborated  like grep or sed, it will not find any match. Huh? Chances are that the file encoding is not ASCII and the standard Unix tools will not understand its content.

```shell
$ less myfile.txt
"myfile.txt" may be a binary file.  See it anyway?
$ file myfile.txt
myfile.txt: Little-endian UTF-16 Unicode text, with CR, LF line terminators
```

At this point, there are two options. You can write a small script with your favourite language or use the standard tools in your system, instead.  The final result will be the same, because all use the same set of functions for the conversions.

If you want to program a bit, the following languages use **iconv** for character set conversion.

* C [http://www.kernel.org/doc/man-pages/online/pages/man3/iconv.3.html](http://www.kernel.org/doc/man-pages/online/pages/man3/iconv.3.html).
* PHP [http://php.net/manual/en/book.iconv.php](http://php.net/manual/en/book.iconv.php).
* Perl [http://search.cpan.org/dist/Text-Iconv/Iconv.pm](http://search.cpan.org/dist/Text-Iconv/Iconv.pm).
* Python [http://pypi.python.org/pypi/iconv/1.0](http://pypi.python.org/pypi/iconv/1.0).
* Ruby [http://ruby-doc.org/stdlib-1.9.2/libdoc/iconv/rdoc/Iconv.html](http://ruby-doc.org/stdlib-1.9.2/libdoc/iconv/rdoc/Iconv.html).

If you are writing a shell script, you can always use the [iconv](http://linux.die.net/man/1/iconv) program.  It accepts the input/output encodings and the source file. It will send the result to the standard output.

```shell
$ iconv -f utf16 -t ascii oldfile > newfile
```
