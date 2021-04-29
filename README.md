# gemspec.yml

> All you need is YAML.

[`gemspec.yml`][gemspec.yml] allows you to define all of your gem's metadata
in plain YAML, and have it loaded by a [boilerplate `<name>.gemspec`][.gemspec]
file which fills in any missing data with smart defaults.

## Example

```yaml
name: foo
summary: Foo gem
description:
  More stuff about the foo gem.

license: MIT
authors: You
email: you@example.com
homepage: https://github.com/you/foo#readme

metadata:
  documentation_uri: https://rubydoc.info/gems/foo
  source_code_uri:   https://github.com/postmodern/foo
  bug_tracker_uri:   https://github.com/postmodern/foo/issues
  changelog_uri:     https://github.com/postmodern/foo/blob/main/CHANGELOG.md

dependencies:
  bar: ~> 0.1
  baz: ~> 0.2, >= 0.2.4
  quix: ">= 1.2.3, < 2"

development_dependencies:
  bundler: ~> 2.0

post_install_message: |
  Multi-Line
  
      $ echo "post install"
  
  Message
```

    $ gem build foo.gemspec
      Successfully built RubyGem
      Name: foo
      Version: 0.0.1
      File: foo-0.0.1.gem

## Specification

* The file MUST be named `gemspec.yml`.
* The file MUST be located in the top-level directory of the gem.
* The file MUST contain plain YAML.
* Nested elements MUST be indented by two spaces.
* The each line SHOULD NOT exceed 80 columns.
* The [`gemspec.yml`][gemspec.yml] file MUST be accompanied by a
  [`<name>.gemspec`][.gemspec] file, which loads it's contents.

### name

The name of the gem.

```yaml
name: foo
```

**Required:** yes

**Type:** String

**Format:** gem name

### version

The version of the gem.

```yaml
version: 0.1.0
```

**Type:** String

**Format:** version number

**Required:** no

**Default:** if omitted, the boilerplate gemspec will attempt to load the
`lib/<name>/version.rb` file and resolve the `<Name>::VERSION` constant.

### summary

A short summary for the gem.

```yaml
summary: Foo gem for all of you foo needs
```

**Required:** yes

**Type:** String

**Format:** text, single-line

### description

A longer description for the gem.

```yaml
description: Foo gem provides foo functionality for tasks requiring foo
```

```yaml
description: |
  Foo gem for providing foo functionality.

  Please refer to the foo documentation.
```

**Required:** yes

**Type:** String

**Format:** text, multi-line

### license

The license identifier for the gem.

```yaml
license: MIT
```

```yaml
license:
  - GPL-3.0
  - LGPL-3.0
```

**Required:** yes

**Type:** String or Array of Strings

**Format:** License identifier

### authors

The author(s) of the gem.

```yaml
authors: Me
```

```yaml
authors:
  - Me
  - Bob
  - Alice
```

**Required:** yes

**Type:** String or Array of Strings

**Format:** name

### email

The primary email contact for the gem.

```yaml
email: me@example.com
```

**Required:** yes

**Type:** String

**Format:** email address

### homepage

The primary homepage for the gem.

```yaml
homepage: https://foo.github.io/
```

**Required:** yes

**Type:** String

**Format:** URL

### metadata

Additional metadata for the gem.

```yaml
metadata:
  documentation_uri: https://rubydoc.info/gems/foo
  source_code_uri:   https://github.com/you/foo
  bug_tracker_uri:   https://github.com/you/foo/issues
  changelog_uri:     https://github.com/you/foo/blob/main/CHANGELOG.md
```

**Required:** no

**Type:** Hash of String => String

**Format:** identifier => text

### require_paths

The directories within the gem that will be added to `$LOAD_PATH` when the gem
is loaded.

```yaml
require_paths: lib
```

```yaml
require_paths:
  - lib
  - vendor/*/lib
```

**Type:** String or Array of Strings

**Format:** relative path or dir glob pattern

**Required:** no

**Default:** if omitted, it will include the `lib/` and `ext/` directories,
if they exist.

### executables

The executable file names that will be installed by the gem.

```yaml
executables:
  - foo
  - bar
```

**Type:** Array of Strings

**Format:** file name

**Required:** no

**Default:** if omitted, it will default to the file names within the gem's
`bin/` directory.

### extensions

Any extension build files that will be executed when the gem is installed.

```yaml
extensions: ext/foo/extconf.rb
```

```yaml
extensions: ext/*/{extconf.rb,Makefile}
```

**Required:** no

**Default:** if omitted, it will default to all `extconf.rb` files within the
gem's `ext/` directory, if it exists.

**Type:** String or Array of Strings

**Format:** path or dir glob pattern

### files

The files that will be packaged into the gem.

```yaml
files:
  - README.md
  - lib/**/*.rb
```

**Required:** no

**Default:** if omitted, it will use the output of `git ls-files`.

**Type:** String or Array of Strings

**Format:** relative path or dir glob pattern

### extra_doc_files

Any additional files that should be included in auto-generated documentation.

```yaml
extra_doc_files: *.md
```

```yaml
extra_doc_files:
  - *.md
  - doc/EXAMPLES.md
  - doc/SPEC.txt
```

**Required:** no

**Default:** if omitted, it will include any top-level `.txt` or `.md` files.

**Type:** String or Array of Strings

**Format:** relative path or dir glob pattern

### requirements

Any external dependencies for the gem.

```yaml
requirements: graphviz >= 2.0.0
```

```yaml
requirements:
  - graphviz >= 2.0.0
  - sqlite3 >= 3.30.0
```

**Required:** no

**Type:** String or Array of Strings

**Format:** dependency

### required_ruby_version

The Ruby version required to use this gem.

```yaml
required_ruby_version: ">= 2.0.0"
```

**Required:** no

**Type:** String

**Format:** version requirement

**Note:** Strings beginning with `>` must be double-quoted for YAML.

### required_rubygems_version

The RubyGems version required to install or use this gem.

```yaml
required_rubygems_version: ">= 3.0.0"
```

**Required:** no

**Type:** String

**Format:** version requirement

**Note:** Strings beginning with `>` must be double-quoted for YAML.

### post_install_message

An optional message to display after the gem has been successfully installed.

```yaml
post_install_message: |
  Congratulations on installing the Foo gem. Do not forget to edit ~/.foorc
```

**Required:** no

**Type:** String

**Format:** multi-line

### dependencies

Runtime gem dependencies for the gem.

```yaml
dependencies:
  bar: ~> 0.1
  baz: ~> 0.5, < 2
  quix: ">= 1.2.3, < 2"
```

**Required:** no

**Type:** Hash of String => String

**Format:** gem name => version requirement

**Note:** Strings beginning with `>` must be double-quoted for YAML.

### development_dependencies

Development dependencies for the gem.

```yaml
dependencies:
  bundler: ~> 2.0
  rspec: ~> 3.0
```

**Required:** no

**Type:** Hash of String => String

**Format:** gem name => version requirement

**Note:** Strings beginning with `>` must be double-quoted for YAML.

[gemspec.yml]: gemspec.yml
[.gemspec]: foo.gemspec
