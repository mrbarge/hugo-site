---
title: "Shells, pipes and precedence"
date: 2020-04-25T14:45:38+10:00
draft: false
categories:
  - Coding
tags:
  - shell scripting
  - bash
  - linux
images:
  - https://bargenqua.st/img/bashpipe.png
thumbnail: "/img/bashpipe.png"
---

A fun distraction occurred this week when the following snippet of `bash` code was suggested in a pull request (simplified for demonstrative clarity):

```bash {linenos=inline}
if [ echo $VAR1 | grep -q "text" ] || [ $VAR2 -eq 0 ]; then
   echo "If test passed."
else
   echo "If test failed."
fi   
```

Taken at initial face value, it looked like it should work okay. There didn't appear to be anything immediately wrong with its syntax. But upon execution, it resulted in a syntax error:

```bash {linenos=inline}
-bash: [: missing `]
grep: ]: No such file or directory
```

So what's going on here? After all, the following is quite valid:

```bash {linenos=inline}
if [ true ] || [ false ]; then
   echo "If test passed."
fi
```

Well, as you've probably guessed from comparing the two examples (if not the header of this very article), the difference is the presence of the pipeline.

When we're talking `sh` (shell) grammar,  the `if` conditional block belongs to a category known as `compound commands`. Pipelines, as it turns out, take higher precedence in parsing order than compound commands, and this subsequently affects how `bash` interprets the whole statement.

If pipelines do take precedence, then `bash` will treat 

```bash
if [ echo $VAR1
```

as a command, and 

```bash
grep -q "text" ] || [ $VAR2 -eq 0 ]; then ...
```

as a command. Now that we know this, the errors make more sense. The leading `"missing ]"` error is because the first command does indeed have a missing closing bracket. The second `"grep: ]: No such file or directory"` error is because `bash` is passing `grep` the `"]"` as an argument.

So where can we find out more about the way shell grammar is parsed? The authoritative list is the [Shell Grammar Rules](https://pubs.opengroup.org/onlinepubs/009695299/utilities/xcu_chap02.html) documentation. Looking specifically at pipelines, we see:

* A `pipeline` can be made up of `pipe_sequence`s.
```bash
pipeline         :      pipe_sequence
```

* A `pipe_sequence` can be made up of a `command`, or more `pipe_sequence`s.
```bash
pipe_sequence    :                             command
                 | pipe_sequence '|' linebreak command
```

* A `command` can be made up of `compound_command`s.

```bash
command          : compound_command
```

* And a `compound_command` can be made up of `if_clause`s.

```bash
compound_command : ...
                 | if_clause
```

So back to the original topic, how should we fix the suggestion? Well, there's probably many ways. I would opt to simplify the `if` conditional and determine the result of the `grep` prior:

```bash {linenos=inline}
VAR1_TEST=$(echo $VAR1 | grep -q "test")
VAR1_RC=$?
if [ $VAR1_RC -eq 0 ] || [ $VAR2 -eq 0 ]; then
...
```

However, in this specific case, we could also make use of the bash `=~` operator to apply a regex test against `$VAR1` instead.

```bash {linenos=inline}
if [[ $VAR1 =~ "test" ]] || [ $VAR2 -eq 0 ]; then
...
```

Now you might be wondering - why did we use `[[` and `]]` here, and why not single brackets? Well, using the double-brackets enables more functionality - including the very `=~` operator used in this test. There's a good write-up of the differences [on this site](http://mywiki.wooledge.org/BashFAQ/031).

