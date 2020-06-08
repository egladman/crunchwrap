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

#### Dependencies

- **Bash 4.0+** Unlike similar projects, crunchwrap doesn't depend on GNU Coreutils, instead crunchwrap leverages Bash's builtins commands.


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

Template:
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

# Acknowledgements

- [dylanaraps/pure-bash-bible](https://github.com/dylanaraps/pure-bash-bible)
