# Functions

Functions are chunks of code with minimal functionality that can be chained together in order to build a workflow. We enforce a minmal amount of conventions to make the whole ecosystem both scaleable and easy to use for everyone.


## Handling of Files (Artefacts)

If you want to make use of the filesystem to create or read from files you have to place them under the `/tmp/` directory. 

If you want to use file/files as input or output of your function you use the `Artefact` type or any of its subtypes provided by the [@edurata/types](https://www.npmjs.com/package/@edurata/types) package in the interface. The function wrapper will automatically handle uploading/downloading the file from cloud storage. 

In order to specify an artefact you either pass in an object of type File or a shorthand string that includes all information about the file.

```typescript
type Path = string // e.g. /path/to/file/
type FileName = string // e.g. foo
type FileType = string // e.g. txt

export type File = {
    path: Path 
    fileName: FileName
    fileType: FileType
}

type FileStr = `file:${Path}/${FileName}.${FileType}`

export type Artefact = File | FileStr

```


## Folder structure

Note that in the following the `root` folder can also be a subfolder in a repository and doesn't have to 
You have freedom about how to structure your files except the following:
- **The root contains an index.ts**: This is the entrypoint of the function and contains the handler function.
- **The root contains a package.json**: In order for us to know which dependencies to install you need to provide a `package.json` in the root directory.
- **The root contains an interface.d.ts**: Since we need information about the signature/interface of your function you need to provide this file that contains only typescript types.

## The handler function

If you have worked with AWS lambda functions before you will know that a handler function is expected in the root directory as an entry point into your function. The convention here is:
- **The handler functions needs to be called handler**.
- **The handler functions needs to be exported**: If you don' export the function it is not possible for our wrapper to pick it up.

## The interface

In order to know which functions are allowed to be chained together we require assumptions about what information to pass in and expect to come out of each of them. This is why an interface is a crucial metainformation attached to your functions code. Luckily for our currently supported runtime `Node.js` you can just use Typescript and strongly type the handler function with a few conventions in order for our compiler to pick it up:

- **Input and output type are objects**: Both the input and output of functions are an object each with several keys-value pairs that represent the actual inputs and outputs. You might be used to positional arguments (parameters) as input coming from javascript functions, meaning that the order of arguments passed to a function is relevant. However edurata functions just expect one object as the first argument, other positional arguments after the first are ignored.
- **You cannot use the any type**: edurata is built on a continously growing public collection of types that should be used to describe your functions. If an interface contains the any type it is not considered ready for usage.
- **You cannot be amiguous about output types**: Output types additionally need to be free of Unions

You have freedom of choice for the following:

- **Import custom types**: You can import custom types of public repositories and use them for your interface
- **No restriction on name of types**: As this is typescript the name of the types is not relevant
- **Input types can be ambiguous**: If you want to be flexible about what data can be passed in you can use [Unions or Intersection types](https://www.typescriptlang.org/docs/handbook/unions-and-intersections.html) 
- **The handler function can be overloaded**: If you want to provide multiple interfaces where the output changes based on the input you can define them through overloading the type that you pass to the handler function.

```typescript
// Import any other types from an open source library to make them available
import type {TypescriptFile, OasFile, UrlString} from "@edurata/types"


type Inputs = {
    oasInput: OasFile | UrlString | string
}

type Outputs = {
    file: TypescriptFile
}

export type Handler = {
    // See here that we pass in only one object "inputs", other arguments are ignored
    (inputs: Inputs): Promise<Outputs>
}

```
*contents of "interface.d.ts"*

## Limitations

We use mostly AWS Lambda functions to execute your functions code. This brings 

