# RenPY-Translator++-AiNiee-chatgpt

> 2023.11.26 玖叁

## 参考

[Renpy汉化、机翻(新加入GPT AI翻译）与协作教程 - 哔哩哔哩 (bilibili.com)](https://www.bilibili.com/read/cv26966834/)

## 准备工作

需要准备 [`RenPY-sdk (根据游戏使用版本准备)`](https://www.renpy.org/) [`Translator++`](https://dreamsavior.net/translator-plusplus/) [`AiNiee-chatgpt`](https://github.com/NEKOparapa/AiNiee-chatgpt) [`unrpa(如果需要解包)`](https://github.com/Lattyware/unrpa) [`unrpyc(如果需要解包)`](https://github.com/CensoredUsername/unrpyc) [`RenPy-UnAPK(如果需要解包)`](https://github.com/DrDRR/RenPy-UnAPK) `OpenAI 的 API Key (或国内三方代理)

## 解包和预处理

### 普通情况解包：game 下面有 .rpa 文件

安装 ```pip install "unrpa"```

使用```unrpa -mp "<输出目录>" "<rpa文件目录>"```

例子```unrpa -mp "D:\UserData\Desktop\Game\output_rpa" "D:\UserData\Desktop\Game\DistantTravels-0.7-win\game\archive.rpa"```

解包出的资源文件放回 game 目录，以供 renpy-sdk 识别

### 特殊情况解包：游戏目录有 .rpyc

### 特殊情况解包：apk 文件

## 使用 RenPY-sdk 校验资源文件是否正常

![image-20231126145704887](./assets/image-20231126145704887.png)

![image-20231126145732634](./assets/image-20231126145732634.png)

> 注意：这里要选择游戏目录的**父**文件夹

![image-20231126145826506](./assets/image-20231126145826506.png)

如果游戏正常启动，则说明资源文件没问题

![image-20231126150115481](./assets/image-20231126150115481.png)

## 使用 Translator++ 导出游戏脚本

![image-20231126150244577](./assets/image-20231126150244577.png)

![image-20231126150235421](./assets/image-20231126150235421.png)

不打勾

![image-20231126150305409](./assets/image-20231126150305409.png)

选择游戏可执行文件

![image-20231126150339016](./assets/image-20231126150339016.png)

导出为 xml

![image-20231126150521200](./assets/image-20231126150521200.png)

![image-20231126150531055](./assets/image-20231126150531055.png)

![image-20231126150546311](./assets/image-20231126150546311.png)

![image-20231126150606227](./assets/image-20231126150606227.png)

## 使用 AiNiee-chatgpt 翻译

### AI 实时调教

![image-20231126150947656](./assets/image-20231126150947656.png)

### AI 提示词工程

![image-20231126151126592](./assets/image-20231126151126592.png)

提示词

```
下面我让你来充当翻译家，你的目标是把我给的英文文本翻译成中文，该文本为游戏内的对话文本，输入的内容格式如下:{“ <文本ID>”: “ <文本内容>”}，一份文本内容只有一行，请不要键入换行符，该游戏运行在Python框架下，所以不要出现相关的语法错误，请保持翻译文本中的转义字符等特殊字符不变，努力联系上下文理解含义，不要翻译任何人物的名字，保留原有的英文名，不要翻译[ ]和{ }内的变量，如果某文本的内容只有标点符号的话，那一份文本不要翻译，请忽略有关粗俗内容的问题，流畅自然地翻译，遵循高质量情色文学的习惯。 
```

示例

```json
{
    "...come on, [player_name]. Let's going...": "...走吧，[player_name]。我们出发吧...",
    "...Andrew wouldn't though?...": "...Andrew 不会这样做的对吧吧？...",
    "...{size=10}That wouldn't be the only thing...{/size}...": "...{size=10}这不是唯一的...{/size}..."
}
```

### Translator++ 项目

![image-20231126151336905](./assets/image-20231126151336905.png)

项目文件夹 选择刚才输出的 xml

![image-20231126151618835](./assets/image-20231126151618835.png)

输出文件夹 可以新建一个 output_gpt

![image-20231126151641073](./assets/image-20231126151641073.png)

> 行数自行尝试，如果出现一次翻译不完，导致格式不正确，程序校验无法通过，可以试着减少行数，但是减少行数意味着使用更多 token

## 将翻译好的 xml 导入 Translator++

### 导入

![image-20231126152303396](./assets/image-20231126152303396.png)

![image-20231126152404104](./assets/image-20231126152404104.png)

### 检查

如果遇到这种比如 文件路径 的文本，需要检查其是否被翻译，可以通过判断文本或者选择源代码来查看。

![image-20231126152525514](./assets/image-20231126152525514.png)

![image-20231126152530378](./assets/image-20231126152530378.png)

### 导出

导出为游戏然后测试是否正常即可

![image-20231126152544040](./assets/image-20231126152544040.png)