# cibseven-migration

## Command line

```bash
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.configLocation=https://cibseven.github.io/cibseven-migration/replace-camunda-with-cibseven.yml -Drewrite.activeRecipes=org.cibseven.ReplaceCamundaWithCIBSeven
```

## Target version

The recipe sets the CIB seven versions through three properties. Each one has a default, so the recipe also works without them:

| Property | Default | Used for |
|---|---|---|
| `cibseven.version` | `2.2.0` | CIB seven platform: the POM properties `cibseven.version`, `version.cibseven` and `version.cibseven.bpm.assert`, and the `org.cibseven.bpm` test artifacts (assert, junit5) |
| `cibseven.community.version` | `2.2.0` | CIB seven community extensions: process test coverage, REST client, mail, cibseven-api, data, mockito, JGiven |
| `cibseven.keycloak.version` | `2.2.1` | CIB seven Keycloak extension |

Any version string works, including Enterprise Edition versions. Example for CIB seven Enterprise:

```bash
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.configLocation=https://cibseven.github.io/cibseven-migration/replace-camunda-with-cibseven.yml -Drewrite.activeRecipes=org.cibseven.ReplaceCamundaWithCIBSeven -Dcibseven.version=2.2.0-ee
```

- `-D` needs rewrite-maven-plugin 6.37.0 or later. With an older plugin version, set the property in the `<properties>` of your POM instead.
- A property that your POM already defines (for example `cibseven.version` in a project that already uses CIB seven) wins over the default; `-D` wins over both.
- Keep `rewrite.resolvePropertiesInYaml` at its default `true`, otherwise the placeholders in the recipe are not resolved.
- Enterprise Edition versions are not on Maven Central. Maven needs the CIB seven Enterprise repository and its credentials in your `settings.xml` to resolve them.

## Pom File

add this to your maven pom.xml:
```xml
  <build>
    <pluginManagement>
      <plugins>
        <plugin>
          <groupId>org.openrewrite.maven</groupId>
          <artifactId>rewrite-maven-plugin</artifactId>
          <version>6.46.1</version>
          <configuration>
            <configLocation>
              https://cibseven.github.io/cibseven-migration/replace-camunda-with-cibseven.yml
            </configLocation>
            <activeRecipes>
              <recipe>org.cibseven.ReplaceCamundaWithCIBSeven</recipe>
            </activeRecipes>
          </configuration>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
```

run
```bash
mvn rewrite:run
```

## Making changes

You can download [replace-camunda-with-cibseven.yml](replace-camunda-with-cibseven.yml) into root dir of your project
change configuration:
<configLocation>${project.basedir}/replace-camunda-with-cibseven.yml</configLocation>
do the changes you need and run it localy

## Clean up

After the migration you can delete the file and rewrite plugin section from your pom.xml
