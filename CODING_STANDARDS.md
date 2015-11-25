Formatting
----------

Configure your editor of choice to do the following:

-   <b>Use a 4 space indent</b>

` emacs: (setq-default c-basic-offset 4)`

` Eclipse:`
`   a. Window->Preferences->Java->Code style->Formatter`
`   b. Edit->Indentation`
`   c. Indentation size: 4, Tab Size: 4`

-   <b>Do not use TAB characters</b>

` emacs: (setq-default indent-tabs-mode nil)`

` Eclipse:`
`    a. Window->Preferences->Java->Code style->Formatter`
`    b. Edit->Indentation`
`    c. Tab Policy: Spaces only`

-   <b>End files with a newline</b>

` emacs: (setq require-final-newline 'query)`
` Eclipse:`
` a. Window->Preferences->Java->Code style->Formatter`
` b. Edit->New lines: check `“`at` `end` `of` `file`”
` `
` `<font color="red">`Note:`</font>` Eclipse does NOT enforce newlines at the end of file--it will only add them when you create new files.  If you delete the trailing newline, like say with a sweeping cut-paste, you are on your own to ensure the trailing newline is there.  `
`   `

<font color="red"><b>The forthcoming formatting guidelines require manual configuration within Eclipse.</b></font>

-   <b>Use Unix-Style newlines (\\n) and UTF-8 file encoding</b>

` emacs: (defun java-setup () (setq buffer-file-coding-system 'utf-8-unix)) (add-hook 'java-mode-hook 'java-setup)`

` Eclipse:`
` a. Window->Preferences->General->Workspace`
` b. New Text file line delimiter: Other/Unix, Text file encoding: UTF-8`

-   <b>Removing trailing whitespace</b>

` Eclipse:`
` a. Window->Preferences->Java->Editor->Save actions.`
` b. Check `“`Additional` `actions`”`.`
` c. Click `“`Configure...`”`.`
` d. `“`Code` `Organizing`”` Tab -> Remove trailing whitespace on All lines.`

-   <b>Do not use non-ascii characters in your source code.</b>

Be especially careful of copy-pasted code from other sources that includes non-ascii single quotes and non-breaking spaces, as these do nothing but make it harder and uglier for certain tools to process code without adding any benefit.

-   <b>When editing other's files, follow the same bracket convention that they use when possible.</b>

Imports
-------

-   Never import \*
-   Never import statics or inner classes, use the enclosing public class name in all references

` Eclipse:`
` a. Window->Preferences->Java->Code style`
` b. Organize imports should be in the following order: java, javax, org, com.jidesoft, com`

Comments
--------

Commented code should only be left in place if it is highly likely to be needed in the future. Comments are NOT a way to remove old code--Subversion is our way to view old code, commented junk code is just distracting noise.

To be explicit:

-   Commenting out imports instead of just deleting them is pointless. REMOVE THEM.

<!-- -->

-   IDE auto-generated comments are similarly beyond worthless and should be removed.

-   Comments should only be put in for non-obvious aspect of the code they are commenting on.

<!-- -->

-   Comments do not need to have your name in them, since again Subversion is how we accomplish this. This includes @author tags in javadoc, which are both redundant with information available through subversion and which are quickly irrelevant.

Naming Conventions
------------------

-   Package names should be lower case

<!-- -->

-   Class names should always be camel case with leading uppercase

<!-- -->

-   Members and methods should be camel case

<!-- -->

-   Constants should be uppercase with \_ word separators

Java 101
--------

-   Use appropriate generics whenever possible.

<!-- -->

-   Never use java.lang.StringBuffer, use java.lang.StringBuilder instead

<!-- -->

-   Never use java.util.Hashtable, use HashMap instead

<!-- -->

-   Never use Java.util.Vector, use ArrayList instead

<!-- -->

-   Do not override superclass methods and simply call them directly. If your IDE auto-generates method like that, turn OFF that misfeature.

Constants
---------

-   Collections of constants should always be declared as static final members of a class. Interfaces should never be used for this purpose.

Subversion
----------

-   Configure your Subversion client to never allow checkins without a comment. Never check anything in without an associated comment.

<!-- -->

-   Subversion comments should be specific to what is changing.

When changing shared files, put comments specific to that file, not mass comments referring to the project or task they are being changed for.

When changing many files for the same reason, check them in in a single commit, do not repeat the same comment across 2, 10, or 30 revisions.

-   Never leave your desk until you have fixed any problems you have committed.

<!-- -->

-   When you remove or move away all files in a package, remove that directory. Similarly, do not commit empty directories to the repository until you are also committing contents to them. check\_all will identify and fail for both of these situations.

Tests
-----

-   Pure test classes should either be Junit tests or classes with main methods that run the appropriate tests. All of these should be in the src/test-java package of the appropriate project.

<!-- -->

-   JUnit test classes should end with Test, all other tests should not. JUnit test cases should be in classes with names ending in Test and marked with the @Test annotation. <font color="red">Do NOT use the pre-junit4 test framework base classes.</font>

<!-- -->

-   Testing code that will never have use outside of a pure testing environment should not be in the main java source tree.

<!-- -->

-   Testing code should follow the same coding standards are the rest of the source tree.

<!-- -->

-   All testing classes should be in a subpackage of what they are testing called “test”. Data files that tests might need should be in the same directories as the tests.

<!-- -->

-   Tests should pass when checked in. Tests that fail should always be the highest priority to fix, as tests that fail merely as a “todo” list of unimplemented functionality are just noise that hides real regression issues that testing would actually benefit us by pointing out.

Logging
-------

-   All logging should be done through the use of Logger libraries, and use appropiate logging levels.

<!-- -->

-   Applications that print anything to System.out or System.err, either through direct calls to those objects, or through the use of Exception.printStackTrace() should NOT be checked in.

Threads
-------

Normally most--if not all--tasks can be handled within a single-threaded environment.


Projects
--------

-   All java code should be in `src/java` and `src/test-java` directories in the appropriate java project.

<!-- -->

-   No package should exist in multiple projects, or in both the <b>src/java</b> and <b>src/test-java</b> project of a package.

<!-- -->

Minor things
------------

-   Do not put ()s around the value of a case statement. This hits bugs in older Java compiler versions, especially when paired with string-based switch statements.

