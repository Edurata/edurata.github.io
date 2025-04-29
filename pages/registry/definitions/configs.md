---
layout: default
title: Schema
parent: Definitions
grand_parent: Registry
---
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [@edurata/types](#eduratatypes)
  - [Table of contents](#table-of-contents)
    - [Interfaces](#interfaces)
    - [Type Aliases](#type-aliases)
  - [Type Aliases](#type-aliases-1)
    - [Step](#step)
    - [StepBase](#stepbase)
    - [StepDependencyNested](#stepdependencynested)
    - [StepDependencyString](#stepdependencystring)
    - [StepWithInline](#stepwithinline)
    - [StepWithSource](#stepwithsource)
- [Interfaces](#interfaces-1)
  - [Interface: ComputeResources](#interface-computeresources)
    - [Table of contents](#table-of-contents-1)
    - [Properties](#properties)
  - [Interface: Config](#interface-config)
    - [Hierarchy](#hierarchy)
    - [Table of contents](#table-of-contents-2)
    - [Properties](#properties-1)
  - [Interface: FunctionConfig](#interface-functionconfig)
    - [Hierarchy](#hierarchy-1)
    - [Table of contents](#table-of-contents-3)
    - [Properties](#properties-2)
  - [Interface: Interface](#interface-interface)
    - [Table of contents](#table-of-contents-4)
    - [Properties](#properties-3)
  - [Interface: InterfaceProperty](#interface-interfaceproperty)
    - [Table of contents](#table-of-contents-5)
    - [Properties](#properties-4)
  - [Interface: Registry](#interface-registry)
    - [Table of contents](#table-of-contents-6)
    - [Properties](#properties-5)
  - [Interface: SourceImageRepo](#interface-sourceimagerepo)
    - [Table of contents](#table-of-contents-7)
    - [Properties](#properties-6)
  - [Interface: SourceRegistry](#interface-sourceregistry)
    - [Table of contents](#table-of-contents-8)
    - [Properties](#properties-7)
  - [Interface: SourceRepo](#interface-sourcerepo)
    - [Table of contents](#table-of-contents-9)
    - [Properties](#properties-8)
  - [Interface: StepDependency](#interface-stepdependency)
    - [Table of contents](#table-of-contents-10)
    - [Properties](#properties-9)
  - [Interface: WorkflowConfig](#interface-workflowconfig)
    - [Hierarchy](#hierarchy-2)
    - [Table of contents](#table-of-contents-11)
    - [Properties](#properties-10)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


<a name="readmemd"></a>

@edurata/types

# @edurata/types

## Table of contents

### Interfaces

- [ComputeResources](#interfacescomputeresourcesmd)
- [Config](#interfacesconfigmd)
- [FunctionConfig](#interfacesfunctionconfigmd)
- [Interface](#interfacesinterfacemd)
- [InterfaceProperty](#interfacesinterfacepropertymd)
- [Registry](#interfacesregistrymd)
- [SourceImageRepo](#interfacessourceimagerepomd)
- [SourceRegistry](#interfacessourceregistrymd)
- [SourceRepo](#interfacessourcerepomd)
- [StepDependency](#interfacesstepdependencymd)
- [WorkflowConfig](#interfacesworkflowconfigmd)

### Type Aliases

- [Step](#step)
- [StepBase](#stepbase)
- [StepDependencyNested](#stepdependencynested)
- [StepDependencyString](#stepdependencystring)
- [StepWithInline](#stepwithinline)
- [StepWithSource](#stepwithsource)

## Type Aliases

### Step

Ƭ **Step**: [`StepWithSource`](#stepwithsource) \| [`StepWithInline`](#stepwithinline)

___

### StepBase

Ƭ **StepBase**: `Object`

#### Type declaration

| Name | Type | Description |
| :------ | :------ | :------ |
| `description?` | `string` | An additional description next to the key of the step. |
| `foreach?` | [`StepDependencyNested`](#stepdependencynested) | If defined and the dependency is of type array, this step will loop over the array. The props attribute can then use "each" as StepDependencySchema.stepId, pointing to each iteration. |
| `if?` | `string` | If defined, this step will only execute if the condition is true. The condition is a javascript boolean expression. |
| `props?` | \{ `[key: string]`: [`StepDependencyNested`](#stepdependencynested);  } | Specifies where to get the input data (from other steps or the global inputs of the workflow defined in the "interface" attribute at the top). Each key must be an input of this step and should be defined in FunctionSchema.interface.inputs of the function defined in "source". |

___

### StepDependencyNested

Ƭ **StepDependencyNested**: \{ `[key: string]`: [`StepDependencyNested`](#stepdependencynested);  } \| [`StepDependencyNested`](#stepdependencynested)[] \| [`StepDependency`](#interfacesstepdependencymd) \| [`StepDependencyString`](#stepdependencystring)

___

### StepDependencyString

Ƭ **StepDependencyString**: \`$\{string}.$\{string \| ""}.$\{string \| ""}\`

Schema for a string representing an educational function step dependency.

**`Example`**

```ts
"stepId.outputId.outputPath"
```

___

### StepWithInline

Ƭ **StepWithInline**: [`StepBase`](#stepbase) & [`FunctionConfig`](#interfacesfunctionconfigmd)

Schema for a workflow step with a function directly defined inline with code property

___

### StepWithSource

Ƭ **StepWithSource**: [`StepBase`](#stepbase) & \{ `source?`: `Source`  }

Schema for a workflow step with source

# Interfaces


<a name="interfacescomputeresourcesmd"></a>

[@edurata/types](#readmemd) / ComputeResources

## Interface: ComputeResources

### Table of contents

#### Properties

- [cpu](#cpu)
- [memory](#memory)

### Properties

#### cpu

• **cpu**: `number`

The number of vCPUs to allocate for the function. The available CPU values depend on the amount of memory allocated to the function and vice versa.
0.25 vCPU - Available memory values: 0.5 GB, 1 GB, 2 GB

 0.5 vCPU - Available memory values: 1 GB, 2 GB, 3 GB, 4 GB

 1 vCPU - Available memory values: 2 GB, 3 GB, 4 GB, 5 GB, 6 GB, 7 GB, 8 GB

 2 vCPU - Available memory values: 4 GB, 16 GB in increments of 1 GB

 4 vCPU - Available memory values: 8 GB, 30 GB in increments of 1 GB

 8 vCPU - Available memory values: 16 GB, 60 GB in 4 GB increments
 This option requires Linux platform 1.4.0 or later.
 16 vCPU - Available memory values: 32 GB, 120 GB in 8 GB increments
 This option requires Linux platform 1.4.0 or later.

**`Example`**

```ts
"2"
```

___

#### memory

• **memory**: `number`

The memory allocated. The available memory values depend on the amount of vCPUs allocated to the function and vice versa. See above

**`Example`**

```ts
"16"
```


<a name="interfacesconfigmd"></a>

[@edurata/types](#readmemd) / Config

## Interface: Config

### Hierarchy

- **`Config`**

  ↳ [`WorkflowConfig`](#interfacesworkflowconfigmd)

  ↳ [`FunctionConfig`](#interfacesfunctionconfigmd)

### Table of contents

#### Properties

- [description](#description)
- [inputs](#inputs)
- [interface](#interface)
- [name](#name)
- [outputs](#outputs)
- [title](#title)

### Properties

#### description

• `Optional` **description**: `string`

An additional description of the workflow or function

___

#### inputs

• `Optional` **inputs**: `Object`

The global inputs of the workflow (or function). These can be used in any step of the workflow. Here fixed values or secrets or variables can be accessed.
 *

**`Example`**

```ts
{ "name": "${variables.employees.top}" }
 *
```

**`Example`**

```ts
{ "name": "John" }
 *
```

**`Example`**

```ts
{ "password": "${secrets.password}" }
```

##### Index signature

▪ [key: `string`]: [`StepDependencyNested`](#stepdependencynested)

___

#### interface

• `Optional` **interface**: [`Interface`](#interfacesinterfacemd)

The schema of inputs and outputs of this workflow or function

___

#### name

• `Optional` **name**: `string`

An identifier that is unique in the registry. It is used as reference in deployments or workflows.

___

#### outputs

• `Optional` **outputs**: `Object`

Outputs of the workflow or function that can be used as inputs in other workflows or functions or just to inspect the output.

##### Index signature

▪ [key: `string`]: [`StepDependencyNested`](#stepdependencynested)

___

#### title

• `Optional` **title**: `string`

A short title that describes the workflow or function. This is NOT the id that will be used in the registry!


<a name="interfacesfunctionconfigmd"></a>

[@edurata/types](#readmemd) / FunctionConfig

## Interface: FunctionConfig

Represents the configuration schema for a function.

### Hierarchy

- [`Config`](#interfacesconfigmd)

  ↳ **`FunctionConfig`**

### Table of contents

#### Properties

- [apiRevision](#apirevision)
- [code](#code)
- [description](#description)
- [entrypoint](#entrypoint)
- [exclude](#exclude)
- [include](#include)
- [inputs](#inputs)
- [interface](#interface)
- [name](#name)
- [outputs](#outputs)
- [registry](#registry)
- [runtime](#runtime)
- [title](#title)

### Properties

#### apiRevision

• `Optional` **apiRevision**: ``"edurata.io/function/v1"``

Refers to the version of this schema and should be updated whenever the schema changes

___

#### code

• `Optional` **code**: `string`

Inline code. You don't need to put the handler function and can write the content of the function directly

___

#### description

• `Optional` **description**: `string`

An additional description of the workflow or function

##### Inherited from

[Config](#interfacesconfigmd).[description](#description)

___

#### entrypoint

• `Optional` **entrypoint**: `string`

Points to the entrypoint of the function. Defaults to index.js, index.py, index.sh, etc.

___

#### exclude

• `Optional` **exclude**: `string`[]

Specifies which files to exclude from the function. Can be a glob pattern. Defaults to none.

___

#### include

• `Optional` **include**: `string`[]

Specifies which files to include in the function. Can be a glob pattern. Defaults to all files in the same directory as the entrypoint.

___

#### inputs

• `Optional` **inputs**: `Object`

The global inputs of the workflow (or function). These can be used in any step of the workflow. Here fixed values or secrets or variables can be accessed.
 *

**`Example`**

```ts
{ "name": "${variables.employees.top}" }
 *
```

**`Example`**

```ts
{ "name": "John" }
 *
```

**`Example`**

```ts
{ "password": "${secrets.password}" }
```

##### Index signature

▪ [key: `string`]: [`StepDependencyNested`](#stepdependencynested)

##### Inherited from

[Config](#interfacesconfigmd).[inputs](#inputs)

___

#### interface

• `Optional` **interface**: [`Interface`](#interfacesinterfacemd)

The schema of inputs and outputs of this workflow or function

##### Inherited from

[Config](#interfacesconfigmd).[interface](#interface)

___

#### name

• `Optional` **name**: `string`

An identifier that is unique in the registry. It is used as reference in deployments or workflows.

##### Inherited from

[Config](#interfacesconfigmd).[name](#name)

___

#### outputs

• `Optional` **outputs**: `Object`

Outputs of the workflow or function that can be used as inputs in other workflows or functions or just to inspect the output.

##### Index signature

▪ [key: `string`]: [`StepDependencyNested`](#stepdependencynested)

##### Inherited from

[Config](#interfacesconfigmd).[outputs](#outputs)

___

#### registry

• `Optional` **registry**: [`Registry`](#interfacesregistrymd)

If the source shouldn't be built but is already in an external registry, you can point to it here.

___

#### runtime

• `Optional` **runtime**: ``"nodejs20"`` \| ``"python3_10"`` \| ``"docker"``

Specifies the programming language the code is written in.

___

#### title

• `Optional` **title**: `string`

A short title that describes the workflow or function. This is NOT the id that will be used in the registry!

##### Inherited from

[Config](#interfacesconfigmd).[title](#title)


<a name="interfacesinterfacemd"></a>

[@edurata/types](#readmemd) / Interface

## Interface: Interface

Schema for an interface of a workflow or function.

**`Example`**

```typescript
{
 inputs: {
   required: ["name"],
   properties: {
     name: {
       type: "string",
       title: "Name",
       description: "The name of the person",
     }
  }
}
```

### Table of contents

#### Properties

- [inputs](#inputs)
- [outputs](#outputs)

### Properties

#### inputs

• `Optional` **inputs**: `Object`

##### Type declaration

| Name | Type |
| :------ | :------ |
| `properties?` | \{ `[key: string]`: [`InterfaceProperty`](#interfacesinterfacepropertymd);  } |
| `required?` | `string`[] |
| `type?` | ``"object"`` |

___

#### outputs

• `Optional` **outputs**: `Object`

##### Type declaration

| Name | Type |
| :------ | :------ |
| `properties?` | \{ `[key: string]`: [`InterfaceProperty`](#interfacesinterfacepropertymd);  } |
| `required?` | `string`[] |
| `type?` | ``"object"`` |


<a name="interfacesinterfacepropertymd"></a>

[@edurata/types](#readmemd) / InterfaceProperty

## Interface: InterfaceProperty

Inspired by JSON Schema for easier conversion from and to other tools.

**`See`**

https://tools.ietf.org/html/draft-handrews-json-schema-validation-01

### Table of contents

#### Properties

- [const](#const)
- [default](#default)
- [description](#description)
- [enum](#enum)
- [examples](#examples)
- [items](#items)
- [properties](#properties)
- [required](#required)
- [title](#title)
- [type](#type)

### Properties

#### const

• `Optional` **const**: [`InterfaceProperty`](#interfacesinterfacepropertymd)

___

#### default

• `Optional` **default**: `any`

___

#### description

• `Optional` **description**: `string`

___

#### enum

• `Optional` **enum**: (`string` \| `number` \| `boolean`)[]

___

#### examples

• `Optional` **examples**: [`InterfaceProperty`](#interfacesinterfacepropertymd)[]

___

#### items

• `Optional` **items**: [`InterfaceProperty`](#interfacesinterfacepropertymd)

___

#### properties

• `Optional` **properties**: `Object`

##### Index signature

▪ [key: `string`]: [`InterfaceProperty`](#interfacesinterfacepropertymd)

___

#### required

• `Optional` **required**: `string`[]

___

#### title

• `Optional` **title**: `string`

___

#### type

• **type**: ``"string"`` \| ``"number"`` \| ``"bigint"`` \| ``"boolean"`` \| ``"undefined"`` \| ``"object"`` \| ``"array"`` \| ``"integer"`` \| ``"null"`` \| ``"any"`` \| ``"file"`` \| ``"env"`` \| ``"cmdValue"`` \| ``"cmdKeyValue"`` \| ``"meta"`` \| ``"dependency"`` \| ``"interpolation"``


<a name="interfacesregistrymd"></a>

[@edurata/types](#readmemd) / Registry

## Interface: Registry

If a registry is used, this is the schema for it. Currently only supported for runtime: "docker"

**`Example`**

```ts
url: "docker.io/edurata", tag: "latest"
```

**`Example`**

```ts
url: "ghcr.io/edurata", tag: "latest"
```

### Table of contents

#### Properties

- [tag](#tag)
- [url](#url)

### Properties

#### tag

• **tag**: `string`

___

#### url

• **url**: `string`


<a name="interfacessourceimagerepomd"></a>

[@edurata/types](#readmemd) / SourceImageRepo

## Interface: SourceImageRepo

If the source is an image, you can point to an image repo and its tag.

### Table of contents

#### Properties

- [imageRepoUrl](#imagerepourl)
- [tag](#tag)

### Properties

#### imageRepoUrl

• **imageRepoUrl**: `string`

The url of the image repository. If dockerhub is used, url is optional.

**`Example`**

```ts
"docker.io/edurata"
```

**`Example`**

```ts
"ghcr.io/edurata"
```

**`Example`**

```ts
"quay.io/edurata"
```

___

#### tag

• **tag**: `string`

The tag of the image.

**`Example`**

```ts
"latest"
```

**`Example`**

```ts
"12"
```

**`Example`**

```ts
"1.0.0"
```


<a name="interfacessourceregistrymd"></a>

[@edurata/types](#readmemd) / SourceRegistry

## Interface: SourceRegistry

If the source is already in the registry you can point to an entry of the registry.

### Table of contents

#### Properties

- [name](#name)
- [revision](#revision)

### Properties

#### name

• **name**: `string`

The name of the function in the registry.

**`Example`**

```ts
"my-function"
```

___

#### revision

• `Optional` **revision**: `string`

The revision of the function in the registry.

**`Example`**

```ts
"12"
```


<a name="interfacessourcerepomd"></a>

[@edurata/types](#readmemd) / SourceRepo

## Interface: SourceRepo

If the source is a git repository, this is the schema for it.

### Table of contents

#### Properties

- [path](#path)
- [ref](#ref)
- [repoUrl](#repourl)

### Properties

#### path

• `Optional` **path**: `string`

the path of where to find the function code inside the repository

**`Example`**

```ts
"tests/sleep"
```

___

#### ref

• `Optional` **ref**: `string`

The ref of the git repository to use. Defaults to "main".

**`Example`**

```ts
"main"
```

___

#### repoUrl

• **repoUrl**: `string`

the url of the git repository

**`Example`**

```ts
"https://github.com/Edurata/edurata-functions"
```


<a name="interfacesstepdependencymd"></a>

[@edurata/types](#readmemd) / StepDependency

## Interface: StepDependency

Schema for an educational function step dependency.

**`Example`**

assuming the step "inputs" has an output "name" with the value "John"
```typescript
{
 stepId: "inputs",
 outputId: "name",
}
```

**`Example`**

assuming the step "inputs" has an output "name" that is a complex object with a key "firstName" with the value "John"
```typescript
{
 stepId: "inputs",
 outputId: "name",
 outputPath: "firstName",
}
```

### Table of contents

#### Properties

- [outputId](#outputid)
- [outputPath](#outputpath)
- [stepId](#stepid)
- [value](#value)

### Properties

#### outputId

• `Optional` **outputId**: `string`

the name of the output of a step (thereby its function). has to be one of the outputs defined in
FunctionSchema.interface.outputs of the dependent step mentioned with "stepId"

___

#### outputPath

• `Optional` **outputPath**: `string`[]

only used when the output is a complex object and the value is inside. is a string with dot notation
to point to the value. e.g. "data.name" to point to the value of the key "name" inside the object
"data".

**`Example`**

```ts
["data", "name"]
```

___

#### stepId

• `Optional` **stepId**: `string`

the step which to depend on. Needs to be one defined in the "steps" attribute of the workflow
definition. Can be "inputs" to refer to the global inputs of the workflow. Can be "each" if the
attribute "foreach" in the parent step is defined.

___

#### value

• `Optional` **value**: `string`

If you want to pass in a value directly instead of a step dependency, you can use this attribute.
You can also use interpolation here.

**`Example`**

```ts
"examplestring"
```

**`Example`**

```ts
"${inputs.name} is here!"
```


<a name="interfacesworkflowconfigmd"></a>

[@edurata/types](#readmemd) / WorkflowConfig

## Interface: WorkflowConfig

Represents the configuration schema for a workflow.

### Hierarchy

- [`Config`](#interfacesconfigmd)

  ↳ **`WorkflowConfig`**

### Table of contents

#### Properties

- [apiRevision](#apirevision)
- [description](#description)
- [inputs](#inputs)
- [interface](#interface)
- [name](#name)
- [outputs](#outputs)
- [schedule](#schedule)
- [steps](#steps)
- [title](#title)

### Properties

#### apiRevision

• `Optional` **apiRevision**: ``"edurata.io/workflow/v1"``

Refers to the version of this schema and should be updated whenever the schema changes

___

#### description

• `Optional` **description**: `string`

An additional description of the workflow or function

##### Inherited from

[Config](#interfacesconfigmd).[description](#description)

___

#### inputs

• `Optional` **inputs**: `Object`

The global inputs of the workflow (or function). These can be used in any step of the workflow. Here fixed values or secrets or variables can be accessed.
 *

**`Example`**

```ts
{ "name": "${variables.employees.top}" }
 *
```

**`Example`**

```ts
{ "name": "John" }
 *
```

**`Example`**

```ts
{ "password": "${secrets.password}" }
```

##### Index signature

▪ [key: `string`]: [`StepDependencyNested`](#stepdependencynested)

##### Inherited from

[Config](#interfacesconfigmd).[inputs](#inputs)

___

#### interface

• `Optional` **interface**: [`Interface`](#interfacesinterfacemd)

The schema of inputs and outputs of this workflow or function

##### Inherited from

[Config](#interfacesconfigmd).[interface](#interface)

___

#### name

• `Optional` **name**: `string`

An identifier that is unique in the registry. It is used as reference in deployments or workflows.

##### Inherited from

[Config](#interfacesconfigmd).[name](#name)

___

#### outputs

• `Optional` **outputs**: `Object`

Outputs of the workflow or function that can be used as inputs in other workflows or functions or just to inspect the output.

##### Index signature

▪ [key: `string`]: [`StepDependencyNested`](#stepdependencynested)

##### Inherited from

[Config](#interfacesconfigmd).[outputs](#outputs)

___

#### schedule

• `Optional` **schedule**: `string`

A cron schedule that determines when the workflow should be executed.

**`Example`**

```ts
"0 0 * * *" -> every day at midnight
```

**`Example`**

```ts
"0 0 * * 0" -> every sunday at midnight
```

**`Example`**

```ts
"0 0 1 * *" -> every first day of the month at midnight
```

**`Example`**

```ts
"0 0 1 1 *" -> every first day of the year at midnight
```

**`Example`**

```ts
"0 0 1 1 0" -> every first sunday of the year at midnight
```

___

#### steps

• **steps**: `Object`

Each step of the workflow specified by a unique key and its definition as a value.
The order of execution and dataflow is inferred by "props".

##### Index signature

▪ [key: `string`]: [`Step`](#step)

___

#### title

• `Optional` **title**: `string`

A short title that describes the workflow or function. This is NOT the id that will be used in the registry!

##### Inherited from

[Config](#interfacesconfigmd).[title](#title)


<a name="schemamd"></a>
