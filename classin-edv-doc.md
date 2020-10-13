#### classin edv 文件格式说明
edv 格式内容为一个 json，样例如下，key 不能改，值可以根据需求调整，数据大小写敏感，使用 UTF-8 编码：
``` json
{
    "url":"http://www2.bing.com/?key=value#anchorHash",
    "nickname":true,
    "identity":true,
    "title":"简历评价测试",
    "size":"800x600,400x300",
    "classin_authority":false
}
```

##### 文件打开时程序会默认传入以下参数：

| 字段       | 类型           | 描述                   |
|------------|----------------|------------------------|
| `schoolId` | 64位无符号整数 | 学校唯一标识号         |
| `courseId` | 64位无符号整数 | 课程（班级）唯一标识号 |
| `classId`  | 64位无符号整数 | 课节（教室）唯一标识号 |
| `uid`      | 64位无符号整数 | 打开该 edv 的用户      |
| `deviceType` | 字符串 | 客户端类型，取值范围是`pc`,`android`,`iPhone`,`iPad` |
| `lang`       | 字符串 | 客户端语言，取值范围是`ar`(阿拉伯语),`en`(英语),`es`(西班牙语),`hu`(匈牙利语),`id`(印尼语),`ja`(日语),`ko`(韩语),`vi`(越南语),`zh-CN`(简体中文),`zh-TW`(繁体中文) |

##### edv 文件必填项：
- `url` 需要打开的网址，例如`http://www.example.io/faq.html?key=value#question13`，classin 会将传入的参数与原有的`?key=value`并列，如`http://www.example.io/faq.html?key=value&schoolId=111&courseId=222&classId=333...#question13`

##### edv 文件选填项：

| 字段                  | 类型   | 取值／`默认值` | 描述                                                           |
|-----------------------|--------|----------------|----------------------------------------------------------------|
| `nickname`            | bool   | `true`, false  | `true`表示 classin 打开 url 时将拼接`nickname=<登录者的nickname>` |
| `identity`            | bool   | `true`, false  | `true`表示 classin 打开 url 时将拼接`identity=<登录者的角色>`<BR> 角色范围是`teacher`, `assistant`, `student`, `auditor`     |
| `title`               | string |                | 文件标题栏会显示此字符串                                       |
| `classin_authority` | bool   | `true`, false  | 暂时无用，待扩展                                               |
| `size`                | string | `"600x400,300x200"` | 值为两组宽高，第一组是打开时窗口的推荐大小，第二组是窗口的最小限制。<BR> **注意：两组大小均不能小于 100x0，且推荐大小不能小于最小限制。宽高之间使用小写字母x分隔，两组宽高之间使用半角逗号`,`分隔** |

添加参数后的完整 url 示例：
```http://test.com/index_exam.html?schoolId=111111&courseId=222222&classId=333333&nickname=call%20me%20teacher&identity=teacher&uid=666666&deviceType=pc&lang=zh-CN```
