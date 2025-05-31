# SchoolAppsUpdate
为学校统一配置的云电脑提供的常用程序快速更新服务

## 目录
1. [开发原因](/#开发原因)
2. [快速使用](/#快速使用)
3. [私有化部署](/#私有化部署)
4. [免费托管服务](/#免费托管服务)
5. [希沃一体机常用教学软件下载目录](/#希沃一体机常用教学软件下载目录)

## 开发原因
部分学校的办公电脑采用的是配置低、运行速度慢的云电脑，运行一些办公软件（如 QQ 、微信等）的最新版本将会严重拖慢系统速度，造成卡顿。一部分地区的学校信息化普及时间较晚，存在老教师不会操作的问题。

SchoolAppsUpdate 项目旨在帮助这些学校搭建可快速分发的软件安装页面，减少安装问题。

## 快速使用
> 仍然建议您使用定制版本，快速使用版本为通用的展示版本，更新极慢。
- [快速使用](fastuse.html)

## 私有化部署
⚠ 此教程使用的代码包含内核较低的浏览器无法显示的 css 样式，如果您所在的学校电脑默认浏览器无法正常显示快速使用版本的页面，请您先尝试[检查浏览器内核](https://check.retiehe.com)并通过更换浏览器的方式解决。若无法解决，请您尝试将教程代码交给 AI 修改为兼容低版本浏览器的代码，**当然，我们不推荐您这样做**。

以下是快速使用版本的标准模板：
```html
<!DOCTYPE html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>应用更新</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css" rel="stylesheet">
    <style>
        /* 禁止用户复制 */
        body {
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
            user-select: none;
        }
    </style>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#0078D4',
                        secondary: '#6B7280',
                        accent: '#3B82F6',
                        neutral: '#F3F4F6',
                        'neutral-dark': '#1F2937',
                    },
                    fontFamily: {
                        inter: ['Inter', 'sans-serif'],
                    },
                    boxShadow: {
                        'card': '0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06)',
                        'card-hover': '0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05)',
                    }
                },
            }
        }
    </script>
    <style type="text/tailwindcss">
        @layer utilities {
            .content-auto {
                content-visibility: auto;
            }
            .card-transition {
                transition: all 0.3s ease;
            }
        }
    </style>
</head>

<body class="bg-gray-50 dark:bg-gray-900 min-h-screen font-inter">
    <div class="container mx-auto px-4 py-8 max-w-7xl">
        <!-- 标题栏 -->
        <header class="mb-8">
            <h1 class="text-[clamp(1.5rem,3vw,2.5rem)] font-bold text-gray-800 dark:text-white text-center">应用更新中心</h1>
            <p id="SID" class="text-sm text-gray-500 dark:text-gray-400 mt-1 text-center">Unknown SID</p>
        </header>

        <br>

        <!-- 集控组件 -->
        <div class="bg-white dark:bg-gray-800 rounded-xl shadow-card card-transition p-6">
            <div class="flex items-start">
                <div
                    class="bg-purple-100 dark:bg-purple-900/30 p-3 rounded-lg mr-4 w-14 h-14 flex items-center justify-center">
                    <i class="fa-solid fa-server text-3xl text-purple-500 dark:text-purple-400"></i>
                </div>
                <div class="flex-1">
                    <h2 class="text-xl font-semibold text-gray-800 dark:text-white">集控管理</h2>
                    <p class="text-sm text-gray-500 dark:text-gray-400 mt-1"><span id="SSID">未知校区</span></p>
                    <p id="ERROR" class="text-sm text-red-500 dark:text-red-400 mt-1"><strong>集控 SID 文件缺失，请联系服务管理员</strong></p>
                </div>
            </div>
        </div>

        <br>

        <!-- 应用小组件网格 -->
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">

            <!-- QQ 稳定版应用小组件 -->
            <div class="bg-white dark:bg-gray-800 rounded-xl shadow-card card-transition p-6">
                <div class="flex items-start">
                    <div
                        class="bg-blue-100 dark:bg-blue-900/30 p-3 rounded-lg mr-4 w-14 h-14 flex items-center justify-center">
                        <i class="fa-brands fa-qq text-3xl text-blue-500 dark:text-blue-400"></i>
                    </div>
                    <div class="flex-1">
                        <h2 class="text-xl font-semibold text-gray-800 dark:text-white">QQ电脑版（办公稳定版）</h2>
                        <p class="text-sm text-gray-500 dark:text-gray-400 mt-1">最新版本: <span
                               id="qqwd-code" class="font-medium">Unknown</span></p>
                        <a id="update-link-qqwd" href="#" target="_blank"
                            class="mt-4 bg-primary hover:bg-primary/90 text-white px-4 py-1.5 rounded-lg transition-all duration-200 flex items-center justify-center w-auto inline-flex">
                            <i class="fa-solid fa-download mr-2"></i>
                            <span>下载最新版本</span>
                        </a>
                    </div>
                </div>
            </div>

            <!-- QQ 应用小组件 -->
            <div class="bg-white dark:bg-gray-800 rounded-xl shadow-card card-transition p-6">
                <div class="flex items-start">
                    <div
                        class="bg-blue-100 dark:bg-blue-900/30 p-3 rounded-lg mr-4 w-14 h-14 flex items-center justify-center">
                        <i class="fa-brands fa-qq text-3xl text-blue-500 dark:text-blue-400"></i>
                    </div>
                    <div class="flex-1">
                        <h2 class="text-xl font-semibold text-gray-800 dark:text-white">QQ电脑版（最新版）</h2>
                        <p class="text-sm text-gray-500 dark:text-gray-400 mt-1">最新版本: <span
                                 id="qq-code" class="font-medium">Unknown</span></p>
                        <a id="update-link-qq" href="#" target="_blank"
                            class="mt-4 bg-primary hover:bg-primary/90 text-white px-4 py-1.5 rounded-lg transition-all duration-200 flex items-center justify-center w-auto inline-flex">
                            <i class="fa-solid fa-download mr-2"></i>
                            <span>下载最新版本</span>
                        </a>
                    </div>
                </div>
            </div>

            <!-- 微信应用小组件 -->
            <div class="bg-white dark:bg-gray-800 rounded-xl shadow-card card-transition p-6">
                <div class="flex items-start">
                    <div
                        class="bg-green-100 dark:bg-green-900/30 p-3 rounded-lg mr-4 w-14 h-14 flex items-center justify-center">
                        <i class="fa-brands fa-weixin text-3xl text-green-500 dark:text-green-400"></i>
                    </div>
                    <div class="flex-1">
                        <h2 class="text-xl font-semibold text-gray-800 dark:text-white">微信电脑版</h2>
                        <p class="text-sm text-gray-500 dark:text-gray-400 mt-1">最新版本: <span
                                id="weixin-code" class="font-medium">Unknown</span></p>
                        <a id="update-link-wechat" href="#" target="_blank"
                            class="mt-4 bg-primary hover:bg-primary/90 text-white px-4 py-1.5 rounded-lg transition-all duration-200 flex items-center justify-center w-auto inline-flex">
                            <i class="fa-solid fa-download mr-2"></i>
                            <span>下载最新版本</span>
                        </a>
                    </div>
                </div>
            </div>

            <!-- 占位小组件 -->
            <div
                class="bg-white dark:bg-gray-800 rounded-xl shadow-card card-transition p-6 border-2 border-dashed border-gray-200 dark:border-gray-700 flex flex-col items-center justify-center">
                <h3 class="text-lg font-medium text-gray-500 dark:text-gray-400">更多应用正在适配</h3>
                <p class="text-sm text-gray-400 dark:text-gray-500 mt-1 text-center">我们正在努力加入更多应用</p>
            </div>
        </div>

        <!-- 底部信息 -->
        <footer class="mt-12 text-center text-gray-500 dark:text-gray-400 text-sm">
            <div class="bg-white dark:bg-gray-800 rounded-xl shadow-card card-transition p-6">
                <h3 class="text-lg font-medium text-gray-500 dark:text-gray-400">更新时间<br><span id="Update-time">NaN</span></h3>
                <p class="text-sm text-gray-400 dark:text-gray-500 mt-1 text-center">© <span id="year"></span> 邵阳市第一中学信息技术社团</p>
                <p class="text-sm text-gray-400 dark:text-gray-500 mt-1 text-center">邵阳市第一中学校园公共服务提供服务支持</p>
            </div>
        </footer>
    </div>

    <script src="https://sysyzspublic.rth1.xyz/host/SID/fastuse.js"></script>
    <script>
        // 动态设置年份
        document.getElementById('year').textContent = new Date().getFullYear();
    </script>
</body>

</html>
```

您可以看到，在代码底部引入了一个外部 JS 文件：

```html
<script src="https://sysyzspublic.rth1.xyz/host/SID/fastuse.js"></script>
```

此文件为集控文件（以下简称 "SID 文件" ）。

对此文件的标准格式如下：

```js
document.addEventListener('DOMContentLoaded', function () {
    const appLinks = {
        'update-link-qqwd': 'https://dldir1.qq.com/qqfile/qq/PCQQ9.7.23/QQ9.7.23.29406.exe',
        'update-link-qq': 'https://dldir1.qq.com/qqfile/qq/QQNT/Windows/QQ_9.9.19_250429_x64_01.exe',
        'update-link-wechat': 'https://pc.weixin.qq.com/'
    };

    const appVersionTexts = {
        'SID': '<span class="font-medium">FASTUSE</span>',
        'SSID': '此页面为快速服务的默认展示页面',
        'ERROR': '',
        'qq-code': '9.9.19.250429',
        'weixin-code': '3.9.5.11',
        'qqwd-code': '9.7.23.29406',
        'Update-time': '2025.05.09',
    };

    for (const [id, link] of Object.entries(appLinks)) {
        const element = document.getElementById(id);
        if (element) {
            element.href = link;
        }
    }

    for (const [id, text] of Object.entries(appVersionTexts)) {
        const element = document.getElementById(id);
        if (element) {
            element.innerHTML = text;
        }
    }
});
```

让我们逐步了解 SID 文件的各个部分定义：
- `appLinks`：应用实际下载地址，但使用者按下下载按钮时，将会下载该链接指向的文件。
- `appVersionTexts`：定义 APP 版本和页面的文字部分。
  - `SID`：集控序列号，当您同时管理多个不同年级的电脑时，可以通过此编码区分分发文件。
  - `SSID`：文本内容，可选设置。
  - `ERROR`：报错文本，默认不显示。当目标电脑的下载页面未正确引用 SID 文件时，页面将无法使用并报错。
  - `Update-time`：页脚的更新时间。
- 映射到 html 文件中的对应 ID

```js
for (const [id, link] of Object.entries(appLinks)) {
    const element = document.getElementById(id);
    if (element) {
        element.href = link;
    }
}

for (const [id, text] of Object.entries(appVersionTexts)) {
    const element = document.getElementById(id);
    if (element) {
        element.innerHTML = text;
    }
}
```

将上述两个文件放在可用的服务器或主机上并正确引用文件即可。

---- 私有化部署教程结束 ----

## 免费托管服务
> 免费托管服务页面的访问速度取决于您所在地区的网络速度。

若您所在的学校相关资源较为缺乏，可向我们寻求免费的页面托管服务。如有需要，请发送邮件到 [sysyzspublic@outlook.com](mailto:sysyzspublic@outlook.com) 。

## 希沃一体机常用教学软件下载目录
- [打开](./seewo/html)

<hr>

<div align="center">
<p align="center">© 2025 邵阳市第一中学信息技术社团</p>
<p align="center">邵阳市第一中学校园公共服务提供服务支持</p>
</div>
