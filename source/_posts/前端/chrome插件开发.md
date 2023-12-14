---
title: Chrome浏览器插件开发
date: 2023-12-05 16:31:15
tags:
	- chrome
categories:
	- 前端
---

## chrome插件几大要素

1. manifest.json
`Manifest`文件是一个插件的元数据，它告诉Chrome插件的名称、描述、版本、权限以及其他插件需要的属性。下面是一个基本的Manifest.json文件:

```json
{
  "manifest_version": 2,
  "name": "My First Extension", // 插件名称
  "description": "This is a sample Chrome Extension", // 描述
  "version": "1.0", // 插件版本
  "icons": {
    "48": "icon.png",
    "128": "icon_large.png"
  },
  "permissions": [ // 权限
    "activeTab",
    "storage",
    "https://*.mywebsite.com/*"
  ],
  "background": {
    "scripts": ["background.js"],
    "persistent": false
  },
  "content_scripts": [
    {
      "matches": ["https://*.google.com/*"],
      "js": ["content.js"],
      "run_at": "document_end"
    }
  ],
  "browser_action": {
    "default_icon": "icon.png",
    "default_popup": "popup.html",
    "default_title": "Open the popup"
  },
  "options_page": "options.html",
  "web_accessible_resources": [
    "script.js",
    "style.css"
  ]
}
```

2. 背景脚本（Background Scripts）

背景脚本是插件的主要工作区域，它可以监听浏览器事件，执行长时间运行的任务，或者管理插件的其他部分。

```javascript
// background.js
chrome.browserAction.onClicked.addListener(function(tab) { // 监听浏览器动作-click事件
  chrome.tabs.executeScript({
    code: 'document.body.style.backgroundColor="green"' // 当前标签页执行一个简单的脚本，将页面背景设为绿色
  });
});
```
3. 内容脚本（Content Scripts）

内容脚本是插入到网页中的脚本，它们可以直接访问和修改网页的DOM。下面是一个内容脚本的例子，它在页面加载完成后，将所有的链接变为红色：

```javascript
// content.js
window.onload = function() {
  var links = document.getElementsByTagName('a');
  for(var i = 0; i < links.length; i++) {
    links[i].style.color = 'red';
  }
};
```

4. 弹出页面(Popup Pages)

弹出页面是插件的用户界面，它们在用户点击插件图标时显示。下面是一个弹出页面的HTML代码，它显示一个简单的欢迎消息：

```html
<!-- popup.html -->
<!DOCTYPE html>
<html>
	<body>
		<h1>Welcome to My Extension!</h1>
	</body>
</html>
```

5. 选项页面(Options Pages)

选项页面是插件的设置页面，用户可以通过它来自定义插件的行为。下面是一个选项页面的例子：

```html
<!-- options.html -->
<!DOCTYPE html>
<html>
<body>
<h1>Extension Options</h1>
<label>Background color: <input type="text" id="bgColor"></label>
<button id="save">Save</button>
<script src="options.js"></script>
</body>
</html>
```

在上面的选项页面中，用户可以输入一个颜色，然后点击保存按钮来改变插件的背景颜色。这需要配合一个options.js脚本来实现：

```javascript
document.getElementById('save').onclick = function() {
  var color = document.getElementById('bgColor').value;
  chrome.storage.sync
 
.set({backgroundColor: color});
};
```




### manifest.json配置项

```json
{
	// 清单文件的版本，这个必须写，而且必须是2
	"manifest_version": 2,
	// 插件的名称"
	name": "demo",
	// 插件的版本
	"version": "1.0.0",
	// 插件描述
	"description": "简单的Chrome扩展demo",
	// 图标，一般偷懒全部用一个尺寸的也没问题"
	icons":{
		"16": "img/icon.png",
		"48": "img/icon.png",
		"128": "img/icon.png"
	},
	// 会一直常驻的后台JS或后台页面
	"background":{
		// 2种指定方式，如果指定JS，那么会自动生成一个背景页
		"page": "background.html"
		//
		"scripts": ["js/background.js"]
	},
	// 浏览器右上角图标设置，browser_action、page_action、app必须三选一
	"browser_action": {
		"default_icon": "img/icon.png",
		// 图标悬停时的标题，可选
		"default_title": "这是一个示例Chrome插件",
		"default_popup": "popup.html"
	},
	// 当某些特定页面打开才显示的图标/*
	"page_action":{
		"default_icon": "img/icon.png",
		"default_title": "我是pageAction","default_popup": "popup.html"
	},*/
	// 需要直接注入页面的JS
	"content_scripts": [{
		//
		"matches": ["http:", "https:"],
		// "<all_urls>" 表示匹配所有地址
		"matches": ["<all_urls>"],
		// 多个JS按顺序注入
		"js": ["js/jquery-1.8.3.js", "js/content-script.js"],
		// JS的注入可以随便一点，但是CSS的注意就要千万小心了，因为一不小心就可能影响全局样式
		"css": ["css/custom.css"],
		// 代码注入的时间，可选值： "document_start", "document_end", or "document_idle"，最后一个表示页面空闲时，默认document_idle
		"run_at": "document_start"
	}, 
	// 这里仅仅是为了演示content-script可以配置多个规则
	{
		"matches": ["*:", "", "*:gif", "*:/.bmp"],
		"js": ["js/show-image-content-size.js"]
	}],
	// 权限申请
	"permissions":[
		"contextMenus", // 右键菜单
		"tabs", // 标签
		"notifications", // 通知
		"webRequest", // web请求
		"webRequestBlocking","storage", // 插件本地存储
		"http:*", // 可以通过executeScript或者insertCSS访问的网站"
		https:/" // 可以通过executeScript或者insertCSS访问的网站
	],
	// 普通页面能够直接访问的插件资源列表，如果不设置是无法直接访问的
	"web_accessible_resources": ["js/inject.js"],
	// 插件主页，这个很重要，不要浪费了这个免费广告位
	"homepage_url": "https://www.baidu.com",
	// 覆盖浏览器默认页面
	"chrome_url_overrides":{
		// 覆盖浏览器默认的新标签页
		"newtab": "newtab.html"
	},
	// Chrome40以前的插件配置页写法
	"options_page": "options.html",
	// Chrome40以后的插件配置页写法，如果2个都写，新版Chrome只认后面这一个
	"options_ui":{
		"page": "options.html",
		// 添加一些默认的样式，推荐使用
		"chrome_style": true
	},
	// 向地址栏注册一个关键字以提供搜索建议，只能设置一个关键字
	"omnibox": { "keyword" : "go" },
	// 默认语言
	"default_locale": "zh_CN",
	// devtools页面入口，注意只能指向一个HTML文件，不能是JS文件
	"devtools_page": "devtools.html"
}
```

## 插件生命周期与事件系统

插件的生命周期是指从用户安装或更新插件，到用户卸载插件的过程。在这个过程中，插件可以响应各种浏览器或用户事件，执行相应的操作

### 插件生命周期

插件的生命周期主要包含以下阶段：
1. 安装或更新：用户第一次安装插件，或者插件有新的版本可供更新时，浏览器会加载并初始化插件。此时，插件可以在background脚本中监听`chrome.runtime.onInstalled`事件，执行初始化操作。
```javascript
chrome.runtime.onInstalled.addListener(function(details) {
	if (details.reason == "install") {
		console.log("This is a first install!");
	} else if (details.reason == "update") {
		console.log("Updated from " + details.previousVersion + " to " + chrome.runtime.getManifest().version + "!");
	}
});
```
2. 启动：用户打开浏览器时，插件会被启动。插件可以在这个阶段初始化数据，设置默认状态等。

```javascript
chrome.runtime.onStartup.addListener(function() {
  console.log("Browser started, initialize plugin data.");
});
```

3. 运行：插件被启动后，就进入了运行阶段。在这个阶段，插件可以响应用户操作，监听和处理浏览器事件，提供各种功能。

```javascript
chrome.tabs.onUpdated.addListener(function(tabId, changeInfo, tab) {
  if (changeInfo.status == 'complete' && tab.active) {
    console.log("Active tab updated, let's do something!");
  }
});
```

4. 停止：用户关闭浏览器时，插件会被停止。插件可以监听chrome.runtime.onSuspend事件，保存数据，清理资源等。

```javascript
chrome.runtime.onSuspend.addListener(function() {
  console.log("Browser is about to close, save plugin data.");
});
```

5. 卸载：用户从浏览器中卸载插件时，插件的生命周期就结束了。插件可以监听chrome.runtime.onInstalled事件的uninstall原因，执行卸载操作。

```javascript
chrome.runtime.setUninstallURL("https://your_website.com/uninstall", function() {
  console.log("Uninstall URL has been set");
});
```
### 插件事件系统
