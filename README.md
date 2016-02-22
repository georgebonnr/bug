# adebugger

### Easier debugging in your ES6+ arrow functions!
*Arrow functions + expressions are cool and fun, and also annoying to debug.*

before:
```js
const myFunction = () => (
    Math.random() * Math.random()
)
```


old way:
```js
/* change parentheses to brackets, add a return statement, add debugger */
const myFunction = () => {
    debugger
    return Math.random() * Math.random()
}
```
😩 *that's a 4-line diff for one debugger statement (and remember to clean up the explicit return when you change everything back!).*

...

here's a better way:
```js
const myFunction = () => (
    (a=>{debugger})() ||
    Math.random() * Math.random()
)
```
😸


### What does this package do?:
This just makes `(a=>{debugger})() ||` easy to trigger as a snippet in SublimeText or Atom.
![](http://g.recordit.co/D0SNooCOAF.gif)

**Instructions for Sublime Text:**

1. Clone this repo and copy the .sublime-snippet file to: `~/Library/Application\ Support/Sublime\ Text\ 3/Packages/User` (your Sublime Text config might differ slightly)

2. Restart Sublime Text

3. Type 'bug' in any javascript file to activate the snippet.
(feel free to modify `<tabTrigger></tabTrigger>` if you want to change the trigger keyword.)

**Instructions for Atom:***

1. Clone this repo and copy bug.cson

2. See if it works / Submit a PR to update this README with instructions 😃

### Usage Tips:

- You can pass a variable in as an argument to the 'a' param if you're impatient and just want to use this like a beefy console.log
- If you don't care about inspecting the line of code *directly after* your debugger expression before it runs, just `step over` twice to be on your merry way (same as a debugger statement)
- If you do care about inspecting the very next line of code, then the best way to replicate the behavior of a debugger statement is:
    
    1. Go *back up* one level in the call stack:  
    ![](https://www.evernote.com/l/APQCtx8eN-RPvq1tB_TJxeEqej1MrEobYOQB/image.png =210x52)
    
        (you can now see your function's scope and can inspect local vars)
    
    2. 'Step out of current function' (`F11` or `Shift+Cmd+;` in Chrome DevTools) to break out of the debugger expression scope and execute the next line of your code.
