[![Orange banner indicating a preview software component][release-level-banner--unstable]](##)

<br />

<!-- markdownlint-disable-next-line line-length -->
<a href="##"><img src="https://raw.githubusercontent.com/OpenINF/openinf.github.io/live/assets/img/svg/logogram-color.svg?sanitize=true" alt="OpenINF logo" title="OpenINF" align="right" height="96" width="96" /></a>

<div align="left">

## `@openinf/tempy`

> Get a random temporary file or directory path

<br />

[!['View on npm'][npm-badge--shields]][npm-badge-url]
[!['License: MIT/Apache-2.0'][license-badge--shields]][license-badge-url]

</div>

<br />

The high-level goal of `@openinf/tempy` is to serve as a Node.js package
containing utilities for **creating random temporary file and directory paths**
that are automatically cleaned up once finished with. We are constantly working
to improve this repository, so please feel free to [contribute](#contributing)
if you notice any omissions or errors.

Thanks!

<br />

<details id="platform--node-js-lts">
	<summary>
		<a
			href="#platform--node-js-lts"
			title="Platform: Node.js LTS"
		>
			<img
				src="https://img.shields.io/badge/Node.js-LTS-black?logo=Node.js&logoColor=lightgreen&color=2a2a2a&labelColor=black"
				alt="Platform: Node.js LTS"
			/>
		</a>
	</summary>
	<div align="left"><br />
		<a
			target="_blank"
			title="Node.js release schedule"
			href="https://github.com/nodejs/release#release-schedule"
		>
			<strong>Supported Node.js Environments</strong>
		</a><br /><br />

- [ ] v4：Argon (Ar)
- [ ] v6：Boron (B)
- [ ] v8：Carbon (C)
- [ ] v10：Dubnium (Db)
- [ ] v12：Erbium (Er)
- [x] v14：Fermium (Fm)
- [x] v16：Gallium (Ga)
- [x] v18：Hydrogen (H)
<!-- TODO
- [x] v20: Iron (Fe) -->

</div></details>

<br />

<div align="center">

[![Code Style: Prettier][prettier-badge]][prettier-url]
[![Commit Style: Conventional Commits][conventional-commits-badge]][conventional-commits-url]
[![Chat on Matrix][matrix-badge--shields]][matrix-url]

</div>

<br /><br />

---

<br />

### Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [API](#api)
- [Contributing](#contributing)
- [License](#license)

<br /><br />

---

<br />

### Installation

`@openinf/tempy` runs on
[supported versions of Node.js](#platform--node-js-lts) and is available via
**`npm`**, **`pnpm`**, or **`yarn`**.

**Using the npm CLI**

<sup>See the
[official documentation for this command](https://docs.npmjs.com/cli/commands/npm-install)
for more information.</sup>

```shell
npm i @openinf/tempy
```

**Using the pnpm CLI**

<sup>See the
[official documentation for this command](https://pnpm.io/cli/add) for more
information.</sup>

```shell
pnpm add @openinf/tempy
```

**Using the Yarn 1 CLI (Classic)**

<sup>See the
[official documentation for this command](https://classic.yarnpkg.com/en/docs/cli/add)
for more information.</sup>

```shell
yarn add @openinf/tempy
```

<br /><br />

### Usage

```js
import { temporaryFile, temporaryDirectory } from '@openinf/tempy';

temporaryFile();
//=> '/private/var/folders/3x/jf5977fn79jbglr7rk0tq4d00000gn/T/4f504b9edb5ba0e89451617bf9f971dd'

temporaryFile({ extension: 'png' });
//=> '/private/var/folders/3x/jf5977fn79jbglr7rk0tq4d00000gn/T/a9fb0decd08179eb6cf4691568aa2018.png'

temporaryFile({ name: 'unicorn.png' });
//=> '/private/var/folders/3x/jf5977fn79jbglr7rk0tq4d00000gn/T/f7f62bfd4e2a05f1589947647ed3f9ec/unicorn.png'

temporaryDirectory();
//=> '/private/var/folders/3x/jf5977fn79jbglr7rk0tq4d00000gn/T/2f3d094aec2cb1b93bb0f4cffce5ebd6'

temporaryDirectory({ prefix: 'name' });
//=> '/private/var/folders/3x/jf5977fn79jbglr7rk0tq4d00000gn/T/name_3c085674ad31223b9653c88f725d6b41'
```

<br /><br />

### API

#### temporaryFile(options?)

Get a temporary file path you can write to.

#### temporaryFileTask(callback, options?)

The `callback` resolves with a temporary file path you can write to. The file is automatically cleaned up after the callback is executed. Returns a promise that resolves with the return value of the callback after it is executed and the file is cleaned up.

##### callback

Type: `(tempPath: string) => void`

A callback that is executed with the temp file path. Can be asynchronous.

##### options

Type: `object`

*You usually won't need either the `extension` or `name` option. Specify them only when actually needed.*

###### extension

Type: `string`

File extension.

###### name

Type: `string`

Filename. Mutually exclusive with the `extension` option.

#### temporaryDirectory(options?)

Get a temporary directory path. The directory is created for you.

#### temporaryDirectoryTask(callback, options?)

The `callback` resolves with a temporary directory path you can write to. The directory is automatically cleaned up after the callback is executed. Returns a promise that resolves with the return value of the callback after it is executed and the directory is cleaned up.

###### callback

Type: `(tempPath: string) => void`

A callback that is executed with the temp directory path. Can be asynchronous.

##### options

Type: `Object`

###### prefix

Type: `string`

Directory prefix.

Useful for testing by making it easier to identify cache directories that are created.

*You usually won't need this option. Specify it only when actually needed.*

#### temporaryWrite(fileContent, options?)

Write data to a random temp file.

#### temporaryWriteTask(fileContent, callback, options?)

Write data to a random temp file. The file is automatically cleaned up after the callback is executed. Returns a promise that resolves with the return value of the callback after it is executed and the file is cleaned up.

###### fileContent

Type: `string | Buffer | TypedArray | DataView | stream.Readable`

Data to write to the temp file.

###### callback

Type: `(tempPath: string) => void`

A callback that is executed with the temp file path. Can be asynchronous.

###### options

See [options](#options).

#### temporaryWriteSync(fileContent, options?)

Synchronously write data to a random temp file.

###### fileContent

Type: `string | Buffer | TypedArray | DataView`

Data to write to the temp file.

###### options

See [options](#options).

#### rootTemporaryDirectory

Get the root temporary directory path. For example: `/private/var/folders/3x/jf5977fn79jbglr7rk0tq4d00000gn/T`

<br /><br />

---

<br />

### Contributing

Pull requests are welcome. For major changes, please open an issue first to
discuss what you would like to change. If for whatever reason you spot something
to fix but cannot patch it yourself, please [open an issue][].

<br />

### License

This project is licensed under either of

- [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0)
- [MIT license](https://opensource.org/licenses/MIT)

at your option.

The [SPDX](https://spdx.dev) license identifier for this project is
`MIT OR Apache-2.0`.

<br /><br />

---

<br />

<div align="center">

### Show Your Support

<br />

If you like the project (or want to bookmark it)&nbsp;&mdash;<br />
&mdash;&nbsp;[give it a star ⭐️][]&nbsp;&mdash;&nbsp;it will greatly encourage
us.

<br /><br />

<a title="The OpenINF website" href="https://open.inf.is" rel="author">
  <img alt="The OpenINF logo" height="32px" width="32px" src="https://raw.githubusercontent.com/openinf/openinf.github.io/live/assets/img/svg/logo.svg?sanitize=true" />
</a>

</div>

<br /><br />

[![Orange banner indicating a preview software component][release-level-banner--unstable]](##)

<!-- BEGIN LINK DEFINITIONS -->
[conventional-commits-badge]: https://img.shields.io/badge/commit%20style-Conventional-%23fa6673?logoColor=white&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAzMCAzMCI+PHBhdGggc3R5bGU9ImZpbGw6ICNGRkYiIGQ9Ik0xNSwyQTEzLDEzLDAsMSwxLDIsMTUsMTMsMTMsMCwwLDEsMTUsMm0wLTJBMTUsMTUsMCwxLDAsMzAsMTUsMTUsMTUsMCwwLDAsMTUsMFoiLz48L3N2Zz4K 'Commit Style: Conventional Commits'
[conventional-commits-url]: https://www.conventionalcommits.org 'Commit Style: Conventional Commits'
[give it a star ⭐️]: https://github.com/OpenINF/openinf-tempy/stargazers
[license-badge--shields]: https://img.shields.io/badge/license-MIT%2FApache--2.0-blue.svg?logo=github 'License: MIT/Apache 2.0'
[license-badge-url]: #license 'License: MIT/Apache 2.0'
[matrix-badge--shields]: https://img.shields.io/badge/matrix-join%20chat-%2346BC99?logo=matrix 'Chat on Matrix'
[matrix-url]: https://matrix.to/#/#openinf-space:matrix.org 'You&apos;re invited to talk on Matrix'
[npm-badge--shields]: https://img.shields.io/npm/v/@openinf/tempy/latest.svg?logo=npm&color=fe7d37 'View on npm'
[npm-badge-url]: https://www.npmjs.com/package/@openinf/tempy#top 'View on npm'
[open an issue]: https://github.com/OpenINF/openinf-tempy/issues
[prettier-badge]: https://img.shields.io/badge/code_style-Prettier-ff69b4.svg?logo=prettier 'Code Style: Prettier'
[prettier-url]: https://prettier.io/playground 'Code Style: Prettier'
[project-status-badge]: https://img.shields.io/badge/project%20status-under%20construction-orange 'Project Status: Under construction badge'
[release-level-banner--unstable]: https://raw.githubusercontent.com/OpenINF/openinf.github.io/live/assets/img/svg/release-level-banner--unstable.svg?sanitize=true 'Banner for Release Level: Unstable'
<!-- END LINK DEFINITIONS -->
