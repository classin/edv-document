#### Introduction of edv file format in ClassIn
edv file is in the format of json. Taking the file below for example, keys cannot be changed, values can be changed as per requirement. Both keys and values are case sensitive, and encoded with UTF-8.
``` json
{
    "url":"http://www2.bing.com/?key=value#anchorHash",
    "nickname":true,
    "identity":true,
    "title":"Resume Evaluation Test",
    "size":"600x400,300x200",
    "classin_authority":false
}
```

##### ClassIn will pass the following parameters by default:

| Field       | Type           | Description                   |
|------------|----------------|------------------------|
| `schoolId` | unsigned int64 | school identifier         |
| `courseId` | unsigned int64 | course identifier |
| `classId`  | unsigned int64 | class identifier |
| `uid`      | unsigned int64 | user identifier of the one who opened this edv file      |
| `deviceType` | string | device type, possible values are`pc`,`android`,`iPhone`,`iPad` |
| `lang`       | string | client language, possible values are`ar`(Arabic),`en`(English),`es`(Spanish),`hu`(Hungarian),`id`(Indonesian),`ja`(Japanese),`ko`(Korean),`vi`(Vietnamese),`zh-CN`(Simplified Chinese),`zh-TW`(Traditional Chinese) |

##### Required fields in edv file:
- `url` url to open, say `http://www.example.io/faq.html?key=value#question13`, ClassIn will put above parameters side by side with original key-value pair`?key=value`, that is`http://www.example.io/faq.html?key=value&schoolId=111&courseId=222&classId=333...#question13`

##### Optional fields in edv file:

| Field                  | Type   | values/`default` | Description                                                           |
|-----------------------|--------|----------------|----------------------------------------------------------------|
| `nickname`            | bool   | `true`, false  | `true`means pass the following part to url`nickname=<user's nickname>` |
| `identity`            | bool   | `true`, false  | `true`means pass the following part to url`identity=<user's role>`<BR> possible values are `teacher`, `assistant`, `student`, `auditor`     |
| `title`               | string |                | Value of this field will be used as title of the file   |
| `classin_authority`   | bool   | `true`, false  | Not applicable for now, will be used in the future   |
| `size`                | string | `"600x400,300x200"` | The value has two sets of width x height. The first set is the recommended size of the window opened by the file, the second set is the minimum size.<BR> **Note：both the two sets cannot be smaller than 100x0，and the recommended size cannot be smaller than the minimum size. Width and height are separated by lower case `x`, two sets are separated by half-width comma`,`** |

Example of a full url with parameters:
```http://test.com/index_exam.html?schoolId=111111&courseId=222222&classId=333333&nickname=call%20me%20teacher&identity=teacher&uid=666666&deviceType=pc&lang=zh-CN```
