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
export bar="give you up" qux="run around and desert you" baz="let you down" foo="Never gonna"
echo -e "{{ foo }} {{ bar }}\n{{ foo }} {{ baz }}\n{{ foo }} {{ qux }}" | cw 
```

#### Results

```
Never gonna give you up
Never gonna let you down
Never gonna run around and desert you
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

#### Results

```
<!DOCTYPE html>
<html>
<body>

<h1>Hello World</h1>

</body>
</html>
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

#### Results

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
helloworld

HeLLo  WorLD

```

### Install

```
git clone https://github.com/egladman/crunchwrap.git
cp crunchwrap/crunchwrap /usr/local/bin/cw
```

# Acknowledgements

- [dylanaraps/pure-bash-bible](https://github.com/dylanaraps/pure-bash-bible)
