Hello World sample to compare the size of the generated runtime image with and without
java.util.logging. Ensure a modules JDK is on the path and the run:

```bash
cd jul
mvn package
jlink --module-path target/dependency/* --add-modules TestModular --launcher testX=TestModular/eu.doppel_helix.dev.testmodular.testmodular.TestClass --output target/runtime-image
target/runtime-image/bin/java --list-modules
# TestModular
# java.base@11.0.2
# java.logging@11.0.2
du -s target/runtime-image
# 48364
cd ..
cd plain
mvn package
jlink --module-path target/dependency/* --add-modules TestModular --launcher testX=TestModular/eu.doppel_helix.dev.testmodular.testmodular.TestClass --output target/runtime-image
target/runtime-image/bin/java --list-modules
# TestModular
# java.base@11.0.2
du -s target/runtime-image
# 48140
```

Conclusion: The impact of having java.util.logging as part of the module image is
minimal (~250kB).
