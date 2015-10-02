
Apache Commons CSV
===================

The Apache Commons CSV library provides a simple interface for reading and writing
CSV files of various types.

Documentation
-------------

More information can be found on the [homepage](https://commons.apache.org/proper/commons-csv).
The [JavaDoc](https://commons.apache.org/proper/commons-csv/archives/1.1/apidocs/index.html) can be browsed.
Questions related to the usage of Apache Commons CSV should be posted to the [user mailing list][ml].

Where can I get the latest release?
-----------------------------------
You can download source and binaries from our [download page](https://commons.apache.org/proper/commons-csv/download_csv.cgi).

Alternatively you can pull it from the central Maven repositories:

```xml
<dependency>
  <groupId>org.apache.commons</groupId>
  <artifactId>commons-csv</artifactId>
  <version>1.2</version>
</dependency>
```

Contributing
------------

We accept PRs via github. The [developer mailing list][ml] is the main channel of communication for contributors.
There are some guidelines which will make applying PRs easier for us:
+ No tabs! Please use spaces for indentation.
+ Respect the code style.
+ Create minimal diffs - disable on save actions like reformat source code or organize imports. If you feel the source code should be reformatted create a separate PR for this change.
+ Provide JUnit tests for your changes and make sure your changes don't break any existing tests by running ```mvn clean test```.

If you plan to contribute on a regular basis, please consider filing a [contributor license agreement](https://www.apache.org/licenses/#clas).
You can learn more about contributing via GitHub in our [contribution guidelines](CONTRIBUTING.md).

License
-------
Code is under the [Apache Licence v2](https://www.apache.org/licenses/LICENSE-2.0.txt).

Donations
---------
You like Apache Commons CSV? Then [donate back to the ASF](https://www.apache.org/foundation/contributing.html) to support the development.

Additional Resources
--------------------

+ [Apache Commons Homepage](https://commons.apache.org/)
+ [Apache Bugtracker (JIRA)](https://issues.apache.org/jira/)
+ [Apache Commons Twitter Account](https://twitter.com/ApacheCommons)
+ #apachecommons IRC channel on freenode.org

[ml]:https://commons.apache.org/mail-lists.html
