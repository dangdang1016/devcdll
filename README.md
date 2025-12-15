# 🚀 Windows DLL 動態載入範例 (Dev-C++ 編寫)

本專案是一個使用 Dev-C++ 環境編寫的完整 Windows DLL 及其主應用程式動態載入的範例。

## 🌟 專案概述

這個範例演示了 **Run-time Dynamic Linking** (執行時動態連結)，即主程式在運行時才載入 DLL，並透過函式名稱查找並呼叫其功能。



### 關鍵技術點

* **DLL 匯出**: 使用 `__declspec(dllexport)` 在 `dll.h` 和 `dll.c` 中定義 `HelloWorld()` 函式。
* **動態載入**: 使用 Windows API 中的 `LoadLibrary`、`GetProcAddress` 和 `FreeLibrary` 實現執行時連結。
* **功能**: 彈出一個標題為 "Hi" 的 Windows 訊息框。

---

## 📁 檔案結構與程式碼

### 1. `dll.h` (DLL 介面定義)

定義了匯出/匯入宏和 `HelloWorld` 函式原型。

```c
#ifndef _DLL_H_
#define _DLL_H_

#if BUILDING_DLL
#define DLLIMPORT __declspec(dllexport)
#else
#define DLLIMPORT __declspec(dllimport)
#endif

// 匯出函式原型
DLLIMPORT void HelloWorld();

#endif
```










2. dll.c (DLL 函式實作與 DllMain)

這段程式碼包含 HelloWorld() 的實作和 DllMain 進入點。







```c


/* Replace "dll.h" with the name of your header */
#include "dll.h"
#include <windows.h>

DLLIMPORT void HelloWorld()
{
    // 透過 Windows API 彈出訊息框
    MessageBox(0,"Hello World from DLL!\n","Hi",MB_ICONINFORMATION);
}

BOOL WINAPI DllMain(HINSTANCE hinstDLL,DWORD fdwReason,LPVOID lpvReserved)
{
    // DllMain 處理 DLL 的初始化和清理事件
    switch(fdwReason)
    {
        case DLL_PROCESS_ATTACH:
        case DLL_PROCESS_DETACH:
        case DLL_THREAD_ATTACH:
        case DLL_THREAD_DETACH:
            break;
    }
    return TRUE;
}
```
