# Storage (Storages)

The `storages` module can be used to save [simple data / configuration / lists], etc.  
Saved data is shared between scripts, so it is not suitable for storing sensitive information.

When saving data, a name is required, similar to a namespace.  
One name corresponds to one independent local storage.  
However, unlike LocalStorage in web development, it cannot provide domain-isolated storage because script paths may change at any time.

Saved data will only be deleted in the following cases:

- The AutoJs6 app is uninstalled or its data is cleared
- Deleted using methods such as [storages.remove](#m-remove) / [Storage#remove](storageType#m-remove) / [Storage#clear](storageType#m-clear)

Supported data types for storage:

- [number](dataTypes#number)
- [boolean](dataTypes#boolean)
- [string](dataTypes#string)
- [null](dataTypes#null)
- [Array](dataTypes#array)
- [Object](dataTypes#object)
- ... ...

具体的存入规则详见 [Storage#put](storageType#m-put) 小节.

存入时, 由 [JSON.stringify](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) 序列化数据为 [string](dataTypes#string) 类型后再存入,  
读取时, 由 [JSON.parse](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse) 还原为原本的数据类型.

---

<p style="font: bold 2em sans-serif; color: #FF7043">storages</p>

---

## [m] create

### create(name)

- **name** { [string](dataTypes#string) } - Storage name
- <ins>**returns**</ins> { [Storage](storageType) }

Creates a local storage named `name` and returns a [Storage](storageType) instance:

```js
/* Create a local storage named "fruit". */
let sto = storages.create('fruit');

/* Store key-value data. */
sto.put('apple', 10);
sto.put('banana', 20);

/* Access the data. */
sto.get('apple'); // 10
sto.get('banana'); // 20
sto.get('cherry'); // undefined
```

Different `name` values create separate local storages:

```js
let stoFruit = storages.create('fruit');
let stoPhone = storages.create('phone');

/* "键" 名均为 apple, 不同的本地存储之间数据独立. */
stoFruit.put('apple', 7);
stoPhone.put('apple', 3);

/* 访问数据 */
stoFruit.get('apple') // 7
stoPhone.get('apple') // 3
```

如果 `name` 参数对应的本地存储已存在, 则返回一个本地存储副本:

```js
let sto = storages.create('fruit');
sto.put('apple', 10);

/* 名为 fruit 的本地存储已创建, 因此返回的是存储副本. */
let stoCopied = storages.create('fruit');

/* 虽然 stoCopied 没有存入 apple 数据, 但 fruit 本地存储中存在. */
stoCopied.get('apple'); // 10

/* 副本与原始的本地存储并非引用关系. */
sto === stoCopied; // false
```

为保证数据安全及唯一性, `name` 参数应尽量具体:

```js
storages.create('project-publishing-schedule');
```

## [m] remove

### remove(name)

- **name** { [string](dataTypes#string) } - 存储名称
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - name 参数对应的本地存储是否存在

清除名为 `name` 的本地存储包含的全部数据.

如果名为 `name` 的本地存储已存在, 返回 `true`, 否则返回 `false`.

```js
let sto = storages.create('fruit');
sto.put('apple', 10);
sto.get('apple'); // 10

/* 相当于 storages.create('fruit').clear(); . */
storages.remove('fruit'); // true

/* 执行 remove 方法后, sto 对象将不存在任何存储数据. */
sto.get('apple'); // undefined

/* 但 sto 依然可以存放新的数据. */
sto.put('banana', 20);
sto.get('banana'); // 20
```