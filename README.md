# awesome-sandboxing

sandboxing of untrusted code

focus on small languages = small runtime size.
ignoring [#large runtimes](#large-runtimes)

example codes: http client

## languages

### javascript

https://news.ycombinator.com/item?id=17021637 Excel Adds JavaScript and Power BI Support

<blockquote>

JavaScript, OTOH, is designed to support secure in-process sandboxing. Other languages with such support do exist (e.g. Lua), but JavaScript is by far the most widely known.

</blockquote>

https://rosettacode.org/wiki/HTTP#JavaScript

```js
main()

async function main() {
  const response = await fetch('http://rosettacode.org')
  const text = response.text()
  console.log(text)
}
```

#### deno

typescript interpreter, based on V8 javascript engine

https://github.com/denoland/deno/issues/6447 Deno should have a maximum sandbox mode

#### quickjs

https://github.com/bellard/quickjs

A small embedded JavaScript interpreter that implements almost all of ES2019 and much of ES2020.

### clojure

https://rosettacode.org/wiki/HTTP#Clojure

```clj
(print (slurp "http://www.rosettacode.org/"))
```

#### babashka

https://github.com/babashka/babashka

Babashka is a native Clojure interpreter for scripting with fast startup. Its main goal is to leverage Clojure in places where you would be using bash otherwise.

### tcl

https://rosettacode.org/wiki/HTTP#Tcl

```tcl
package require http
set request [http::geturl "http://www.rosettacode.org"]
puts [http::data $request]
http::cleanup $request
```

### Squirrel

"the better lua"

C-like syntax, stable performance

https://github.com/albertodemichelis/squirrel

https://computerscomputing.wordpress.com/2013/02/18/lua-and-squirrel-the-case-for-squirrel/

> In contrast to Lua, Squirrel uses a C-like syntax and supports classes, enums, constants, and attributes. It uses a mixed approach of automatic reference counting and garbage collection to manage memory.

> One of the most common issues facing game developers who embed Lua is the unpredictability of the garbage collector, which can affect real-time performance.

> Squirrel performs constant memory management through refcounting.

### lua

"The only reasonably safe way to handle untrusted Lua scripts is to isolate them in a process context".
http://lua-users.org/lists/lua-l/2011-02/msg01106.html

```lua
local http = require("socket.http")
local url = require("socket.url")
local page = http.request('http://www.google.com/m/search?q=' .. url.escape("lua"))
print(page)
```

quirks:

- no arrays, only maps ("tables")
- GC, unstable performance

https://stackoverflow.com/questions/1224708/how-can-i-create-a-secure-lua-sandbox

### python

https://news.ycombinator.com/item?id=17021637 Excel Adds JavaScript and Power BI Support

<blockquote>

One issue with embedding Python is that it's difficult to sandbox - to securely limit what the embedded runtime, and hence (potentially malicious) custom functions, can do:

> [The Python developers'] standard answer to "How do I sandbox Python code?" has been "Use a subprocess and the OS provided process sandboxing facilities" for quite some time. [1]

</blockquote>

https://rosettacode.org/wiki/HTTP#Python

```py
import urllib.request
response = urllib.request.urlopen("http://rosettacode.org")
text = response.read()
print(text)
```

### micropython

https://github.com/micropython/micropython

### scheme

#### chibi scheme

https://github.com/ashinn/chibi-scheme

#### chicken scheme

https://rosettacode.org/wiki/HTTP#Scheme

```scm
(use http-client) ; http://api.call-cc.org/doc/http-client
(print
  (with-input-from-request "http://google.com/"
                           #f read-string))
```

#### guile

## large runtimes

- java
- dotnet
- common lisp
- smalltalk
- erlang

## see also

- https://github.com/dbohdan/embedded-scripting-languages - A list of embedded scripting languages
- https://gitlab.com/nuald-grp/embedded-langs-footprint
- https://github.com/seifreed/awesome-sandbox-evasion
- https://www.reddit.com/r/ProgrammingLanguages/comments/7poi8q/should_an_embeddable_scripting_language_support/
- https://xkcd.com/2044/ Sandboxing Cycle
- https://www.reddit.com/r/rust/comments/eh73wx/safe_interpreted_language_to_embed_untrusted_code/
   - https://github.com/rust-unofficial/awesome-rust#scripting
   
