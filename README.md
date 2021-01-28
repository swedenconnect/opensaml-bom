![Logo](https://raw.githubusercontent.com/swedenconnect/opensaml-security-ext/master/img/sc-logo.png)

# opensaml-bom

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) [![Maven Central](https://maven-badges.herokuapp.com/maven-central/se.swedenconnect.opensaml/opensaml-bom/badge.svg)](https://maven-badges.herokuapp.com/maven-central/se.swedenconnect.opensaml/opensaml-bom)

Maven Bill of Materials (BOM) for OpenSAML

---

The dependencies you get from OpenSAML sometimes are old and [Snyk](https://snyk.io) complains about some of them. This project contains a Maven BOM that fixes these issues.

The versioning of this BOM corresponds to the OpenSAML version that it fixes (starting from 3.4.3) followed by another version which is the actual version for this BOM regarding the given OpenSAML release, for example `4.0.1.R1`.

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
        
---

Copyright &copy; 2019-2021, [Sweden Connect](https://swedenconnect.se). Licensed under version 2.0 of the [Apache License](http://www.apache.org/licenses/LICENSE-2.0).
