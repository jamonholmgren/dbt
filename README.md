Analizaruptor
-------------

Analizaruptor is a tool that looks for `break`, `require`, and `provides`
commands (and does a *teensy* bit of code analyzing (`/(class|module)\s*(\w`)/`)
to provide some defaults) to make your RubyMotion `Rakefile` and `debugger_cmds`
files short and consistent.

**CAUTION**: It overwrites the `debugger_cmds` file!

To use, include this gem (`gem 'analizaruptor'`), and add `app.analyze` to your
`Rakefile`, after you have added your libraries and whatnot.  In your source
code you can add Analizaruptor commands

```ruby
#----> provides Foo
#----> requires Bar
def method
#----> break
end
```

And those will be translated into directives for `app.files_dependencies` and
`debugger_cmds`.

Run `rake` or `rake debug=1`, and off you go!

The syntax for a command is:

```regex
^#--+> *(break|require|provides)( *(\w+|[0-9]+))?$
```

If a line number is given to the `break` command, a breakpoint will be added at
that line, otherwise it will be added to the line below `break`.  It's better to
insert the `#--> break` where you NEED it, rather than hardcode line numbers.
Line numbers are not constant.
