# C++20 Modules Status Report

"When can we begin to use modules?"

This document reports about the state of the ongoing effort to use C++20's modules across the C++ ecosystem - compilers, build systems, and (currently almost non-existent) libraries.

This document references a lot of work in progress, and will hopefully get outdated fast - so PRs to update and expand this document are very welcome.

## Compilers Support

### MSVC
MSVC have a complete implementation of modules. Support of C++23's 
`import std` is has been merged to the STL and is expected to ship in VS2022 17.5, probably in early 2023.

See [here](https://developercommunity.visualstudio.com/search?space=62&q=modules&stateGroup=active&sort=votes) for a list of reported compiler modules bugs.

### GCC
GCC has some support for modules, but it seems to still be pretty buggy and progress has pretty much stalled until very recently (Sep 22). See [here](https://gcc.gnu.org/projects/cxx-status.html#cxx20) for the state of the module papers and [here](https://gcc.gnu.org/bugzilla/show_bug.cgi?id=103524) for a list of reported bugs in the current implementation.

### Clang
Work on Clang C++20 modules support is ongoing. See [here](https://clang.llvm.org/cxx_status.html#cxx20) for the state of module papers and [here](https://github.com/llvm/llvm-project/issues?q=is%3Aissue+is%3Aopen+label%3Aclang%3Amodules) for module related issues.

[This](https://github.com/ChuanqiXu9/stdmodules) project explores modularizing libc++ with Clang.

## Build Systems

### CMake
There's been some recent progress. You can see changes relevant to modules [here](https://gitlab.kitware.com/cmake/cmake/-/merge_requests?scope=all&state=all&label_name[]=area%3Acxxmodules), and  [this](https://gitlab.kitware.com/cmake/cmake/-/issues/18355) is the relevant gitlab issue with some interesting discussions.

The CMake strategy relies on the module scanning protocol from P1689R5, which means they rely on compiler support for this. There are GCC and Clang patches implementing this in preliminary review, but none of them are upstreamed yet. Until then only (very recent) MSVC will have this experimental CMake support.
A stub project for using CMake with MSVC is available [here](https://github.com/GabrielDosReis/cmake-for-modules).

[This](https://www.youtube.com/watch?v=hkefPcWySzI) recent talk details the goals of the CMake modules support.

### Bazel
Relevant bazel issue is [here](https://github.com/bazelbuild/bazel/issues/4005).

[rules_ll](https://github.com/eomii/rules_ll) have support for compiling modules with Bazel + Clang. [This](https://github.com/rnburn/rules_cc_module) is another Bazel modules attempt that targets Clang.

### MSBuild
Should work (in Visual Studio).

### Meson
Pretty old blogpost [here](https://nibblestew.blogspot.com/2020/11/adding-very-preliminary-support-for-c.html).

### Build2
Build2 supports building modules with GCC since the start of 2021. [This](https://build2.org/blog/build2-cxx20-modules-gcc.xhtml) blog post has details on how to use it, and there is a [repository](https://github.com/build2/cxx20-modules-examples) with various usage examples.

### xmake

xmake seem to have a pretty good support for modules with all the big-three compilers, having rolled out their own dependency discovery code. [Here's](https://github.com/xmake-io/xmake/tree/master/tests/projects/c%2B%2B/modules) a good place to find usage examples.

## Standardization

The modules related discussions in WG21 happen in 'SG15', the committee's study group dedicated to C++ tooling. Its mailing list archive is open and available [here](https://lists.isocpp.org/sg15).

## IDEs

### Visual Studio
As it is tightly integrated with MSVC and MSBuild, Visual Studio can be expected to work quite well with C++ modules. However, since IntelliSense is running
with a different compiler frontend (EDG), it is not always up to par with MSVC in this regard.

### CLion
CLion have [anounced coming support](https://blog.jetbrains.com/clion/2022/10/clion-2022-3-eap-cpp20-modules-now-supported/) for C++ modules in their upcoming 2022.3 edition.

## Libraries

### fmtlib
[fmtlib]() supports modules, but only on windows.

### Boost
There was a discussion about modules in boost in April [on their mailing list](https://lists.boost.org/Archives/boost/2022/04/252629.php). Currently there seem to be no progress in this direction.

### async_simple
There's a development branch that uses modules [here](https://github.com/alibaba/async_simple/tree/CXX20Modules), usable in Clang 15.

## Usage Examples

### LibTwo
LibTwo makes some usage of modules, particularly importing some third-party dependencies
as modules [here](https://github.com/hugoam/two/tree/master/src/3rdparty).

### HiveWE
The open source [HiveWE](https://github.com/stijnherfst/HiveWE) uses modules and has some practical examples.

## Blogposts

* [C++20 modules with GCC11 by Niall Cooling](https://blog.feabhas.com/2021/08/c20-modules-with-gcc11)
* [Moving a project to C++ named Modules - Cameron DaCamara](https://devblogs.microsoft.com/cppblog/moving-a-project-to-cpp-named-modules/)
* [C++20 modules with Clang - Eduardo Costa](https://blog.ecosta.dev/en/tech/cpp-modules-with-clang)
* [Integrating C++ header units into Office using MSVC (1/n) - Cameron DaCamara & Zachary Henkel](https://devblogs.microsoft.com/cppblog/integrating-c-header-units-into-office-using-msvc-1-n/)
