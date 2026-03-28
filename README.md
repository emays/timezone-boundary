# Time Zone Boundary

[![Build](https://github.com/emays/timezone-boundary/actions/workflows/maven.yml/badge.svg)](https://github.com/emays/timezone-boundary/actions/workflows/maven.yml)

Packages time zone boundary files as Maven artifacts.

Boundary files are downloaded from the [timezoneboundary-builder](https://github.com/evansiroky/timezone-boundary-builder) project releases on Github.

Latest release is timezones-with-oceans-now.geojson version 2025b.

To package a different version, update the project version

```
	<artifactId>timezone-boundary</artifactId>
	<!--Update timezone-boundary.version in properties to this major version-->
	<version>2025b.0.1-SNAPSHOT</version>
```

and, as noted, the `timezone-boundary.version` property

```
	<properties>
		<timezone-boundary.version>2025b</timezone-boundary.version>
	</properties>
```
	
To package a different time zone boundary file, update `fromFile` in the wagon plugin configuration

```
	<configuration>
		<url>https://github.com/evansiroky/timezone-boundary-builder/releases/download/${timezone-boundary.version}</url>
		<fromFile>timezones-with-oceans-now.geojson.zip</fromFile>
		<toDir>${project.build.outputDirectory}</toDir>
	</configuration>
```
	
After building the project

```
	mvn clean install
```
	
Use this packaged file in another project by unpacking with the Maven dependency plugin

```
	<plugin>
		<groupId>org.apache.maven.plugins</groupId>
		<artifactId>maven-dependency-plugin</artifactId>
		<executions>
			<execution>
				<id>unpack-timezone-data</id>
				<phase>generate-test-resources</phase>
				<goals>
					<goal>unpack</goal>
				</goals>
				<configuration>
					<artifactItems>
						<artifactItem>
							<groupId>io.github.emays</groupId>
							<artifactId>timezone-boundary</artifactId>
							<version>2025b.0.1-SNAPSHOT</version>
						</artifactItem>
					</artifactItems>
					<outputDirectory>${project.basedir}/src/test/resources/timezone</outputDirectory>
				</configuration>
			</execution>
		</executions>
	</plugin>
```

## License

Copyright 2026 Mays Systems LLC

Licensed under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0).
