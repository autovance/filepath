# @autovance/filepath

> URL like utility for manipulating file paths, names and extensions

Use this class to parse and manipulate file paths and names across platforms. Check out the tests for example use.

**Dependencies: zero**  
**Test Coverage: 100%**

## API

### constructor

Setup a path

```js
const path = new FilePath('this/is/a/file.jpeg');
```

### path

**Set**: set up a path. Used in the constructor  
**Get**: get the fully qualified path

```js
const originalFile = new FilePath();
originalFile.path = '/this/is/a/file.jpeg';
console.log(originalFile.path);

> '/this/is/a/file.jpeg'
```

### file

**Set**: set a file and extension  
If the extension is missing, it will be undefined.  
**Get**: get the file with the extension

```js
const path = new FilePath('this/is/a/file.jpeg');
path.file = 'other.pdf'

console.log(path.file, path.filename, path.extension, path.path);

> 'other.pdf'
> 'other'
> 'pdf'
> 'this/is/a/other.pdf'

path.file = 'new';

console.log(path.file, path.filename, path.extension, path.path);

> 'new'
> 'new'
> undefined
> 'this/is/a/new'
```

### dir

**Set**: change the directory (without the file)  
**Get**: get the directory (without the file)

```js
const path = new FilePath('this/is/a/file.jpeg');
path.dir = '/this/is/the'

console.log(path.dir, path.file, path.filename, path.extension, path.path);

> '/this/is/the'
> 'file.jpeg'
> 'file'
> 'jpeg'
> '/this/is/the/file.jpeg'

```

### filename

**Set**: set the filename (without extension)  
**Get**: get the filename (without extension)

```js
const path = new FilePath('this/is/a/file.jpeg');
path.filename = 'new'

console.log(path.file, path.filename, path.extension, path.path);

> 'new.jpeg'
> 'new'
> 'jpeg'
> 'this/is/a/new.jpeg'
```

### extension

**Set**: set the extension  
**Get**: get the extension (does not include the `.` delimiter)

```js
const path = new FilePath('this/is/a/file.jpeg');
path.extension = 'png';

console.log(path.extension, path.file, path.path);

> 'png'
> 'file.png'
> 'this/is/a/file.png'
```

### folders

An ordered array of folder names. folders[0] represents the root of the path. If absolute, it will be empty '' (required), if relative, it will be the first folder, or reference '.' or '..'.

The recommended use it to change a specific folder in the path, using the index.

```js
const path = new FilePath('/this/is/a/file.jpeg');
console.log(path.folders);

> ['', 'this', 'is', 'a']

path.path = 'this/is/the/file.jpeg';
console.log(path.folders);

> ['this', 'is', 'the']

path.folders.unshift('..');
path.folders[path.folders.length - 1] = 'relative';
console.log(path.folders, path.path);

> ['..', 'this', 'is', 'relative']
> '../this/is/relative/file.jpeg'
```

### isAbsolute and isRelative

Booleans indicating if the path is absolute or relative. Absolute paths start with '/',
and `path.folders[0] === ''`;

```js

const path = new FilePath('/this/is/a/file.jpeg');
console.log(path.isAbsolute, path.isRelative)

> true
> false

path.path = 'this/is/a/file.jpeg';
console.log(path.isAbsolute, path.isRelative)

> false
> true

path.path = './this/is/a/file.jpeg';
console.log(path.isAbsolute, path.isRelative)

> false
> true

path.path = '../this/is/a/file.jpeg';
console.log(path.isAbsolute, path.isRelative)

> false
> true
```
