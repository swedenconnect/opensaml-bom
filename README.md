![Logo](https://raw.githubusercontent.com/swedenconnect/opensaml-security-ext/master/img/sc-logo.png)

# opensaml-bom

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) [![Maven Central](https://maven-badges.herokuapp.com/maven-central/se.swedenconnect.opensaml/opensaml-bom/badge.svg)](https://maven-badges.herokuapp.com/maven-central/se.swedenconnect.opensaml/opensaml-bom)

Maven Bill of Materials (BOM) for OpenSAML

---

The dependencies you get from OpenSAML sometimes are old and [Snyk](https://snyk.io) complains about some of them. This project contains a Maven BOM that fixes these issues.

The versioning of this BOM corresponds to the OpenSAML version that it fixes (starting from 3.4.3) followed by another version which is the actual version for this BOM regarding the given OpenSAML release, for example `3.4.3.R1`.

Include the following in your POM using OpenSAML to get patched transitive dependencies:

```
<dependencyManagement>
  <dependencies>
      
    <!-- Setup OpenSAML dependencies with no reported vulnerabilities. -->
    <dependency>
      <groupId>se.swedenconnect.opensaml</groupId>
      <artifactId>opensaml-bom</artifactId>
      <version>...</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>

  </dependencies>
</dependencyManagement>

```

### Special handling

In most cases you could just include the OpenSAML dependency you need and trust that the OpenSAML BOM has sorted out all dependencies, but for some includes you need to do a little bit more yourself.

#### dom4j

The `opensaml-storage-impl` jar has a transitive dependency to `dom4j:dom4j:jar:1.6.1`. This version has been reported to be vulnerable (<https://snyk.io/vuln/SNYK-JAVA-DOM4J-174153>). Unfortunately, the replacement needed has another group name (`org.dom4j`) so the BOM cannot fix this for you. It excludes the bad `dom4j`-dependency from `opensaml-storage-impl`, but you need to add the `org.dom4j` dependency yourself.

So, if you include `opensaml-storage-impl` as a dependency, you must do:

```
<dependency>
  <groupId>org.opensaml</groupId>
  <artifactId>opensaml-storage-impl</artifactId>
</dependency>

<!-- We don't want to use dom4j:dom4j:jar:1.6.1 from opensaml-storage-impl. -->   
<dependency>
  <groupId>org.dom4j</groupId>
  <artifactId>dom4j</artifactId>
</dependency>

```

#### Velocity and commons-collection

The Velocity template engine jar (`org.apache.velocity:velocity:jar:1.7`) is included by `opensaml-saml-impl`. This dependency will include the `commons-collections:commons-collections:jar:3.2.1` dependency which Snyk reports has an arbitrary code execution vulnerability (<https://app.snyk.io/vuln/SNYK-JAVA-COMMONSCOLLECTIONS-30078>). It does not exist any fixes for this bug, so the OpenSAML BOM simply excludes the Velocity-dependency. If you need Velocity (for example when sending an `AuthnRequest` using OpenSAML-style), you need to include the dependency yourself.

```
<dependency>
  <groupId>org.apache.velocity</groupId>
  <artifactId>velocity</artifactId>
  <version>1.7</version>
</dependency>
```
        
---

Copyright &copy; 2019, [Sweden Connect](https://swedenconnect.se). Licensed under version 2.0 of the [Apache License](http://www.apache.org/licenses/LICENSE-2.0).
