---
title: "Annotations"
weight: 2
---

Coat provides two annotations, a type-level annotation `@Coat.Config` and
a method-level annotation `@Coat.Param`. Both annotations are mandatory.


### @Coat.Config

Each interface that should be processed by the annotation processor must be
annotated with `@Coat.Config`. 

The generated class will always be generated in the same package as the
annotated interfaec.

The name of the generated class is by the default the interface name with
`Immutable` prepended to it. One exception is if the interface name starts with
an underscore. In that case the generated class name is the same as the
interface, but with the leading underscore remove. There for the interface
`_MyConfig` the generated class would be `MyConfig`.

`@Coat.Config` supports a single parameter `className` that can be specified to
generate a class with a different name than when applying the above
mentioned naming rules. When `className` is specified it will be used as
the generated class name. It will still be generated in the same package as
the annotated interface.

### @Coat.Param

Each accessor method in the annotated interface must be annotated with
`@Coat.Param`. 

The mandatory parameter `key` specifies the name of the key
as it must be specified in the config file (or the `Properties` or `Map`
object with which the config class is instantiated).

An optional parameter `defaultValue` can be specified to define a default
value that will be used if the config key is missing in the config file.
The default value must be specified as a String in the same form it would
be specified in the config file. For example:

```java
@Coat.Param(key = "port", defaultValue = "8080")
public int port();
```

The generated config would return the value that was specified in the
config file or `8080` if no port was specified.


