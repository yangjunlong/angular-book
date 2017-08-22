# 日期格式化过滤器

> filter:date

格式化日期为字符串。

* `'yyyy'`: 4位数字表示年份（例如: AD 1 ＝＞0001，AD 2010 = > 2010）
* `'yy'`: 两位数字表示年份（00-99）（例如：AD 2001 => 01, AD 2010 => 10）
* `'y'`: 一位数字表示年份（例如：AD 1 => 1, AD 199 => 199）
* `'MMMM'`: 英文全称表示月份（January-December）
* `'MMM'`: 英文缩写表示月份（Jan-Dec）
* `'MM'`: 两位数字表示月份（01-12）
* `'M'`: 月份（1-12）
* 'LLLL': 独立英文全称表示月份 (January-December)
* `'dd'`: 两位数字表示日（01-31）
* `'d'`: 日（1-31）
* `'EEEE'`: 英文全称的一周中的天（Sunday-Saturday）
* `'EEE'`: 英文缩写的一周中的天（Sun-Sat）
* `'HH'`: 两位数表示24小时制的时（00-23）
* `'H'`: 24小时制的时（0-23）
* `'hh'`: 两位数字表示上午或下午时 (01-12)
* `'h'`: 上午或下午的时 (1-12)
* `'mm'`: 两位数字表示分 (00-59)
* `'m'`: 分 (0-59)
* `'ss'`: 两位数字表示秒 (00-59)
* `'s'`: 秒 (0-59)
* `'sss'`: 毫秒 (000-999)
* `'a'`: AM/PM 
* `'Z'`: 4位数字（+符号）代表时区偏移量 (-1200-+1200)
* `'ww'`: 用两位数字表示一年的周数（00-53），第一周（01）是一年中的第一个星期四
* `'w'`: 一年的周数(0-53)，第一周（1）是一年中的第一个星期四
* `'G'`, `'GG'`, `'GGG'`: 年代字符串的缩写形式（例如: 'AD' 公元）
* `'GGGG'`: 年代字符串的全称 (例如: 'Anno Domini' 公元)

格式字符串提供了下面一些预定义的可本地化的格式：

* `'medium'`: 相当于 'MMM d, y h:mm:ss a' (例如. Sep 3, 2010 12:05:08 PM)
* `'short'`: 相当于 'M/d/yy h:mm a' (例如. 9/3/10 12:05 PM)
* `'fullDate'`: 相当于 'EEEE, MMMM d, y' (例如. Friday, September 3, 2010)
* `'longDate'`: 相当于 'MMMM d, y' for (例如. September 3, 2010)
* `'mediumDate'`: 相当于 'MMM d, y' (例如. Sep 3, 2010)
* `'shortDate'`: 相当于 'M/d/yy' for (例如. 9/3/10)
* `'mediumTime'`: 相当于 'h:mm:ss a' (例如. 12:05:08 PM)
* `'shortTime'`: 相当于 'h:mm a' (例如. 12:05 PM)

格式化字符串可以包含文本值。这些需要被单引号包围（例如 "h 'in the morning'"）,如果想输出一对单引号，就在一个序列中用两个双引号（例如："h 'o''clock'"）

格式字符串中的任何其他字符将被原样输出。

## 用法
### 在HTML模板中绑定

```
{{ date_expression | date : format : timezone}}
```
### 在JavaScript中

```
$filter('date')(date, format, timezone)
```

### 参数说明

| 参数 | 类型 | 说明 |
|:-------------|:--------------|:---------------| 
| date | Date/Number/String | 日期对象，毫秒，各种ISO 8601日期的字符串格式（例如yyyy mm ddthh：MM：ss.sssz和短的版本一样，ddthh yyyy mm：MMZ，yyyy-mm-dd或yyyymmddthhmmssz）。如果没有时区字符串中指定的输入，时间是在当地时间。 |
| format(可选) | String | 格式的规则（见说明）。如果没有指定，mediumdate使用。 |
| timezone(可选) | String | 时区指定，支持UTC / GMT和大陆美国时区缩写，但对于一般的使用，使用一个时区偏移量，例如，“＋0430”（4小时，30分钟的格林尼治子午线以东）如果未指定的时区，使用浏览器默认时区 |

## 参考
[angular:filter:date](https://docs.angularjs.org/api/ng/filter/date)