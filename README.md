# qna.js [![Build Status](https://img.shields.io/travis/Alex-ray/qna.svg?branch=master&style=flat)](https://travis-ci.org/Alex-ray/qna)
[![Coverage Status](https://img.shields.io/coveralls/Alex-ray/qna.svg?style=flat)](https://coveralls.io/r/Alex-ray/qna)

> Chat like questions and answers

##Usage

#### [Editable Example](http://jsfiddle.net/57xon9ov/7/)
```html
<body>

	<div class="question-wrapper">
	    <p class="question">
	        <span class="question-snippet"></span>
	        <span class="question-snippet"></span>
	    </p>

	    <form id="question-form" name="question">
				<input name="name" type="text" placeholder="Your Name">
	    </form>
	</div>

	<div class="answer-wrapper">
	    <p class="answer">
	        <span class="answer-snippet"></span>
	        <span class="answer-snippet"></span>
	    </p>
	</div>

	<script src="dist/qna.min.js"></script>
	<script>

	document.addEventListener('DOMContentLoaded', function() {

		var questionText = [
	        {str: 'Hello, '},
	        {str: 'What\'s your name?', pauseDelay: 50}
	    ];

	    var defaultAnswerText = [
	    	{str: 'It\'s, great to meet you'}
	    ];

	    var answerResponder = function ( event, form ) {
	    	event.preventDefault();

	    	var input = form.querySelector('input');

	    	input.blur();

	    	var name = input.value.trim().toLowerCase();

	    	return [
	    		{str: 'Hello, '+name},
	    		{str: 'It\'s, great to meet you'}
	    	];
	    };

	    var answerOpts   = { responder: answerResponder };
	    var questionOpts = { form: '#question-form' };

	    var a = new qna('.answer-wrapper', '.answer-snippet', defaultAnswerText, answerOpts);
		var q = new qna('.question-wrapper', '.question-snippet', questionText, questionOpts);

		q.answer(a) ;
		q.ask( );

	});

	</script>
</body>
```


##Api

In the browser, `qna` is a global variable. In Node, do:

```js
var qna = require('qna');
```

#### var q = new qna(containerElement, nodeSelection, snippets [, opts]);

This will initialize an question on the `containerElements` `nodeSelection` and corresponding `snippets` and options.

- `containerElement` &mdash; A DOM Element or a selector string.
- `nodeSelection`    &mdash; A DOM Node List or a selector string scoped within the `containerElement`.
- `snippets`         &mdash; An ordered Array of `snippetObjects`.
- `snippetObjects`   &mdash; An Object literal with the following properties
	- `str`          &mdash; A String
	- `pauseDelay`   &mdash; A Number representing the delay before typing in milliseconds
	- `typeSpeed`    &mdash; A Number representing the typing speed in milliseconds
- `opts`             &mdash;

Key | Description | Value
:--|:--|:--
`responder` | A function to respond to a form submission | A function with Parameters `formEvent` and `formElement` and Returns a `snippetObject` Array
`form` | The questions form element to respond to | A DOM Element or a selector String
`answer` | The answer to the question | An instance on qna

#### q.ask([callback])

Type the `snippets` to the corresponding `nodeSelection` defined at initialization with an optional callback that will be called after all the snippets have been typed to the screen.

#### q.answer(a, [callback])

`a` is a instance of qna.

`callback` is a function that will be called after the question has been asnwered.

Assign an answer and optional callback to a question.

The answers `a.respond` method will be triggered when the questions form is submitted with the parameters `formEvent` and `formNode`;

#### q.respond([callback, args])

Will trigger the instances responder function with the arguments supplied and set the return value as the instances `snippets` variable and type them to the screen.

## Installation

Install via [npm](https://npmjs.com):

```
$ npm i --save qna
```

Install via [bower](http://bower.io):

```
$ bower i --save alex-ray/qna
```

## License

[MIT](LICENSE)
