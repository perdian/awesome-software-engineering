# Analyzer integrations for Maven

## SpotBugs

pom.xml:
```xml
<plugin>
    <groupId>com.github.spotbugs</groupId>
    <artifactId>spotbugs-maven-plugin</artifactId>
    <version>4.8.2.0</version>
    <configuration>
        <excludeFilterFile>.spotbugs-exclude.xml</excludeFilterFile>
    </configuration>
    <executions>
        <execution>
            <phase>verify</phase>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

[.spotbugs-exclude.xml](https://spotbugs.readthedocs.io/en/latest/filter.html):
```xml
<FindBugsFilter>
    <Match>
        <Or>
            <Bug pattern="CT_CONSTRUCTOR_THROW" />
            <Bug pattern="DM_DEFAULT_ENCODING" />
            <Bug pattern="EI_EXPOSE_REP" />
            <Bug pattern="EI_EXPOSE_REP2" />
            <Bug pattern="MS_EXPOSE_REP" />
            <Bug pattern="NP_NULL_ON_SOME_PATH_FROM_RETURN_VALUE" />
            <Bug pattern="RV_RETURN_VALUE_IGNORED_BAD_PRACTICE" />
            <Bug pattern="SE_COMPARATOR_SHOULD_BE_SERIALIZABLE" />
        </Or>
    </Match>
</FindBugsFilter>
```
