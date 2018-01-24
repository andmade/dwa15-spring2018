## What is the PATH variable?
When you run a command for a program in command line, it looks for the corresponding executable files using the directories listed in your **PATH variable** as a map. The PATH variable is one of many **Environment Variables** your computer uses.

Given this, when you add a new executable/program you wish to use via command line, you have to add its directory to your PATH variable.


## Mac: Edit your PATH
To start, use this command to see what your PATH variable is currently set to:

```bash
echo $PATH
```

Example output:

<img src='http://making-the-internet.s3.amazonaws.com/sysadmin-example-echo-path@2x.png' style='max-width:660px;' alt=''>

Note that each path in the PATH variable is separated by a colon.

One way to add new paths to your PATH variable is to add them in the `/etc/paths` file.  

Let's use an example scenario of adding the PHP executable that comes with MAMP to your PATH. This will make it so that when you run the command `php` from command line, it will use MAMP's PHP executable.

This semester, the version of PHP we're using with MAMP is `php7.1.6`:

<img src='http://making-the-internet.s3.amazonaws.com/sysadmin-identify-latest-version-of-php-in-mamp@2x.png' style='max-width:538px'>

If you dig into the MAMP folder contents on your computer, you can find a PHP executable in `/Applications/MAMP/bin/php/php7.1.6/bin`, so that's the path we want to add.

<img src='http://making-the-internet.s3.amazonaws.com/sysadmin-finding-php-in-mamp@2x.png' style='max-width:1433; width:100%' alt='Finding PHP in MAMP'>

Using Nano and the `sudo` command, open `/etc/paths`:

```bash
$ sudo nano /etc/paths
```

At the **top** of `/etc/paths`, add this line:

```xml
/Applications/MAMP/bin/php/php7.1.6/bin
```

<img src='http://making-the-internet.s3.amazonaws.com/sysadmin-append-to-paths@2x.png' style='max-width:803px; width:100%' alt=''>

Save your changes (`ctrl` + `x`, then `y`, then *Enter*).

Close and restart Terminal. (This step is important! If you don't do this, your changes won't take effect)

Test it out:

```bash
$ which php
/Applications/MAMP/bin/php/php7.1.6/bin/php
```

```bash
$ php -v
PHP 7.1.6 (cli) (built: Jul  3 2017 15:25:20) ( NTS )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies
```


## Windows: Edit your PATH

To begin, use this command to see what your PATH variable is currently set to:

```bash
PATH
```

Example output:

<img src='http://making-the-internet.s3.amazonaws.com/sysadmin-example-echo-path-windows@2x.png' style='max-width:942px;' alt=''>

Note that each path in the PATH variable is separated by a semi-colon.

Let's use an example scenario of adding the PHP executable that comes with XAMPP to your PATH. This will make it so that when you run the command `php` from command line, it will use XAMPP's PHP executable.

XAMPP includes a php executable located at `C:\xampp\php\`:

<img src='http://making-the-internet.s3.amazonaws.com/sysadmin-finding-php-in-xampp@2x.png' style='max-width:772px; width:100%' alt='Finding PHP in XAMPP'>

...so that's the path we want to add.

To edit PATH variables in Windows...

1. Goto *My Computer* > *Properties* (alternatively, you can get here by running `sysdm.cpl` from Command Line)

2. Then, from the *Properties* screen, go to *Advanced* > *Environment Variables* > *Path*.

3. You'll find `Path` under *System variables*. Select it and click *Edit*.

4. Then, add a new path and set it to `c:\xampp\php\` to the end (be sure to include the trailing backslash at the end).

Above steps illustrated:

<img src='http://making-the-internet.s3.amazonaws.com/laravel-setting-path-variable-on-windows@2x.png' class='' style='max-width:1714px; width:100%' alt='Editing your PATH in Windows'>

Ok/Save your changes.

Close and restart Cmder. (This step is important! If you don't do this, your changes won't take effect)

Test it out:

```bash
$ where.exe php
c:\xampp\php\php.exe
```

```bash
$ php -v
PHP 7.1.8 (cli) (built: Aug  1 2017 21:10:46) ( ZTS MSVC14 (Visual C++ 2015) x86 )
Copyright (c) 1997-2017 The PHP Group
Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies
```


## Reference
+ [Mac OSX Change Path Variables](http://architectryan.com/2012/10/02/add-to-the-path-on-mac-os-x-mountain-lion/#.U9nTwIBs9vI).
+ [SO: Adding directory to PATH Environment Variable in Windows](http://stackoverflow.com/questions/9546324/adding-directory-to-path-environment-variable-in-windows)
+ [How to set path and environment variables in Windows](http://www.computerhope.com/issues/ch000549.htm)
