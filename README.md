# Gradle multi-project, using a custom-named main build-file

This project shows an issue with Gradle multi-projects.
When the main build script has custom name, the call to `gradle` command should be:

```sh
./gradlew --no-daemon --build-file custom-name.gradle tasks
```

The `settings.gradle` file includes the children projects, (and it is processed, at least the `println`).
But when listing all the projects from main build script only the root project appears:

```
<settings> :client
<settings> :service
<custom> [root project 'gradle-multi-project-custom-buildfilename']
> rootProject.name: gradle-multi-project-custom-buildfilename
> project.name: gradle-multi-project-custom-buildfilename
:tasks
...
```

It does not apply the `rootProject.name` property neither.
Does not work even adding the `--settings-file` flag to the command line.

Asked in [this thread from Gradle forums](https://discuss.gradle.org/t/multi-project-using-custom-named-main-build-file/20657?u=lucasvc) if this is an expected behaviour.

Tested with Gradle 3.0 and 3.2.1 (uploaded wrapper 3.2.1).
