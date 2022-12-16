---
title: 论使用python和WebAssembly重写scratch编译器
date: 2022-10-05 08:14:52
tags: 
- python
- scratch
- C++
- SDL
- WebAssembly
categories: 
- 编程
---

scratch最大的缺陷就是性能及其拉跨，自从有了Evoluted-Scratch,Turbowarp, leopard-js等jit编译器，这个问题得到了一部分的解决。但是并没有使scratch的性能与其他语言接近，所以我认为可以用WASM来写scratch编译器，或许能最大程度提升scratch的运行速度。

目前使用python来写编译器的核心部分，编译器会将project.json和assets编译成C++(使用SDL作为渲染引擎)，再使用Emscripten将C++编译成WASM。

在BlockAssembly中，所有的积木都是scratch3.0包含的标准积木，但是可以通过一个类似core.js的"标准编译器", 将clipcc, ccw, acamp等平台的特殊积木编译成标准积木。也可以更方便的编写扩展库，只需要一个json文件就能将block和code对应起来，编写成一个模块。也可以使用scratch积木轻松编写模块。

使用SDL和WASM的好处是，一样的代码能在不同的平台运行，(Andriod, IOS, Mac, Windows, Web等等)，scratch程序就可以轻松的打包到不同的平台。SDL后端使用OpenGL渲染，能稳定的达到浏览器支持的最高帧数。

最后，Github项目地址: [BlockAssembly](https://github.com/LuminousWL/BlockAssembly)