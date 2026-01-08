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
    // "sourceMap": true,                                /* Create source map files for emitted JavaScript files. */
    // "inlineSourceMap": true,                          /* Include sourcemap files inside the emitted JavaScript. */
    // "noEmit": true,                                   /* Disable emitting files from a compilation. */
    // "outFile": "./",                                  /* Specify a file that bundles all outputs into one JavaScript file. If 'declaration' is true, also designates a file that bundles all .d.ts output. */
    // "outDir": "./",                                   /* Specify an output folder for all emitted files. */
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

