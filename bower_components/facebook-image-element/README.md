# &lt;facebook-image&gt;

Web Component wrapper for Facebook Image using Polymer.

> Maintained by [Luiz Tiago](https://github.com/luiztiago).

## Demo

> [Check it live](http://luiztiago.github.io/facebook-image-element).

## Usage

1. Import Web Components' polyfill:

	```html
	<script src="//cdnjs.cloudflare.com/ajax/libs/polymer/0.0.20130711/polymer.min.js"></script>
	```

2. Import Custom Element:

	```html
	<link rel="import" href="src/facebook-image.html">
	```

3. Start using it!

	```html
	<facebook-image object="luiztiago"></facebook-image>
	```

## Options

Attribute  | Options                              | Default             | Description
---        | ---                                  | ---                 | ---
`object`   | *string*                             | ``                  | People, Event, Groups, Page, Application or Photo Album id
`type`     | `square`, `small`, `normal`, `large` | `large`             | Type (size) of image. Check Facebook API and see each width and heigh
`width`    | *int*                                | ``                  | Width of image in pixels (only need int argument)
`height`   | *int*                                | ``                  | Height of image in pixels (only need int argument)


## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## History

* v0.0.1 September 03, 2013
	* Started project using [boilerplate-element](https://github.com/customelements/boilerplate-element)

## License

[MIT License](http://opensource.org/licenses/MIT)