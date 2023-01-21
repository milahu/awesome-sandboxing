# awesome-sandboxing

sandboxing of untrusted code

focus on small languages = small runtime size.
ignoring [#large runtimes](#large-runtimes)

example codes: http client

other criteria: popularity, developer experience (debugging, interactive programming, ...)

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

https://v8.dev/docs/untrusted-code-mitigations

<blockquote>

Sandbox untrusted execution in a separate process

If you execute untrusted JavaScript and WebAssembly code in a separate process from any sensitive data, the potential impact of SSCA is greatly reduced. Through process isolation, SSCA attacks are only able to observe data that is sandboxed inside the same process along with the executing code, and not data from other processes.

Consider tuning your offered high-precision timers

A high-precision timer makes it easier to observe side channels in the SSCA vulnerability. If your product offers high-precision timers that can be accessed by untrusted JavaScript or WebAssembly code, consider making these timers more coarse or adding jitter to them.

</blockquote>

see also

- https://pwnisher.gitlab.io/nodejs/sandbox/2019/02/21/sandboxing-nodejs-is-hard.html
- https://stackoverflow.com/questions/7446729/how-to-run-user-submitted-scripts-securely-in-a-node-js-sandbox
- https://stackoverflow.com/questions/10937870/how-to-run-untrusted-code-serverside
- https://stackoverflow.com/questions/45767337/running-untrusted-javascript-code-on-server-in-sandbox
- https://github.com/fulcrumapp/v8-sandbox/blob/main/src/sandbox.cc
- https://github.com/gf3/sandbox embeds a JavaScript interpreter in the library which executes code in a separate context in another thread. based on the [Boa](https://github.com/boa-dev/boa) JavaScript interpreter, written in Rust
- https://www.figma.com/blog/how-we-built-the-figma-plugin-system/ compiling a JavaScript VM written in C to WebAssembly
- https://www.freecodecamp.org/news/running-untrusted-javascript-as-a-saas-is-hard-this-is-how-i-tamed-the-demons-973870f76e1c/ nodejs in Docker container
- https://github.com/milahu/awesome-javascript-interpreters

#### deno

typescript interpreter, based on V8 javascript engine

https://github.com/denoland/deno/issues/6447 Deno should have a maximum sandbox mode

#### quickjs

https://github.com/bellard/quickjs

A small embedded JavaScript interpreter that implements almost all of ES2019 and much of ES2020.

#### boa

https://github.com/boa-dev/boa

Boa is an embeddable and experimental Javascript engine written in Rust. Currently, it has support for some of the language.

#### duktape

https://github.com/svaarala/duktape

### clojure

https://rosettacode.org/wiki/HTTP#Clojure

```clj
(print (slurp "http://www.rosettacode.org/"))
```

- https://github.com/WillDetlor/TinyClojure
- https://github.com/chr15m/awesome-clojure-likes
- https://github.com/bakpakin/Fennel - Fennel is a lisp that compiles to Lua. It aims to be easy to use, expressive, and has almost zero overhead compared to writing Lua directly.

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

https://gitlab.com/nuald-grp/embedded-langs-footprint

```squirrel
function fn() {
  return "Hello, " + read();
}
```

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

https://softwareengineering.stackexchange.com/questions/191623/best-practices-for-execution-of-untrusted-code

<blockquote>

Python sandboxing is hard. Python is inherently introspectable, at multiple levels.

This also means that you can find the factory methods for specific types from those types themselves, and construct new low-level objects, which will be run directly by the interpreter without limitation.

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

python for microcontrollers

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

### wasm

https://news.ycombinator.com/item?id=18279635 WebAssembly’s post-MVP future

> I agree that WASM is only really interested for embedding untrusted code, but am not sure that the browser is the only place where you need that. A good example is Cloudflare's workers

https://stackoverflow.com/questions/61709122/can-i-use-webassembly-to-safely-execute-untrusted-user-code-within-my-web-app

## large runtimes

- java
- dotnet
- common lisp
- smalltalk
- erlang
- babashka https://github.com/babashka/babashka - Babashka is a native Clojure interpreter for scripting with fast startup.

## see also

- https://github.com/dbohdan/embedded-scripting-languages - A list of embedded scripting languages
- https://gitlab.com/nuald-grp/embedded-langs-footprint
- https://github.com/seifreed/awesome-sandbox-evasion
- https://www.reddit.com/r/ProgrammingLanguages/comments/7poi8q/should_an_embeddable_scripting_language_support/
- https://xkcd.com/2044/ Sandboxing Cycle
- https://www.reddit.com/r/rust/comments/eh73wx/safe_interpreted_language_to_embed_untrusted_code/
   - https://github.com/rust-unofficial/awesome-rust#scripting
