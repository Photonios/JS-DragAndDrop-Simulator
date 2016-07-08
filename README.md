# js-drag-and-drop-simulator
Pure JavaScript implementation HTML5 drag & drop simulator. It is to be used in UI tests using WebDriver.

Most WebDriver implementations by major browser vendors have not yet properly implemented support for automating HTML5 drag and drop. Although it's actively being worked on, it is not yet there.

	https://bugs.chromium.org/p/chromedriver/issues/detail?id=1392#c4

Until then, this is the only solution. Existing implementations:

* Are incomplete
* Are incorrect
* Depend on frameworks such as jQuery.

The most widely spread example of this is:

	https://gist.github.com/rcorreia/2362544

Which doesn't work correctly since it fails to implement the `DataTransfer` object correctly, neither does it implement all the drag and drop events. This solution does all of that and is written in pure JavaScript. It dispatches the following events in the following order:

* `mousedown`
* `dragstart`
* `drag`
* `dragenter`
* `dragover`
* `drop`
* `dragend`
* `mouseup`

Which is exactly what the browser emits when you perform the drag and drop manually. On top of that, it more properly implements the `DataTransfer` object described here:

	https://developer.mozilla.org/en-US/docs/Web/API/DataTransfer

## Using
All you have to do is figure out how to execute JavaScript code in your UI automation framework. In Selenium C# this would be:

	IJavaScriptExecutor executor = driver as IJavaScriptExecutor;
	executor.ExecuteScript("js code here");

Inject the code contained in `dndsim.js` and then you can call the following JavaScript code to perform the drag and drop:

	DndSimulator.simulate('#sourceElem', '#targetElem');

You can pass in CSS selectors or a JavaScript `HTMLElement` object.

## License
This code is licensed under the MIT license. See `LICENSE` for more information or visit:

	https://opensource.org/licenses/MIT