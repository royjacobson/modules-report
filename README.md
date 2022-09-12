# C++20 Modules Status Report

"When can we begin to use modules?"

This document reports about the state of the ongoing effort to use C++20's modules across the C++ ecosystem - compilers, build systems, and (currently almost non-existent) libraries.

This document references a lot of work in progress, and will hopefully get outdated fast - so PRs to update and expand this document are very welcome.

## Compilers Support

### MSVC
MSVC have a complete implementation of modules, and work to support C++23's 
`import std` is ongoing [here](https://github.com/microsoft/STL/issues/2930).

See [here](https://developercommunity.visualstudio.com/search?space=62&q=modules&stateGroup=active&sort=votes) for a list of reported compiler modules bugs.

### GCC
GCC has some support for modules, but it seems to still be pretty buggy and progress has pretty much stalled. See [here](https://gcc.gnu.org/projects/cxx-status.html#cxx20) for the state of the module papers and [here](https://gcc.gnu.org/bugzilla/show_bug.cgi?id=103524) for a list of reported bugs in the current implementation.

### Clang
Work on Clang C++20 modules support is ongoing. See [here](https://clang.llvm.org/cxx_status.html#cxx20) for the state of module papers and [here](https://github.com/llvm/llvm-project/issues?q=is%3Aissue+is%3Aopen+label%3Aclang%3Amodules) for module related issues.

[This](https://github.com/ChuanqiXu9/stdmodules) project explores modularizing libc++ with Clang.

## Build Systems

### CMake
There's been some recent progress. You can see changes relevant to modules [here](https://gitlab.kitware.com/cmake/cmake/-/merge_requests?scope=all&state=all&label_name[]=area%3Acxxmodules), and  [this](https://gitlab.kitware.com/cmake/cmake/-/issues/18355) is the relevant gitlab issue with some interesting discussions.

[This](https://www.youtube.com/watch?v=hkefPcWySzI) recent talk details the goals of the CMake modules support.

### Bazel
Relevant bazel issue is [here](https://github.com/bazelbuild/bazel/issues/4005).

[rules_ll](https://github.com/eomii/rules_ll) have support for compiling modules with Bazel + Clang. [This](https://github.com/rnburn/rules_cc_module) is another Bazel modules attempt that targets Clang.

### MSBuild
Should work (in Visual Studio).

### Meson
Pretty old blogpost [here](https://nibblestew.blogspot.com/2020/11/adding-very-preliminary-support-for-c.html).

## Standardization

The modules related discussions in WG21 happen in 'SG15', the committee's study group dedicated to C++ tooling. Its mailing list archive is open and available [here](https://lists.isocpp.org/sg15).

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