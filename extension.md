---
title: AsterixDB Extensions
---

* TOC
{:toc}

---

## Integrating with AsterixDB Build

Extensions can be built as part of the AsterixDB + Hyracks build by adding a module in 'asterixdb/asterix-opt'  The
 presence of a pom.xml in this directory adds this to the maven reactor as a sub-module of asterixdb.

### Bill of Materials Maven Module

A Bill of Materials (i.e. BOM) must be provided to indicate which (if any) jars & dependencies should be included in
 the AsterixDB (e.g. asterix-server, asterix-installer, etc.) binary assemblies.  Typically, the maven module defined
 in asterixdb/asterix-opt will have a BOM project as a sub-module.

This BOM must have the following coordinates, as this is used as the linkage into the asterix-server binary-assembly:
`org.apache.asterix:asterix-opt-bom:0.8.9-SNAPSHOT:pom` (_version must match AsterixDB project version_)

Any dependencies specified in the BOM (as well as transitive dependencies) will be included in the AsterixDB binary
  assemblies.  If no jars are desired to be included in the AsterixDB binary assemblies, the BOM need not specify any
  dependencies.

#### Example BOM

    <project
        xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">

      <modelVersion>4.0.0</modelVersion>

      <!-- project coordinates -->
      <groupId>org.apache.asterix</groupId>
      <artifactId>asterix-opt-bom</artifactId>
      <version>0.8.9-SNAPSHOT</version>
      <packaging>pom</packaging>
      <name>psu-nittany-bom</name>
      <description>Penn State Nittany Lion Search Extension to AsterixDB</description>

      <!-- any dependencies listed here will be included in -->
      <!-- asterix-server, etc. binary assemblies -->
      <dependencies>
          <dependency>
          <groupId>edu.psu.cs</groupId>
          <artifactId>nittany-search</artifactId>
          <version>0.1.0-SNAPSHOT</version>
        </dependency>
      </dependencies>
    </project>
