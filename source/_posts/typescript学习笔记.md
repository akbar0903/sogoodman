---
title: typescript学习笔记
date: 2026-01-07 16:09:46
tags: ['typescript']
categories: ['TypeScript']
cover: https://www4.bing.com//th?id=OHR.KenyaElephants_ZH-CN7587207512_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp
---

# --watch 模式

在开发过程中，使用 `--watch` 模式可以让 TypeScript 编译器在文件更改时自动重新编译代码。这样可以提高开发效率，避免手动运行编译命令。
```bash
tsc --watch [your-file].ts
```
# --init 命令

`--init` 命令用于在当前目录下创建一个 `tsconfig.json` 文件，该文件包含 TypeScript 项目的配置选项。运行以下命令即可生成默认的配置文件：
```bash
tsc --init
```

`tsconfig.json`文件：
```json
{
  "compilerOptions": {
    /* Visit https://aka.ms/tsconfig to read more about this file */

    /* Projects */
    // "incremental": true,                              /* Save .tsbuildinfo files to allow for incremental compilation of projects. */
    // "composite": true,                                /* Enable constraints that allow a TypeScript project to be used with project references. */
    // "tsBuildInfoFile": "./.tsbuildinfo",              /* Specify the path to .tsbuildinfo incremental compilation file. */
    // "disableSourceOfProjectReferenceRedirect": true,  /* Disable preferring source files instead of declaration files when referencing composite projects. */
    // "disableSolutionSearching": true,                 /* Opt a project out of multi-project reference checking when editing. */
    // "disableReferencedProjectLoad": true,             /* Reduce the number of projects loaded automatically by TypeScript. */

    /* Language and Environment */
    
    /********************* 配置编译结果会输出哪种等级的JavaScript代码，比如 ES5、ES6（ES2015）、ES2016 等 *********************************/
    "target": "es2015",                                  /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */
    /********************* 如果lib被注释，使用默认的lib，如果没有被注释，需要提供 *********************************/
    "lib": [
      "dom", // 可以访问浏览器的DOM API，如果是nodejs环境，可以去掉
      "es2015", // 包含 ES2015 的标准库声明，不然typescript中没办法写 ES2015 的代码，比如const、let、Promise等
    ],                                        /* Specify a set of bundled library declaration files that describe the target runtime environment. */
    // "jsx": "preserve",                                /* Specify what JSX code is generated. */
    // "experimentalDecorators": true,                   /* Enable experimental support for legacy experimental decorators. */
    // "emitDecoratorMetadata": true,                    /* Emit design-type metadata for decorated declarations in source files. */
    // "jsxFactory": "",                                 /* Specify the JSX factory function used when targeting React JSX emit, e.g. 'React.createElement' or 'h'. */
    // "jsxFragmentFactory": "",                         /* Specify the JSX Fragment reference used for fragments when targeting React JSX emit e.g. 'React.Fragment' or 'Fragment'. */
    // "jsxImportSource": "",                            /* Specify module specifier used to import the JSX factory functions when using 'jsx: react-jsx*'. */
    // "reactNamespace": "",                             /* Specify the object invoked for 'createElement'. This only applies when targeting 'react' JSX emit. */
    // "noLib": true,                                    /* Disable including any library files, including the default lib.d.ts. */
    // "useDefineForClassFields": true,                  /* Emit ECMAScript-standard-compliant class fields. */
    // "moduleDetection": "auto",                        /* Control what method is used to detect module-format JS files. */

    /* Modules */
    /********************* 配置编译结果会输出哪种模块规范的代码，比如 CommonJS、ES6 模块等 *********************************/
    "module": "commonjs",                                /* Specify what module code is generated. */

    /********************* rootDir配置要编译的ts文件的目录，比如./src目录 *********************************/
    // "rootDir": "./",                                  /* Specify the root folder within your source files. */
    // "moduleResolution": "node10",                     /* Specify how TypeScript looks up a file from a given module specifier. */
    // "baseUrl": "./",                                  /* Specify the base directory to resolve non-relative module names. */
    // "paths": {},                                      /* Specify a set of entries that re-map imports to additional lookup locations. */
    // "rootDirs": [],                                   /* Allow multiple folders to be treated as one when resolving modules. */
    // "typeRoots": [],                                  /* Specify multiple folders that act like './node_modules/@types'. */
    // "types": [],                                      /* Specify type package names to be included without being referenced in a source file. */
    // "allowUmdGlobalAccess": true,                     /* Allow accessing UMD globals from modules. */
    // "moduleSuffixes": [],                             /* List of file name suffixes to search when resolving a module. */
    // "allowImportingTsExtensions": true,               /* Allow imports to include TypeScript file extensions. Requires '--moduleResolution bundler' and either '--noEmit' or '--emitDeclarationOnly' to be set. */
    // "resolvePackageJsonExports": true,                /* Use the package.json 'exports' field when resolving package imports. */
    // "resolvePackageJsonImports": true,                /* Use the package.json 'imports' field when resolving imports. */
    // "customConditions": [],                           /* Conditions to set in addition to the resolver-specific defaults when resolving imports. */
    // "noUncheckedSideEffectImports": true,             /* Check side effect imports. */
    // "resolveJsonModule": true,                        /* Enable importing .json files. */
    // "allowArbitraryExtensions": true,                 /* Enable importing files with any extension, provided a declaration file is present. */
    // "noResolve": true,                                /* Disallow 'import's, 'require's or '<reference>'s from expanding the number of files TypeScript should add to a project. */

    /* JavaScript Support */
    /********************* allowJs和checkJs配置是否支持编译JavaScript文件 *********************************/
    // "allowJs": true,                                  /* Allow JavaScript files to be a part of your program. Use the 'checkJS' option to get errors from these files. */
    // "checkJs": true,                                  /* Enable error reporting in type-checked JavaScript files. */

    // "maxNodeModuleJsDepth": 1,                        /* Specify the maximum folder depth used for checking JavaScript files from 'node_modules'. Only applicable with 'allowJs'. */

    /* Emit */
    // "declaration": true,                              /* Generate .d.ts files from TypeScript and JavaScript files in your project. */
    // "declarationMap": true,                           /* Create sourcemaps for d.ts files. */
    // "emitDeclarationOnly": true,                      /* Only output d.ts files and not JavaScript files. */

    /********************* 通过开启sourceMap可以对应的filename.js.map文件，然后可以通过浏览器的调试工具调试ts代码 *********************************/
    // "sourceMap": true,                                /* Create source map files for emitted JavaScript files. */
    // "inlineSourceMap": true,                          /* Include sourcemap files inside the emitted JavaScript. */
    // "noEmit": true,                                   /* Disable emitting files from a compilation. */
    // "outFile": "./",                                  /* Specify a file that bundles all outputs into one JavaScript file. If 'declaration' is true, also designates a file that bundles all .d.ts output. */

    /********************* outDir配置编译后的文件输出目录，比如./dist目录 *********************************/
    // "outDir": "./",                                   /* Specify an output folder for all emitted files. */

    /********************* removeComments 配置ts中的注释是否也编译到输出文件中 *********************************/
    // "removeComments": true,                           /* Disable emitting comments. */
    // "importHelpers": true,                            /* Allow importing helper functions from tslib once per project, instead of including them per-file. */
    // "downlevelIteration": true,                       /* Emit more compliant, but verbose and less performant JavaScript for iteration. */
    // "sourceRoot": "",                                 /* Specify the root path for debuggers to find the reference source code. */
    // "mapRoot": "",                                    /* Specify the location where debugger should locate map files instead of generated locations. */
    // "inlineSources": true,                            /* Include source code in the sourcemaps inside the emitted JavaScript. */
    // "emitBOM": true,                                  /* Emit a UTF-8 Byte Order Mark (BOM) in the beginning of output files. */
    // "newLine": "crlf",                                /* Set the newline character for emitting files. */
    // "stripInternal": true,                            /* Disable emitting declarations that have '@internal' in their JSDoc comments. */
    // "noEmitHelpers": true,                            /* Disable generating custom helper functions like '__extends' in compiled output. */

    /********************* noEmitOnError配置如果有类型检查错误则不输出文件, 直到修复错误 *********************************/
    // "noEmitOnError": true,                            /* Disable emitting files if any type checking errors are reported. */
    // "preserveConstEnums": true,                       /* Disable erasing 'const enum' declarations in generated code. */
    // "declarationDir": "./",                           /* Specify the output directory for generated declaration files. */

    /* Interop Constraints */
    // "isolatedModules": true,                          /* Ensure that each file can be safely transpiled without relying on other imports. */
    // "verbatimModuleSyntax": true,                     /* Do not transform or elide any imports or exports not marked as type-only, ensuring they are written in the output file's format based on the 'module' setting. */
    // "isolatedDeclarations": true,                     /* Require sufficient annotation on exports so other tools can trivially generate declaration files. */
    // "allowSyntheticDefaultImports": true,             /* Allow 'import x from y' when a module doesn't have a default export. */
    "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
    // "preserveSymlinks": true,                         /* Disable resolving symlinks to their realpath. This correlates to the same flag in node. */
    "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */

    /* Type Checking */
    
    "strict": true,                                      /* Enable all strict type-checking options. */
    // "noImplicitAny": true,                            /* Enable error reporting for expressions and declarations with an implied 'any' type. */
    // "strictNullChecks": true,                         /* When type checking, take into account 'null' and 'undefined'. */
    // "strictFunctionTypes": true,                      /* When assigning functions, check to ensure parameters and the return values are subtype-compatible. */
    // "strictBindCallApply": true,                      /* Check that the arguments for 'bind', 'call', and 'apply' methods match the original function. */
    // "strictPropertyInitialization": true,             /* Check for class properties that are declared but not set in the constructor. */
    // "strictBuiltinIteratorReturn": true,              /* Built-in iterators are instantiated with a 'TReturn' type of 'undefined' instead of 'any'. */
    // "noImplicitThis": true,                           /* Enable error reporting when 'this' is given the type 'any'. */
    // "useUnknownInCatchVariables": true,               /* Default catch clause variables as 'unknown' instead of 'any'. */

    /********************* 编译后的JavaScript文件最上面带有'use strict' *********************************/
    // "alwaysStrict": true,                             /* Ensure 'use strict' is always emitted. */

    // "noUnusedLocals": true,                           /* Enable error reporting when local variables aren't read. */
    // "noUnusedParameters": true,                       /* Raise an error when a function parameter isn't read. */
    // "exactOptionalPropertyTypes": true,               /* Interpret optional property types as written, rather than adding 'undefined'. */
    // "noImplicitReturns": true,                        /* Enable error reporting for codepaths that do not explicitly return in a function. */
    // "noFallthroughCasesInSwitch": true,               /* Enable error reporting for fallthrough cases in switch statements. */
    // "noUncheckedIndexedAccess": true,                 /* Add 'undefined' to a type when accessed using an index. */
    // "noImplicitOverride": true,                       /* Ensure overriding members in derived classes are marked with an override modifier. */
    // "noPropertyAccessFromIndexSignature": true,       /* Enforces using indexed accessors for keys declared using an indexed type. */
    // "allowUnusedLabels": true,                        /* Disable error reporting for unused labels. */
    // "allowUnreachableCode": true,                     /* Disable error reporting for unreachable code. */

    /* Completeness */
    // "skipDefaultLibCheck": true,                      /* Skip type checking .d.ts files that are included with TypeScript. */
    "skipLibCheck": true                                 /* Skip type checking all .d.ts files. */
  },

  // 配置：Include and Exclude，哪些文件会被编译，哪些文件不会被编译
  "include": [
    "src/**/*"
  ],
  "exclude": [
    "node_modules", // 默认会排除 node_modules 文件夹
    "**/*.spec.ts"
  ]
}
```

然后执行以下命令编译整个项目（编译每个ts文件，然后生成对应的js文件）：
```bash
tsc
```

也可以使用 `--watch` 模式实时编译项目：
```bash
tsc --watch
```

# 类型注解 (Type Annotations)

## 基本类型

- `number`: 用于表示数字类型。
- `string`: 用于表示字符串类型。
- `boolean`: 用于表示布尔类型，只有两个值：`true` 和 `false`。
- `any`: 表示任意类型，可以赋值为任何类型的值。
- `void`: 通常用于函数没有返回值的情况。
- `null` 和 `undefined`: 分别表示空值和未定义值。
- `unknown`: 表示未知类型，类似于 `any`，但更安全。

  b比如：
  ```typescript
  let value: unknown;
  value = 42;          // 正确
  value = "Hello";     // 也正确
  ``` 

  unknown 类型的值不能直接赋值给其他类型，必须进行类型检查或类型断言：
  ```typescript
  let value: unknown = "Hello, TypeScript!";
  let str: string;
  if (typeof value === "string") {
    str = value; // 现在可以安全地赋值
  }
  ```

- `never`: 表示永远不会有值的类型，通常用于抛出错误或无限循环的函数。

  比如，
  ```typescript
  // 一个永远不会返回的函数
  function throwError(message: string): never {
    throw new Error(message);
  }
  ```

- `symbol`: 用于表示唯一的标识符。
  比如：
  ```typescript
  let sym1: symbol = Symbol('unique');
  let sym2: symbol = Symbol('unique');
  console.log(sym1 === sym2); // false
  ```

- `Function`: 用于表示函数类型，可以指定参数和返回值的类型。
  比如：
  ```typescript
  let add: (a: number, b: number) => number;
  add = (x, y) => x + y;
  console.log(add(2, 3)); // 5
  ```

  又比如包含callback的函数：
  ```typescript
  function fetchData(url: string, callback: (data: string) => void): void {
    // 模拟异步数据获取
    setTimeout(() => {
      const data = `Data from ${url}`;
      callback(data);
    }, 1000);
  }

  fetchData('https://api.example.com', (data) => {
    console.log(data); // 输出: Data from https://api.example.com
  });
  ```

## 引用类型

- `array`: 用于表示数组类型，可以使用两种语法：`number[]` 或 `Array<number>`。
- `object`: 用于表示对象类型，一般要配合泛型使用。
- `tuple`: 用于表示固定长度和类型的数组（Fix Length of Array），例如 `[string, number]`。

比如，下面的代码定义了一个包含字符串和数字的元组：

```typescript
let tuple: [string, number];
tuple = ["hello", 42]; // 正确
```

又比如：
```typescript
interface User {
  username: string
  password: string
  email?: string
  phoneNumber: string
  // Tuple
  role: [number, string]
}

const user: User = {
  username: 'alice',
  password: 'my-password',
  phoneNumber: '123-456-7890',
  role: [1, 'author'],
}
```

> tuple 是一个固定长度的数组，比如上面代码中 `role: [number, string]` 告诉typescript，这个role是一个数组，但是这个数组只能有两个元素，第一个是number类型，第二个是string类型。

- `enum`: 用于定义一组命名的常量。

比如，
```typescript
enum Color {
  RED = 'red',
  GREEN = 'green',
  BLUE = 'blue',
}

console.log(Color.RED)
```

# Union Types 联合类型

Union Types（联合类型）允许一个变量可以持有多种类型的值。使用竖线 `|` 来分隔不同的类型。

```typescript
let value: string | number;
value = "Hello"; // 正确
value = 42;      // 也正确
// value = true; // 错误，不能赋值为布尔类型
```

# Type Aliases 类型别名

Type Aliases（类型别名）允许你为一个类型创建一个新的名称，使用 `type` 关键字。

```typescript
type ID = string | number;
let userId: ID;
userId = "abc123"; // 正确
userId = 456;      // 也正确
```


# 类型断言 `as`


# Object Oriented Programming 面向对象编程

## 类 class

下面看一个示例代码：
```typescript
class Department {
  name: string

  constructor(name: string) {
    this.name = name
  }

  describe(this: Department) {
    console.log(`Department name: ${this.name}`)
  }
}

const department = new Department('Learn01')
department.describe()

const myDepartment = { describe: department.describe }
myDepartment.describe()  // 这里报错
```

为什么`myDepartment.describe()`会报错呢？
我们需要先搞懂`describe(this: Department)`这里的this是什么意思：

这里的 this: Department 是 TypeScript 的虚拟参数。它在运行时不存在，但在编译时，它告诉 TypeScript：“只有当 this 指向一个符合 Department 结构的实例时，才能调用这个方法。”

当执行以下代码时：
```typescript
const myDepartment = { describe: department.describe }
myDepartment.describe()
```
- 运行时的行为：在 JavaScript 中，当你通过 myDepartment.describe() 调用函数时，函数内部的 this 会指向 myDepartment 这个对象。
- 编译时的检查：TypeScript 检查发现 myDepartment 的类型是 { describe: function }。
- 冲突点：describe 方法要求 this 必须是一个 Department（必须包含 name 属性和 describe 方法），但你的 myDepartment 对象没有 name 属性。

因此，TypeScript 抛出错误，警告你：“你正在一个没有 name 属性的对象上调用一个需要 name 属性的方法，这会导致运行时错误（或输出 undefined）。”

所以，我们只要把 myDepartment 对象改成符合 Department 结构的对象就可以了：
```typescript
const myDepartment = {
  name: 'Learn02',
  describe: department.describe
}
myDepartment.describe()  // 正常输出 Department name: Learn02
```

## private 和 public 修饰符

### public 修饰符

默认情况下，类的属性和方法都是 public 的，比如：
```typescript
class Department {
  name: string  // 默认是 public

  constructor(name: string) {
    this.name = name
  }

  describe(this: Department) {
    console.log(`Department name: ${this.name}`)
  }
}

const department = new Department('Learn01')
// 直接访问 name 属性
console.log(department.name)  // 输出 Learn01
```

### private 修饰符

我们看一下下面的代码有什么问题：
```typescript
class Department {
  name: string
  employees: string[] = []

  constructor(name: string) {
    this.name = name
  }

  describe(this: Department) {
    console.log(`Department name: ${this.name}`)
  }

  addEmployee(employee: string) {
    this.employees.push(employee)
  }

  printEmployeeInformation() {
    console.log('count of employee',this.employees.length)
    console.log('employees:', this.employees)
  }
}

const department = new Department('Learn01')
// 直接department添加employee
department.employees.push('Max', 'Manu')

department.printEmployeeInformation()
```

上面代码中，`department.employees.push('Max', 'Manu')` 这一行代码直接访问了 `employees` 属性并修改了它。这违反了封装的原则，因为 `employees` 应该只能通过类的方法来修改。

为了解决这个问题，我们可以使用 `private` 修饰符将 `employees` 属性设为私有：
```typescript
class Department {
  name: string
  private employees: string[] = []
  ...
}
```
现在只能通过 `addEmployee` 方法来添加员工，外部代码无法直接访问 `employees` 属性，从而保护了数据的完整性。

## 简化类属性的声明和初始化

```typescript
class Department {
  private id: string
  private name: string

  constructor(id: string, name: string) {
    this.id = id
    this.name = name
  }
}
```

可以简化为：
```typescript
class Department {
  constructor(private id: string, private name: string) {
  }
}
```

## readonly 修饰符

`readonly` 修饰符用于将类的属性设置为只读属性。一旦赋值后，就不能再修改它们。

```typescript
class Department {
  constructor(private readonly id: string, private name: string) {
  }
} 
```
这个很合理，因为部门的ID通常是固定的，不应该在创建后被修改。

## inheritance 继承

```typescript
class Department {
  private id: string
  private name: string
  private employees: string[] = []

  constructor(id: string, name: string) {
    this.id = id
    this.name = name
  }
}
```

ITDepartment 继承自 Department 类：
```typescript
class ITDepartment extends Department {
  admins: string[]

  constructor(id: string, admins: string[]) {
    super(id, 'IT') // calling the base class constructor
    this.admins = admins
  }
}
```
