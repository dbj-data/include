
![wip](media/work_in_progres_raw.jpg)

<h4> This is **NOT** VS Code Multi Root Workspace </h4>

<h1> This readme and everything in here is: W.I.P. </h1>

## Back to the Common Header

- The common "stuff" is not repeated "all around the place", in all the "single headers"
- Opposite to the "single header" philosophy. Here we are following the "common headers" philosophy
- This is where "machine wide" includes are.

### The Management

- The development also happens in these many folders and that means a lot of cruft. Potentially.
- Be careful not to develop in the master branch
- Be careful to use the master branch when including

In case you especially want something from here please do mention it in issues and we might focus on your needs. Hint: if you are persuasive :wink:

---
## DBJ_CAPI / DBJ_CPP
- Currently, "two headed" code organization: `DBJ_CAPI` and `DBJ_CPP` are to be on the logical top of all  includes. 
- But. The firm roadmap is
to have a single top and that is to be: **DBJ_CAPI** .

## For C++ Aficionados

We use C++ in a non-standard form: no exceptions, no iostreams, no RTTI, no type_traits shenanigans, no `system_error`, no meta programming and all the other C++ things you love and loathe.
 
MS STL can be built and used in a so called "kernel" mode. That is a *"big deal"*. That means non standard C++ and non standard std lib, are delivered and maintained by Microsoft.
 
- No C++ exceptions, and no RTTI
- "kernel" mode does require using the cl.exe `/kernel` switch. 
- `CPP_UNWIND` is undefined if cl.exe switch `/DNO_EXCEPTIONS=1` is used
  - see it in `<vcruntime.h>` in action.
- Also keywords: `try`,`throw` and `switch` are rendered non-existent
- [RTTI](https://docs.microsoft.com/en-us/cpp/build/reference/gr-enable-run-time-type-information?view=msvc-160) is switched off by using `/GR-` cl.exe switch

## Building 

- For building we use most often Visual Studio as IDE and clang-cl as a compiler. 
- When we use VS Code we prefer simple bat files for building
  - VS Code has trouble finding and using clang-cl.exe

### Linking

For every "MACHINE_WIDE" stuff, if there are lib's or dll's they are in `~\MACHINE_WIDE\lib`. 
- Perhaps you might add it to your [`/LIBPATH`](https://docs.microsoft.com/en-us/cpp/build/reference/libpath-additional-libpath?view=msvc-160). For happy Visual Studio building (clang-cl or cl) 
  - please place your lib's after the `/linker` switch.

### DBJ_MACHINE_WIDE envvar

- Not in use
- We are aiming for this to be the only user environment variable one might need to use DBJ stuff, "machine wide". 
- We will set it to the devlr machine location of the "machine_wide" repo.
  - for example ours is: `D:\\machine_wide;`
  - Important: notice the semicolon at the end of it.
    - above is a location from our DEVL machines
    - If your machines do not have the D drive, you might use the `subst` command to "make fake" `D:` drive
      - Perfectly legal and useful.
- Please add the `%DBJ_MACHINE_WIDE%` to the PATH user environment variable

> We use and recommend [Rapid Environment Editor](https://www.rapidee.com/en/about)



---
# APPENDIX

## Why or Why Not is something in here

It all depends how fast "something" in the code, has proven itself, or not. Generaly everything goes through [dbj-bench](https://github.com/dbj-data/dbj-bench) before being accepted.

dbj-bench is built with Visual Studio and it has pretty wide variety of builds. That is not simple. Again the sole purpose is to try and develop very precise benchmarking.

## We need to talk about WIL

[WIL](https://github.com/microsoft/wil) is a treasure trove for anyone using all sorts of realy important WIndows API's. In some pleaces it is using reallu low level legacy stuf (MS RPC), or complex stuff (COM).

WIL is also very revealing on what MSFT top programers think of many thigs you also think about. Like for example `stl.h`. Therefore take some time and think whayt is NOT inside and what is inside.

But "things" will be definitely and regularly "nicked" from WIL and transformed to some dbj win32 internals.