# cibseven-migration

add this to your maven pom.xml:
```xml
  <build>
    <pluginManagement>
      <plugins>
        <plugin>
          <groupId>org.openrewrite.maven</groupId>
          <artifactId>rewrite-maven-plugin</artifactId>
          <version>5.44.0</version>
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

After the migration you can delete the file and rewrite plugin section from you pom.xml