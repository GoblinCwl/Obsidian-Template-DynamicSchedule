---
tag: 分享
create: 2023-05-14 15:36
---
![2 拷贝.png|1400](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141811205.png)
## 项目地址
下载一个Obsidian演示项目来直接体验
- Gitee: <https://gitee.com/goblincwl/Obsidian-Template-DynamicSchedule>
- GitHub: <https://github.com/GoblinCwl/Obsidian-Template-DynamicSchedule>

## 可以做到什么？
1. 创建每天精确时间的固定日程任务
2. 自动在配置的每周几时创建日程任务
3. 自动在配置的每月几日创建日程任务
4. 匹配排期任务，指定日期在未来自动创建对应日程任务
5. 通过逻辑判断创建任务
6. 生成的周记动态统计本周每天的日程内容

## 需要插件
- **日记** - Obsidian核心插件，提供日记功能
- **Templater** - 提供脚本模板以及脚本函数支持
- **Dataview** - 提供脚本函数支持
- *Calendar* - 右侧日历
- *Day Planner* - 右侧日程表
- *Checklist* - 右侧任务清单
- ToggleList - 快捷切换任务状态
- Style Setting - 样式美化


## 如何使用
### 存放模板
在你的笔记中创建一个文件夹专门用于存储***模板***，并且创建一个***日记***文件夹和一个***周记***文件夹，位置不限。
在*模板文件夹*中新建两个文件，放入下面分享的**日记模板**和**周记模板**。
- 日记模板：<https://gitee.com/goblincwl/Obsidian-Template-DynamicSchedule/blame/main/@%E6%A8%A1%E6%9D%BF/%E6%97%A5%E8%AE%B0%E6%A8%A1%E6%9D%BF.md>
- 周记模板：<https://gitee.com/goblincwl/Obsidian-Template-DynamicSchedule/blame/main/@%E6%A8%A1%E6%9D%BF/%E5%91%A8%E8%AE%B0%E6%A8%A1%E6%9D%BF.md>

### 配置插件
打开设置，从左下 *"第三方插件"* 列表找到插件名字，点击即可进入插件配置

#### **日记**
- 配置日记
![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305182216042.png)

#### **Templater**
- 配置模板文件夹
![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141626103.png)
- 打开这个选项
![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305182222437.png)
- 配置日记和周记模板映射
![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141628623.png)

#### **Dataview**
- 打开JS支持选项 
  ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141643412.png)

#### *Calendar*
- 配置日历上显示周数，方便快速创建周记
  ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141645301.png)
- 配置点击创建的周记信息
  ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141647002.png)

#### *Day Planner*
- 设置模式为Commond mode
  ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141641890.png)
- 这个选项是当前时间线之前的任务会自动被完成，按需要开关
  ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305182222988.png)

#### *Checklist*
- 屏蔽模板文件夹
  ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141649552.png)

#### ToggleList
- 配置任务切换类型
  ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141651511.png)
- 配置任务切换快捷键
  ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141652993.png)

- 点击下面的**HotKey**按钮，给这个操作设置快捷键
  ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141655956.png)

#### Style Setting
- 放入CSS片段
  ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141657489.png)
  - CSS片段：<https://gitee.com/goblincwl/Obsidian-Template-DynamicSchedule/blob/main/.obsidian/snippets/GoblinCwl@CSS.css>
- 在Style Setting的插件设置中可以找到这个CSS，可以配置颜色
  ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141659647.png)
> 这里有显示BUG，同组颜色会显示一样，实际效果实现了就好
### 配置脚本
脚本中提供了非常简单的方式来自定义你的日程清单。
#### 日记文件
```JAVASCRIPT TI:"日记文件"
//日记文件名格式（定义成你自己日记文件名的格式，替换其中的变量）
//yyyy = 年份（例如：2023）
//m    = 自适应位数月份（例如：3、10）
//mm   = 两位数月份（例如：03、10）
//d    = 自适应位数日期（例如：3、10）
//dd   = 两位数日期（例如：03、10）
let dailyFileFormat = "日记：yyyy年m月d日";
```
首先在这里配置你的日记文件名称，例如我的日记文件名称是“日记：2023年5月18日”，就如图配置。

#### 时间段
```JAVASCRIPT TI:"时间段"
//时间段
const timeRegionArray = [
	"00:00|04:59|凌晨",
	"05:00|08:59|早晨",
	"09:00|11:29|上午",
	"11:30|13:29|中午",
	"13:30|17:59|下午",
	"18:00|23:59|晚上",
];
```
在脚本中找到这块代码，来定义日程中对任务的时间段分类，
格式为`时:分|时:分|时间段名称`，**时和分必须是两位数！**
此后，当日程生成时，会根据任务前面的时间来分类到对应的时间段。
如果想排序，更改代码中时间段的顺序就好。

#### 每日任务
```JAVASCRIPT TI:"每日固定任务"
//每日任务清单，预输入固定的每日任务
let taskArray = [
	"07:20|🌞起床",
	"07:25|🪥喝一杯水，洗漱",
	"07:30|🍵**泡茶**",
	"12:25|👀眼保健操",
	"12:30|💤午睡",
	"21:30|📚自考学习",
	"23:15|🥛热牛奶",
	"23:50|🌙洗漱，早睡",
];
```
在脚本中找到这块代码，来定义每天必定会创建的日程，
格式为`时:分|任务`，可以使用emoji和加粗/斜体，
此后，每一天的日程都会有上面的任务。

#### 每周任务
```JAVASCRIPT TI:"每周任务"
//周常任务清单
let weekTaskArray = [{},[],[],[],[],[],[],[]];
//想把任务加在周几，数字就填几
weekTaskArray[5].push("17:00|📰**周报**");
weekTaskArray[6].push("16:00|📞**给妈妈打电话**");
weekTaskArray[7].push("17:00|🧹*整理环境*");
weekTaskArray[7].push("22:00|🗒️**周记**");
```
在脚本中找到这块代码，来定义需要根据星期几来创建的任务，
在`weekTaskArray`后的中括号中输入要星期几创建任务，在后面输入任务格式，
例如，我需要在周四上午的10:30进行笔记整理任务，则另起一行输入`weekTaskArray[4].push("10:30|笔记整理");`
此后，在每周四的日程表中，会创建10:30分的笔记整理这个任务。

#### 每月任务
```JAVASCRIPT TI:"每月任务"
//月任务清单
let monthTaskArray = [{},[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[]];
//想把任务加在每月几号，数字就填几
monthTaskArray[10].push("17:00|🗒💴发工资咯~");
```
在脚本中找到这块代码，来定义需要每个月几号创建的任务，
在`monthTaskArray`后的中括号中输入要每月几号创建任务，在后面输入任务格式。
例如，我需要在每月30号19:00整理月账单，则另起一行输入`weekTaskArray[30].push("19:00|整理月账单");`
此后，在每月的30号的日程表中，会创建19:00整理月账单这个任务。
当然，此处只是根据每月几号，并不是每月最后一天，像2月可能就没有30号，一整个月都不会创建整理月账单，
如果有这方面需求，可以自己写js根据日期判断一下。

#### 排期计划任务
```JAVASCRIPT TI:"排期计划"
//排期计划文件
const planFile = tp.file.find_tfile("排期计划");
//生成日程后排期计划内当天的任务是否删除(true=删除，false=不删除)
const planFileRemoveFlg = true;
//排期计划中未指定精确时间的任务应该在哪个时间点
const planDefaultTaskTime = "09:00";
```
在脚本中找到这块代码，来定义不需要重复，只是未来的某一天需要创建的日程。
首先需要有一个 **"排期计划"** 的笔记，当然你也可以自己明明，修改代码中对应的名字就行
在该文件中以如下形式写下未来日程需要创建的任务：
```MARKDOWN
## 2023年5月17日
- [ ] 13:30 🐱寄养小猫
```
此后，在2023年5月17日这一天，就会创建13:30的🐱寄养小猫任务。
如果你希望创建后保留排期计划中设置的任务，则将`planFileRemoveFlg`的值改为`false`，
否则，在当天创建完日程后，排期计划的笔记中将会自动删除刚刚创建日程时创建的任务。
此外，当你在排期计划中没有明确指定时间点时，将会默认以"09:00"的时间创建任务，
当然，你也可以更改`planDefaultTaskTime`的值来更改默认的时间点。
**planDefaultTaskTime的值中时钟和分钟必须是两位数。**

#### 逻辑判断任务
```JAVASCRIPT TI:"动态任务"
//动态任务，需要独立判断
//昨天日期
let yesterdayDate = new Date(today);
yesterdayDate.setDate(today.getDate() - 1);
// 昨天日记文件名
let fullFileName = "日记："+yesterdayDate.getFullYear()+"年"+(yesterdayDate.getMonth()+1)+"月"+yesterdayDate.getDate()+"日";
const file = tp.file.find_tfile(fullFileName);
if(file != null){
	const content = await app.vault.cachedRead(file);
	const contentStr = content.toString();
	// 隔一天跑步散步
	if(contentStr.contains("- [x] 20:30 👟跑步")){
		taskArray.push("20:30|👞散步");
	}else{
		taskArray.push("20:30|👟跑步");
	}
}
```
可能你还需要一些更有逻辑的任务创建，但是这需要一些Javascript基础来编写。
如代码所示，此处编写的是如果昨天的日程中我完成了跑步任务，那么今天就生成散步任务，否则生成跑步任务。

### 今日工作和今日文章
#### 今日工作
你肯定注意到模板下面还有一些内容，这些内容是个人日程外对日记的一个附加信息。
比如可以从当天的日报中获取今天日报的任务，显示在日记中，
> 任务：指"- [ ]"开头的东西，不管你日报是什么样式，只是读取日报中的任务
``` JAVASCRIPT
//日报文件名格式（定义成你自己的格式，替换其中的变量）
//yyyy = 年份（例如：2023）
//m    = 自适应位数月份（例如：3、10）
//mm   = 两位数月份（例如：03、10）
//d    = 自适应位数日期（例如：3、10）
//dd   = 两位数日期（例如：03、10）
let dailyWorkFileFormat = "日报：yyyy年m月d日";
//日报文件夹目录
let dailyWorkFilePath = "002.工作/工作记录/日报";
```
更改代码中日报文件名格式和日报文件夹目录，来读取日报中的任务到日记中
#### 今日文章
```JAVASCRIPT
const fileToday = new Date(dv.current().create);
```
今日文章会显示当天创建的文件在这个列表中，但是只会读取元数据中带有create字段且值为当天的数据
例如文件元数据是这样的：
```YAML
---
create: 2023-05-14 18:44
tag: 临时
---
```
这样就会被读取到2023年5月14日的日记中
你可以在模板中如下配置，让通过模板创建的笔记自带一个create的元数据
```YAML
---
create: <% tp.file.creation_date () %>
tag: 临时
---
```
### 周记
周记模板会自动获取那一周所有的日记文件，并且进行统计
但是周记模板是通过周记文件名来获取精确的一周的时间的，
**你的周记文件名中必须包含年份和周数！**
你需要在模板开头配置你的周记文件名，让模板可以精确的获取周记对应的周的时间
```JAVASCRIPT
//周记文件名格式
//周记文件名必须包含年份和周数
//yyyy = 年份（例如：2023）
//ww   = 周数（例如：19）
let weekFileFormat = "周记：yyyy年ww周";
```
在中间的代码块需要配置你的日记和日报的文件名称格式和存放文件夹，让周记可以读取内容
```JAVASCRIPT
//日记文件名格式（定义成你自己日记文件名的格式，替换其中的变量）
//yyyy = 年份（例如：2023）
//m    = 自适应位数月份（例如：3、10）
//mm   = 两位数月份（例如：03、10）
//d    = 自适应位数日期（例如：3、10）
//dd   = 两位数日期（例如：03、10）
let dailyFileFormat = "日记：yyyy年m月d日";
//日记文件夹路径
const dailyFilePath = "003.自我/日记";

//日报文件名格式（定义成你自己日报文件名的格式，替换其中的变量）
//yyyy = 年份（例如：2023）
//m    = 自适应位数月份（例如：3、10）
//mm   = 两位数月份（例如：03、10）
//d    = 自适应位数日期（例如：3、10）
//dd   = 两位数日期（例如：03、10）
let dailyWorkFileFormat = "日报：yyyy年m月d日";
//日记文件夹路径
const dailyWorkFilePath = "002.工作/工作记录/日报";
```

## 总结
个人使用中这套模板还是非常方便的，也期待发现更方便的方式管理日程。

## 备注
1. 创建日记后，记得将日记关联到Day Pannel
   ![image.png|670](https://cwl-img.oss-cn-beijing.aliyuncs.com/202305141816852.png)
