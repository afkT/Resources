# SharedPreferences 工具类

#### 使用演示类 [ShareUse][ShareUse] 介绍了配置参数及使用

> 1.apply 没有返回值而 commit 返回 boolean 表明修改是否提交成功
> 2.apply 是将修改数据原子提交到内存，而后异步真正提交到硬件磁盘，而 commit 是同步的提交到硬件磁盘
> 3.apply 方法不会提示任何失败的提示 apply 的效率高一些，如果没有必要确认是否提交成功建议使用 apply

#### 项目类结构 - [包目录][包目录]

* SharedPreferences 工具类（[SPUtils][SPUtils]）：SP 操作工具类，实现 IPreferenceHolder 初始化方法

* IPreference 持有类（[IPreferenceHolder][IPreferenceHolder]）：IPreference 持有类，内部返回实现类 IPreference

* IPreference 接口类（[IPreference][IPreference]）：主要是正常操作方法接口类

* PreferenceImpl 接口实现类（[PreferenceImpl][PreferenceImpl]）：实现 IPreference 接口，SharedPreferences 操作接口具体实现类

* SharedPreferences 快捷使用工具类（[SharedUtils][SharedUtils]）：内部实现 SPUtils，直接进行使用 put/get 等

## API 文档

| 方法 | 注释 |
| :- | :- |
| put | 保存数据 |
| putAll | 保存 Map 集合(只能是 Integer、Long、Boolean、Float、String、Set) |
| get | 根据 key 获取数据 |
| getAll | 获取全部数据 |
| remove | 移除数据 |
| removeAll | 移除集合的数据 |
| contains | 是否存在 key |
| clear | 清除全部数据 |
| getInt | 获取 int 类型的数据 |
| getFloat | 获取 float 类型的数据 |
| getLong | 获取 long 类型的数据 |
| getBoolean | 获取 boolean 类型的数据 |
| getString | 获取 String 类型的数据 |
| getSet | 获取 Set 类型的数据 |

#### 使用示例
```java
// 具体实现方法 基于 PreferenceImpl 实现

// 存在可调用的方法 IPreference

// SharedUtils 二次分装 SPUtils, 快捷调用

SharedUtils.put("aa", "aa");
SharedUtils.put("ac", 123);

// ===========
// = SPUtils =
// ===========

// 想要自定义 模式, 名字等
SPUtils.getPreference(DevUtils.getContext()).put("aa", 1);
SPUtils.getPreference(DevUtils.getContext(), "xxx").put("aa", 1);
SPUtils.getPreference(DevUtils.getContext(), "xxxxx", Context.MODE_PRIVATE).put("aa", 1);


// 默认值如下
switch (type) {
    case INTEGER:
        return preferences.getInt(key, -1);
    case FLOAT:
        return preferences.getFloat(key, -1F);
    case BOOLEAN:
        return preferences.getBoolean(key, false);
    case LONG:
        return preferences.getLong(key, -1L);
    case STRING:
        return preferences.getString(key, null);
    case STRING_SET:
        return preferences.getStringSet(key, null);
    default: // 默认取出String类型的数据
        return null;
}
```





[ShareUse]: https://github.com/afkT/DevUtils/blob/master/application/DevUtilsApp/src/main/java/utils_use/share/ShareUse.java
[包目录]: https://github.com/afkT/DevUtils/blob/master/lib/DevApp/src/main/java/dev/utils/app/share
[SPUtils]: https://github.com/afkT/DevUtils/blob/master/lib/DevApp/src/main/java/dev/utils/app/share/SPUtils.java
[IPreferenceHolder]: https://github.com/afkT/DevUtils/blob/master/lib/DevApp/src/main/java/dev/utils/app/share/IPreferenceHolder.java
[IPreference]: https://github.com/afkT/DevUtils/blob/master/lib/DevApp/src/main/java/dev/utils/app/share/IPreference.java
[PreferenceImpl]: https://github.com/afkT/DevUtils/blob/master/lib/DevApp/src/main/java/dev/utils/app/share/PreferenceImpl.java
[SharedUtils]: https://github.com/afkT/DevUtils/blob/master/lib/DevApp/src/main/java/dev/utils/app/share/SharedUtils.java