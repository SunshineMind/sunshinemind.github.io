---
date: '2026-01-15T23:56:18+08:00'
draft: false
title: '奇怪的修复 Unity WebGL 打包失败方法'
lastmod: 2026-01-21T00:51:00+08:00

categories:
- Unity
- 没啥技术含量文章

tags:
- WebGL
- 构建失败
---

>先说结论，关闭了XMP解决了Unity构建WebGL失败的问题，但我没有理解原因。


昨晚尝试在公司的电脑上使用Unity 6000.0.40f1 上构建一个WebGL应用失败。

出现错误

```
C:\Users\***\UnityProject\***>set MYDIR=C:\Program Files\Unity\Hub\Editor\6000.0.40f1\Editor\Data\PlaybackEngines\WebGLSupport\BuildTools\Emscripten\emscripten\ 

C:\Users\***\UnityProject\***>goto FOUND_MYDIR emcc: error: '"C:/Program Files/Unity/Hub/Editor/6000.0.40f1/Editor/Data/PlaybackEngines/WebGLSupport/BuildTools/Emscripten/binaryen\bin\wasm-opt" --strip-dwarf --signext-lowering --post-emscripten -O2 --low-memory-unused --zero-filled-memory --pass-arg=directize-initial-contents-immutable --strip-debug --strip-producers Library/Bee/artifacts/WebGL/build/debug_WebGL_wasm/build.wasm -o Library/Bee/artifacts/WebGL/build/debug_WebGL_wasm/build.wasm --mvp-features --enable-mutable-globals --enable-sign-ext' failed (returned 3221225477) UnityEditor.

EditorApplication:Internal_CallDelayFunctions ()
```

很奇怪，记得之前是可以正常构建WebGL app的。

不想思考，将报错信息交给ChatGPT。

根据ai反馈的可能原因逐一进行排查。

1. 删除缓存重试

    删除项目下Library目录整体，重启Unity重新生成，没用。

2. 杀毒软件防护/干扰

    这点排除，我的工作电脑只有windows defender。

3. 重装 WebGL Support Build

    这个我不想试，众所周知，UnityHub删除某一个组件非常麻烦，
    并且之前可以正常工作，这个问题可能性不高，先排除。

4. 重装修复VC++库

    vc库很全，并且之前可以正常工作，这个问题可能性不高，先排除。

5. CPU/内存不稳定

    诶呦，这个有意思。

    虽然我不是13/14代酷睿，但和巧合的是，在出现这个问题前，我确实在BIOS中开启了自动XMP。

    我的工作电脑出现了问题，做了一点简单的处理。修复之后，我进行了被恢复到默认的BIOS设置，在重新开启了处理器虚拟化之后，我顺手打开了XMP。

这下好了，难道是我开启XMP导致的？

直接重启电脑尝试处理，在BIOS中关闭XMP（顺便一提，这老华硕主板BIOS做的不错，XMP不用进高级选项就可以设置，开启就可以自动设置频率、电压等），保存，重启。

重新启动Unity，直接点击构建。

五分钟后...

成了！

我不懂但我大受震撼.png

就这样吧，没察觉到关掉或开启XMP对我的开发的影响，就这样一直关着吧，等我有机会了解“真相”再说吧😂。