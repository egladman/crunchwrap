# crunchwrap
Barebones mustache-like templating written in pure Bash. Crunchwrap works by evalulating existing variables in your shell's environment. Use anywhere you'd use pipes!

### Dependencies

- **Bash 4.0+** Unlike similar projects, crunchwrap doesn't depend on GNU Coreutils, instead crunchwrap leverages Bash's builtins commands.


### Syntax

```
{{ <var> }}
```

### Examples

```
export foo="Never gonna" bar="give you up" baz="let you down" qux="run around and desert you"
echo -e "{{ foo }} {{ bar }}\n{{ foo }} {{ baz }}\n{{ foo }} {{ qux }}" | cw 
```

--- 

```
cat << EOF > /tmp/sample.html.cw

<!DOCTYPE html>
<html>
<body>

<h1>{{ foo }}</h1>

</body>
</html>
EOF
```

```
export foo="Hello World"; cat /tmp/sample.html.cw | cw > /tmp/sample.html
```

---

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

{{ f }}

EOF
```

```
export a="Hello" b="H E L L O" c="world" d="hello" e=" & " f="HeLLo  WorLD" g="{{ d }}{{ c }}"; cat /tmp/helloWorld.txt.cw | cw > /tmp/helloWorld.txt
```



### Install

```
git clone https://github.com/egladman/crunchwrap.git
cd crunchwrap
cp crunchwrap /usr/local/bin/cw
```

# Acknowledgements

- [dylanaraps/pure-bash-bible](https://github.com/dylanaraps/pure-bash-bible)
