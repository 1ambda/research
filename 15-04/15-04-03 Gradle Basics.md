
### Plugins

#### Application Plugin

[Docs](http://gradle.org/docs/current/userguide/application_plugin.html)


```gradle
apply plugin: 'application'
mainClassName = "git.lambda.app.Main"

```

Then, you can run application using `gradle run`

<br/>

#### Java Plugins

Tasks

![](http://gradle.org/docs/current/userguide/img/javaPluginTasks.png)

Dependency Management

![](http://www.sinking.in/blog/wp-content/uploads/2013/12/gradle_configurations_and_sourcesets-1024x276.png)



<br/>

### Build Life Cycle

- build phases: Initialization, Configuration, Execution

```gradle
// setting.gradle
println 'This is executed during the initialization phase.'

// build.gradle
println 'This is executed during the configuration phase.'

task configured {
    println 'This is also executed during the configuration phase.'
}

task test << {
    println 'This is executed during the execution phase.'
}

task testBoth {
    doFirst {
      println 'This is executed first during the execution phase.'
    }
    doLast {
      println 'This is executed last during the execution phase.'
    }
    println 'This is executed during the configuration phase as well.'
}
```

output of `gradle test testBoth`

```
> gradle test testBoth
This is executed during the initialization phase.
This is executed during the configuration phase.
This is also executed during the configuration phase.
This is executed during the configuration phase as well.
:test
This is executed during the execution phase.
:testBoth
This is executed first during the execution phase.
This is executed last during the execution phase.

BUILD SUCCESSFUL

Total time: 1 secs
```

<br/>

### Provided

dependencies which required at compiled time but should be removed when application is executed (runtime). See [gradle-extra-configurations-plugin](https://github.com/nebula-plugins/gradle-extra-configurations-plugin)
