

### 分析 `package.jason` 和 `extension.js` 文件

`package.json`

```{.line-numbers}
{
  "name": "helloworld",                 // 插件名称
	"displayName": "HelloWorld",
	"description": "LEAVE BLANK",
	"version": "0.0.1",                 // 插件版本
	"engines": {
		"vscode": "^1.68.0"             // vscode 版本
	},
	"categories": [
		"Other"
	],
	"activationEvents": [               // 扩展激活事件 (当什么情况下激活)
        "onLanguage:javascript"
	],
	"main": "./out/extension.js",       // 入口文件
	"contributes": {                    // vscode 插件的大部分功能配置都在这里
		"commands": [
			{
				"command": "plaintext",
				"title": "Hello World"
			}
		],
		"menus": {
			"editor/context": [
				{
				"when": "editorFocus",
				"command": "plaintext",
				"group": "navigation"
				}
			],
			"explorer/context":[
				{
					"command": "plaintext",
					"group": "navigation"
				}
			]
		}
	},
	"scripts": {
		"vscode:prepublish": "npm run compile",
		"compile": "tsc -p ./",
		"watch": "tsc -watch -p ./",
		"pretest": "npm run compile && npm run lint",
		"lint": "eslint src --ext ts",
		"test": "node ./out/test/runTest.js"
	},
	"devDependencies": {
		"@types/vscode": "^1.68.0",
		"@types/glob": "^7.2.0",
		"@types/mocha": "^9.1.1",
		"@types/node": "16.x",
		"@typescript-eslint/eslint-plugin": "^5.30.0",
		"@typescript-eslint/parser": "^5.30.0",
		"eslint": "^8.18.0",
		"glob": "^8.0.3",
		"mocha": "^10.0.0",
		"typescript": "^4.7.4",
		"@vscode/test-electron": "^2.1.5"
	}
}
```

`extension.js`

```
"use strict";
Object.defineProperty(exports, "__esModule", { value: true });
exports.deactivate = exports.activate = void 0;
// The module 'vscode' contains the VS Code extensibility API
// Import the module and reference it with the alias vscode in your code below
const vscode = require("vscode");
// this method is called when your extension is activated
// your extension is activated the very first time the command is executed
function activate(context) {
    // Use the console to output diagnostic information (console.log) and errors (console.error)
    // This line of code will only be executed once when your extension is activated
    console.log('Congratulations, your extension "helloworld" is now active!');
    // The command has been defined in the package.json file
    // Now provide the implementation of the command with registerCommand
    // The commandId parameter must match the command field in package.json
    let disposable = vscode.commands.registerCommand('helloworld.helloWorld', () => {
        // The code you place here will be executed every time your command is executed
        // Display a message box to the user
        vscode.window.showInformationMessage("Hello World!!");
    });
    context.subscriptions.push(disposable);
}
exports.activate = activate;
// this method is called when your extension is deactivated
function deactivate() { }
exports.deactivate = deactivate;
//# sourceMappingURL=extension.js.map
```

---

## Vscode插件开发 -- 代码提示、代码补全、代码分析

https://blog.csdn.net/luoluoyang23/article/details/124543453


