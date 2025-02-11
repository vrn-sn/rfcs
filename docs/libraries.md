# Libraries

## Summary

This RFC defines the structure of a Luau library, outlining the standards for creating and maintaining reusable code modules in Luau.

## Motivation

The primary motivation for this RFC is to establish a clear and consistent structure for Luau libraries, which will facilitate code reuse, improve maintainability, and promote best practices within the development community.
By defining these standards, we aim to:

- Encourage the creation of high-quality libraries.
- Simplify the process of integrating third-party libraries into projects.
- Enhance collaboration among developers by providing a common framework.
- Reduce redundancy and duplication of effort by promoting the use of shared libraries.

This is an important prerequisite for building standardized package management for Luau.
The expected outcome is a robust ecosystem of reusable Luau libraries that can be easily discovered, integrated, and maintained, ultimately making development workflows more efficient.

## Design

### Components

At a bare minimum, a library must comprise three components: a root container, a top-level configuration file, and a Luau script serving as the library's entry point.

### Configuration File

The configuration file, named `metadata.luon`, contains a Luau table literal with the library's metadata and settings.
This file must be placed in the root directory of the library.

Below is an example of what a `metadata.luon` file might look like.

```luau
{
    metadata = {
        name = "example-library",
        version = "1.0.0",
        description = "An example Luau library",
        license = "MIT",
        author = "Person Doe",
        keywords = {"example", "library", "luau"},
    }
    config = {
        entry = "./src/init.luau",
        luaurc = {
            languageMode = "strict",
            lint = {
                "*": true,
                "LocalUnused": false
            },
            lintErrors = true,
            globals = {},
            aliases = {}
        }
    }
    dependencies = {
        dependency1 = "2.0.0",
        dependency2 = ">=1.2.0 <=1.5.0"
    }
    distribution = {
        repository = "https://github.com/author/example-library",
        documentation = "https://github.com/author/example-library#readme"
    }
}
```

#### Metadata

The metadata table includes essential information about the library:

- `name`: The name of the library. This should be unique within the ecosystem.
- `version`: The version of the library, following semantic versioning.
- `description`: A brief description of what the library does.
- `license`: The license under which the library is distributed, adhering to the identifier format of the [SPDX License List](https://spdx.org/licenses/).
- `author`: The name of the author or maintainer of the library.
- `keywords`: A list of keywords that describe the library and can help in its discovery.

#### Configuration

The configuration table specifies settings relevant to the interaction, execution, and development of the library:

- `entry`: The path to the entry point script of the library, relative to `libconfig.luon`.
- `luaurc`: A table containing settings that appear in `.luaurc` files outside of a library context.
Similar to `.luaurc`, these settings apply to the contents of the library's root directory.

#### Dependencies

The dependencies table lists other libraries that this library depends on, along with their versions.
Every key in this table is the name of another library, with compatible versions stored under each key.

#### Distribution

The distribution table provides information on where the library's source code and documentation can be found:

- `repository`: The URL of the repository hosting the library's source code.
- `documentation`: The URL of the library's documentation.

#### Additional fields

This is the bare minimum that the Luau specification defines for a library.
However, other tools and frameworks are free to require additional fields and properties to support their specific use cases and requirements.

## Drawbacks

This RFC proposes a more structured approach to library creation and management, which may initially appear to conflict with the lightweight and flexible nature of an embeddable language like Luau.
However, the intention is to strike a balance between preserving the embeddable philosophy of Luau and offering a comprehensive framework for reusable code modules.
By establishing clear guidelines and standards, we aim to enhance the quality and consistency of libraries without compromising the core principles of the language.
This design is intended to be sufficiently generalized, ensuring that it can be adapted to any embedded context that opts to implement this functionality.

## Alternatives

Not implementing this RFC would mean a continuation of the current state.
As of now, a library ecosystem for Luau has not developed due to a lack of standardized structures and guidelines.
Without a clear framework, developers face challenges in creating, sharing, and integrating libraries, leading to fragmented efforts and limited collaboration.
This RFC aims to address these issues by providing a consistent approach, fostering a more cohesive and robust library ecosystem.