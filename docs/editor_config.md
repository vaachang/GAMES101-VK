# Zed配置
## Windows
需要安装mingw用于编译C/C++，vcpkg用于包管理。

Zed配置文件如下：

.zed/debug.json

```
[
  {
    "label": "Make And Debug",
    "build": {
      "command": "mingw32-make",
      "args": ["-C", "build"]
    },
    "program": "build/vkTest/vkTest.exe",
    "request": "launch",
    "adapter": "CodeLLDB",
    "cwd": "build/vkTest"
  }
]

```

.zed/settings.json

```
{
  "lsp": {
      "clangd": {
        "binary": {
          "arguments": ["--compile-commands-dir=$ZED_DIRNAME/build"]
        }
      }
  }
}
```

.zed/tasks.json

```
[
  {
    "label": "CMAKE Build",
    "command": "cmake",
    "args": [
      "-G",
      "'MinGW Makefiles'",
      "-S",
      "$ZED_DIRNAME",
      "-B",
      "$ZED_DIRNAME/build",
      "-DCMAKE_TOOLCHAIN_FILE",
      "$VCPKG_ROOT/scripts/buildsystems/vcpkg.cmake"
    ],
    "use_new_terminal": false,
    "allow_concurrent_runs": false,
    "reveal": "always",
    "reveal_target": "dock",
    "hide": "never",
    "shell": "system"
  }
]

```

另外，需要配置文件.clangd

```
CompileFlags:
  Add:
    - --target=x86_64-w64-windows-gnu

```

## Linux
需要安装Ninja

.zed/debug.json

```
[
  {
    "label": "Make And Debug",
    "build": {
      "command": "ninja",
      "args": ["-C", "build"]
    },
    "program": "build/vkTest/vkTest",
    "request": "launch",
    "adapter": "CodeLLDB",
    "cwd": "build/vkTest"
  }
]

```

.zed/settings.json

```
{
  "lsp": {
    "clangd": {
      "binary": {
        "arguments": ["--compile-commands-dir=$ZED_DIRNAME/build"]
      }
    }
  }
}
```

.zed/tasks.json

```
[
  {
    "label": "CMake Build",
    "command": "cmake",
    "args": [
      "-G",
      "Ninja",
      "-S",
      "$ZED_DIRNAME",
      "-B",
      "$ZED_DIRNAME/build"
    ],
    "use_new_terminal": false,
    "allow_concurrent_runs": false,
    "reveal": "always",
    "reveal_target": "dock",
    "hide": "never",
    "shell": "system"
  }
]

```
