# cibseven-migration

## Command line

```bash
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.configLocation=https://cibseven.github.io/cibseven-migration/replace-camunda-with-cibseven.yml -Drewrite.activeRecipes=org.cibseven.ReplaceCamundaWithCIBSeven
```

## Target version

The recipe sets the CIB seven versions through three properties. Each one has a default, so the recipe also works without them:

| Property | Default | Used for |
|---|---|---|
| `cibseven.version` | `3.0.0` | CIB seven platform: the POM properties `cibseven.version`, `version.cibseven` and `version.cibseven.bpm.assert`, and the `org.cibseven.bpm` test artifacts (assert, junit5) |
| `cibseven.community.version` | `2.2.0` | CIB seven community extensions: process test coverage, REST client, mail, cibseven-api, data, mockito, JGiven |
| `cibseven.keycloak.version` | `2.2.1` | CIB seven Keycloak extension |

Any version string works, including Enterprise Edition versions. Examples:

```bash
# CIB seven 3.0.0 (the default)
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.configLocation=https://cibseven.github.io/cibseven-migration/replace-camunda-with-cibseven.yml -Drewrite.activeRecipes=org.cibseven.ReplaceCamundaWithCIBSeven -Dcibseven.version=3.0.0

# CIB seven Enterprise 3.0.0
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.configLocation=https://cibseven.github.io/cibseven-migration/replace-camunda-with-cibseven.yml -Drewrite.activeRecipes=org.cibseven.ReplaceCamundaWithCIBSeven -Dcibseven.version=3.0.0-ee
```

- `-D` needs rewrite-maven-plugin 6.37.0 or later. With an older plugin version, set the property in the `<properties>` of your POM instead.
- A property that your POM already defines (for example `cibseven.version` in a project that already uses CIB seven) wins over the default; `-D` wins over both.
- Keep `rewrite.resolvePropertiesInYaml` at its default `true`, otherwise the placeholders in the recipe are not resolved.
- Enterprise Edition versions are not on Maven Central. Maven needs the CIB seven Enterprise repository and its credentials in your `settings.xml` to resolve them.

## Migrating to CIB seven 2.2

The recipe targets CIB seven 3.0: for example, it maps the `-jakarta` artifacts to the artifacts without the suffix that replace them in 3.0. To migrate to CIB seven 2.2, use the recipe as it was for 2.2:

```bash
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.configLocation=https://raw.githubusercontent.com/cibseven/cibseven-migration/e69532d204b91e174ef0dd357acc3242a22f7508/replace-camunda-with-cibseven.yml -Drewrite.activeRecipes=org.cibseven.ReplaceCamundaWithCIBSeven
```

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
