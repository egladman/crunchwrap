# crunchwrap
Barebones logic-less templating written in pure Bash inspired by [mustache](https://mustache.github.io/). Crunchwrap works by evaluating variables in your shell.

```
printf '%s\n' "Hello {{ USER }}!" | cw
```

### Install

```
git clone https://github.com/egladman/crunchwrap.git
cp crunchwrap/crunchwrap /usr/local/bin/cw
```

```
$ cw --help
crunchwrap v0.1.0, a logic-less templating engine.
Usage: cw [options...] <path/to/variables>
Options:
  -h, --help                                 show this help text
  -v, --verbose                              make the operation more talkative
  -i, --ignore-emvironment                   start with an empty environment
  -V. --version                              print crunchwrap version

Report issues at https://github.com/egladman/crunchwrap/issues
```

#### Dependencies

- **Bash 4.0+** Unlike similar projects, crunchwrap doesn't depend on GNU Coreutils by default. Everything is handled by Bash's builtins.

##### Disclaimer

Optional flag`-i, --ignore-environment` depends on `env`, an external program provided by Coreutils. I could've looped through each variable and leveraged builtin `unset` to empty the environment. However this solution isn't as elegant as `env -i`. Given how ubiquitous `env` is, I don't think it's inclusion will negatively impact anyone.

### Variables

```
{{ <var> }}
{{! <var> }}                   # Exit if variable evaluates to an empty string
{{% <var> }}                   # Escape HTML
```

---

### Templates

A template is a file that contains any number of crunchwrap tags. The template's filename typically ends with `.cw`, however this is not a requirement.


#### Importing Templates

```
{{@ <path/to/template> }}
```

*Note:* At this time the template's path specified in the tag cannot contain any spaces.

### Examples

Create Template:
```
cat << EOF > /tmp/helloWorld.txt.cw

{{ a }}World

hello {{ c }}
hello {{ c }}\r?
 hello {{ c }}!
{{ b }}    W O R L D
{{ d }}_{{ c }}
  {{ d }}{{ c }}
HELLO{{ e }}WORLD
HELLO {{ e }} WORLD
{{ d }}\t{{ c }}
{{ g }}

{{% f }}

EOF
```

Command:
```
export a="Hello" b="H E L L O" c="world" d="hello" e=" & " f="\"HeLLo\" & GoODbyE" g="{{ c }}{{ d }}"; cat /tmp/helloWorld.txt.cw | cw
```

Output:
```

HelloWorld

hello world
hello world\r?
 hello world!
H E L L O    W O R L D
hello_world
  helloworld
HELLO & WORLD
HELLO  &  WORLD
hello\tworld
worldhello

&quot;HeLLo&quot; &amp; GoODbyE

```

# License

MIT


# Acknowledgements

- [dylanaraps/pure-bash-bible](https://github.com/dylanaraps/pure-bash-bible)
