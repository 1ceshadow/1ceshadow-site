---
title: window图形处理库
date: 2025-01-31 14:28:30
feed: hide
---
wingdi.h 是 Windows 图形设备接口（GDI）的头文件，主要提供了用于图形绘制、图像处理、字体管理等方面的功能。它本身并没有直接支持 PNG 格式，因为 GDI 的核心目的是为了支持 Windows 系统的基本图形功能，并不是专门设计来处理图像格式如 PNG 或 JPEG 的。
BMP 格式在 wingdi.h 中的支持

在 wingdi.h 中，Windows 提供了一些结构和函数来处理 BMP（位图）格式，最主要的是：

    BITMAP 结构：用于描述位图的基础信息。
    BITMAPINFO 结构：用于描述位图的颜色信息和格式。
    CreateDIBSection、GetDIBits、SetDIBits 等函数：这些函数可以用于创建、获取和设置 DIB（设备独立位图），其中也支持 BMP 格式的读取和写入。

PNG 格式的支持

Windows GDI 本身并不直接支持 PNG 格式，因此在 wingdi.h 中不会找到关于 PNG 格式的结构或函数。wingdi.h 主要关注的是更基础的图像处理（如 BMP、GDI 绘图等），而对于 PNG 和其他高级图像格式（如 JPEG、TIFF 等），你通常需要借助额外的库来处理。
如何处理 PNG 格式

虽然 wingdi.h 及其 GDI 并没有直接支持 PNG 格式，但你可以通过以下几种方式在 Windows 中处理 PNG 图像：
1. 使用 GDI+

GDI+ 是一个高级的图形库，提供了对多种图像格式的支持，包括 PNG。在 GDI+ 中，你可以使用 Bitmap 类加载和操作 PNG 图像。

    GDI+ 相关功能已经在 Windows 中内置，无需额外安装。
    你可以通过 Bitmap::FromFile() 或 Bitmap::FromStream() 来加载 PNG 图像。

GDI+ 示例代码：
```C
#include <windows.h>
#include <gdiplus.h>
```
using namespace Gdiplus;
```C
int main() {
    ULONG_PTR gdiplusToken;
    GdiplusStartupInput gdiPlusStartupInput;
    GdiplusStartup(&gdiplusToken, &gdiPlusStartupInput, NULL);

    // 加载PNG文件
    Bitmap* bitmap = Bitmap::FromFile(L"example.png");
    if (bitmap->GetLastStatus() == Ok) {
        // 处理图像
    }

    delete bitmap;
    GdiplusShutdown(gdiplusToken);
    return 0;
}
```

2. 使用 libpng 库

libpng 是一个专门用于读取和写入 PNG 格式的库，支持各种 PNG 相关的功能，如解码、编码、透明度处理等。如果你需要更底层的控制，或者你的程序需要在多个平台上运行，可以选择 libpng。

    你可以使用 libpng 库来读取、处理 PNG 图像，并进行更详细的操作。

libpng 示例代码：
```C
#include <stdio.h>
#include <png.h>

void read_png_file(const char *filename) {
    FILE *fp = fopen(filename, "rb");
    if (!fp) abort();

    png_structp png = png_create_read_struct(PNG_LIBPNG_VER_STRING, NULL, NULL, NULL);
    if (!png) abort();

    png_infop info = png_create_info_struct(png);
    if (!info) abort();

    if (setjmp(png_jmpbuf(png))) abort();

    png_init_io(png, fp);
    png_read_info(png, info);

    int width = png_get_image_width(png, info);
    int height = png_get_image_height(png, info);
    int bit_depth = png_get_bit_depth(png, info);
    int color_type = png_get_color_type(png, info);

    // 读取图像数据
    png_bytep row = (png_bytep) malloc(4 * width * sizeof(png_byte));
    for (int y = 0; y < height; y++) {
        png_read_row(png, row, NULL);
        // 处理每一行数据
    }

    // 清理资源
    png_destroy_read_struct(&png, &info, NULL);
    fclose(fp);
}

int main() {
    read_png_file("example.png");
    return 0;
}
```
总结

    wingdi.h：只提供了对 BMP 图像格式的支持，并没有关于 PNG 格式的任何内容。
    GDI+：Windows 提供的更高级的图形库，支持 PNG 格式，可以直接用于加载、保存和操作 PNG 图像。
    libpng：如果你需要处理 PNG 图像格式并且希望有更多控制，建议使用 libpng，这是一个专门用于处理 PNG 格式的库。

对于 PNG 图像处理，最推荐的方式是使用 GDI+（对于 Windows 平台）或者 libpng（跨平台）。