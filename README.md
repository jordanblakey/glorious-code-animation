# Glorious Demo

> The easiest way to demonstrate your code in action.

## Installation

```
npm install @glorious/demo --save
```

## Basic Usage

```html
<link rel="stylesheet" href="node_modules/@glorious/demo/dist/gdemo.min.css">
<script src="node_modules/@glorious/demo/dist/gdemo.min.js"></script>
```

```javascript
const demo = new GDemo('#container');

const code = `
function greet(){
  console.log("Hello World!");
}

greet();
`;

demo
  .openApp('editor', { minHeight: '350px', windowTitle: 'demo.js' })
  .write(code, { onCompleteDelay: 1500 })
  .openApp('terminal', { minHeight: '350px', promptString: '$' })
  .command('node ./demo', { onCompleteDelay: 500 })
  .respond('Hello World!')
  .command('')
  .end();
```

### API

#### `openApp`

Opens or maximizes an open application.

```javascript
/*
** @applicationType: String [required]
** @options: Object [optional]
*/

// Possible values are 'editor' or 'terminal'
const applicationType = 'terminal';

const openAppOptions = {
  minHeight: '350px',
  windowTitle: 'bash',
  promptString: '~/my-project $', // for 'terminal' applications only
  onCompleteDelay: 1000 // Delay before executing the next method
};

demo.openApp(applicationType, openAppOptions).end();
```

#### `write`

Writes some code in the open Editor application.

```javascript
/*
** @codeSample: String [required]
** @options: Object [optional]
*/

// Tabs and line breaks will be preserved
const codeSample = `
function sum(a, b) {
  return a + b;
}

sum();
`;

const writeOptions = {
  onCompleteDelay: 500 // Delay before executing the next method
};

demo
  .openApp('editor')
  .write(codeSample, writeOptions)
  .end();
```

#### `command`

Writes some command in the open Terminal application.

```javascript
/*
** @command: String [required]
** @options: Object [optional]
*/

const command = 'npm install @glorious/demo --save';

// Redefines prompt string for this and following commands
const promptString = '$';

// Can optionally be an HTML string:
const promptString = '<span class="my-custom-class">$</span>';

const commandOptions = {
  promptString,
  onCompleteDelay: 500 // Delay before executing the next method
};

demo
  .openApp('terminal')
  .command(command, commandOptions)
  .end();
```

#### `respond`

Shows some response on the open Terminal application.

```javascript
/*
** @response: String [required]
** @options: Object [optional]
*/

// Line breaks will be preserved
const response = `
+ @glorious/demo successfully installed!
+ v0.1.0
`;

// Can optionally be an HTML string:
const response = `
<div><span class="my-custom-class">+</span> @glorious/demo successfully installed!</div>
<div><span class="my-custom-class">+</span> v0.6.0</div>
`;

const respondOptions = {
  onCompleteDelay: 500 // Delay before executing the next method
};

demo
  .openApp('terminal')
  .respond(response, respondOptions)
  .end();
```

#### `end`

Indicates the end of the demonstration. Do not forget to invoke it at the end of your demo. Otherwise, the demo won't be played.
