<!-- You have some errors, warnings, or alerts. If you are using reckless mode, turn it off to see useful information and inline alerts.
* ERRORs: 3
* WARNINGs: 0
* ALERTS: 0 -->

<h2>Docs to Markdown: Tigre edition</h2>

These are features that are new to Docs to Markdown with the development version of Docs to Markdown: Tigre edition. More to come!

This document has been converted to Markdown/HTML using the current development version.

<h2 id="comments">Comments</h2>

This feature allows you to insert comments in a Google Doc that will not appear in the converted output (with the exception of comments in a code block).

* Comments are single-line // comments that use leading-dot notation with //. That is, comment lines start with .//, followed by the comment. 
* Comment lines do not appear in the converted output unless they are inside a code block.
* For example, these comments in a code block do appear in the output:

    ```
    .// Some comments in a code block.
    .// These will appear in the output.

    ```

Some normal text.

<h2 id="variables">Variables</h2>

Variables let you define small (or large) snippets of text or source code that you can reuse at multiple places in a document.

Some characteristics of variable definitions:

* Variable definitions use leading-dot notation.
* Single-line variable definitions look like simple assignments:

```
.var name = Baby Sniglar

```

* Multi-line variable definitions are more like an HTML block tag:

```
.var name
This is the value
of the variable called name.
This will not override a single-line variable
called name.
./var

```

* Variable definitions can appear anywhere in the document. (They need not appear before they are used.)
* Variable definitions do not appear in the converted output, unless they are in a code block.
* Single-line variable definitions get parsed first, then multi-line variable definitions.
* If there are duplicate variable names, the first definition wins. That is, there is no overriding of variable values. If a single-line definition and a multi-line definition share the same variable name, the single-line definition wins.

To use a variable value, use .$ followed by the variable name. For example, to use the value of the variable named z: .&dollar;z (which converts to: this is the value of the variable called z).

<h3>Variable examples</h3>

* .&dollar;name: Baby Sniglar
* .&dollar;z: this is the value of the variable called z
* .&dollar;multi: This is a multiline var value
with two lines
* .&dollar;y: value of y
* .&dollar;varTest: variable test (first single-line definition)

My name is Baby Sniglar. This is this is the value of the variable called z. This is This is a multiline var value
with two lines. This is value of y. These variables may be defined after this paragraph.

If a variable is defined more than once, the first definition wins. And single-line variables get parsed before multiline variables. So the following variable definitions:

```
.var varTest
This is a multiline definition
of vartest.
.var varTest = variable test (first single-line definition)
.var varTest=variable override testing
./var
```

Result in this: This is the value of varTest: variable test (first single-line definition).

<h3>Code examples as variables</h3>

When you use a variable that is a code example, you must format it in a constant-width font, otherwise it will appear as normal text. For example, this is how the .&dollar;helloJava variable instance is formatted as normal text:

lang:  java
// Your First Program

class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!"); 
    }
}

Here is the same  code sample variable formatted as code:

```java
// Your First Program

class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!"); 
    }
}
```

Note that you can also include the language specification in code samples (see docs on code blocks for details): The next code sample is defined in this variable that starts with `lang: bash`:

```
.var bashFunction
lang: bash
# Process and analyze a log file.
function alog {
  sed -n 's/userKey.*>>/\n&\n/gp' $* > jkey.txt
  echo head:
  head -n 5 jkey.txt
  echo
  echo tail:
  tail -n 5 jkey.txt
  echo
  nfiles=`ls $* | wc -l`
  echo number of files: $nfiles 

  gds jkey.txt
}
./var
```

And it results in a code block like this:

```bash
# Process and analyze a log file.
function alog {
  sed -n 's/userKey.*>>/\n&\n/gp' $* > jkey.txt
  echo head:
  head -n 5 jkey.txt
  echo
  echo tail:
  tail -n 5 jkey.txt
  echo
  nfiles=`ls $* | wc -l`
  echo number of files: $nfiles 

  gds jkey.txt
}
```

We want to see comments included in code samples:

```go
package main
// We want to see this comment!
import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

<h3 id="undefined-variables">Undefined variables</h3>

If you use an [UNDEFINED VAR]:undefinedVar, you will get a stern and visible warning. For example:

This is a variable test (first single-line definition). My name is Baby Sniglar. This variable is [UNDEFINED VAR]:bogus. We need to alert for undefined variables. But we don’t care about unused variables. Another use of [UNDEFINED VAR]:bogus. This is .&dollar;multi: This is a multiline var value
with two lines.

<h3 id="unused-variables">Unused variables</h3>

Unused variables do not cause an error.

<h3 id="referring-to-variable-instances">Referring to variable instances</h3>

When you want to talk about .&dollar;varname, you need to use the HTML entity for $ instead of the $ sign itself (&amp;dollar;).
