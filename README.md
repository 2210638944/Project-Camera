# 项目相机（Project Camera）

一个原生 Android（Kotlin + Jetpack Compose + CameraX）项目照片管理应用：以项目为组织单元拍照、打水印、导出 PDF/ZIP。

## 功能

- **项目树**：首页创建项目，项目内可无限创建子项目
- **拍照与水印**：项目内进入相机拍摄，可勾选水印（项目名 / 日期时间 / 位置 / 经纬度，可组合、可调位置与字号、带文字阴影）；可勾选拍照压缩（JPEG 质量 85，体积更小）
- **相册**：项目内浏览照片、滑动翻页、删除、分享
- **导出**：选中项目生成 PDF（该项目下图片一页一张，不动子项目）或 ZIP（含所有子目录图片）
- **导出/分享**：导出到 存储根目录/项目相机/ 专属目录，可打开目录；或分享到微信、QQ 等主流平台
- **设置**：水印参数、水印样式、存储目录入口、版本号

## 存储结构

```
存储根目录/
└── 项目相机/
    ├── 项目A/
    │   ├── IMG_xxxx.jpg
    │   └── 子项目A1/
    │       └── IMG_xxxx.jpg
    ├── PDF/          # 导出的 PDF
    └── ZIP/          # 导出的 ZIP
```

## 技术栈

- Kotlin 1.9+ / Jetpack Compose（Material 3）
- Android CameraX（预览 / 拍摄）
- 水印使用 Canvas 直接烧录进照片
- PDF 生成使用系统 `android.graphics.pdf.PdfDocument`，ZIP 使用 `java.util.zip`（无第三方依赖）

## 构建

环境要求：JDK 17、Android SDK（compileSdk 35）。

```bash
# 使用仓库自带 wrapper
./gradlew assembleDebug
# 产物：app/build/outputs/apk/debug/app-debug.apk
```

## 权限说明

- 相机：拍摄
- 定位（可选）：水印中的位置 / 经纬度信息
- 所有文件访问（Android 11+）：照片与导出文件存放在存储根目录的专属目录 `/项目相机/`
- 拍摄照片后同时写入系统相册

## 版本

- 1.4.0：拍照压缩开关；版本号统一由 BuildConfig 输出；移除 DocumentsProvider（修复启动闪退）
- 1.3.2：二分测试版（临时移除文档提供器）
- 1.3.0：存储目录可点击打开；导出后「打开目录」；图标缩小
- 1.2.0：新应用图标（浅色清新风格）
- 1.1.0：存储位置移至存储根目录；状态栏适配；导出后可打开目录
- 1.0.0：首个可用版本

## 开源协议

MIT
