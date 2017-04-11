---
layout: post
title:  "Riot Components"
image: ''
date:   2017-04-10 10:40:00
tags:
- riot
- web
- javascript
description: ''
categories:
- Javascript 
---

<a href="http://riotjs.com/"><img src="http://riotjs.com/made-with-riot/img/logo_2x.png" /></a>

## Another framework? Great...

If you're too *fatigued* out then please head over <a href="https://www.youtube.com/watch?v=SRsnpJxM_GA">here</a> and take a breather. Back? Isn't Endless Forest insane? Anyway, Riot isn't really a framework - it's a neat tiny library for making small view components. It follows the React philosophy in much of it's design except that it's a lot more lightweight.

## How hard is it to make a component?

Here's a fake login component...
{% highlight javascript %}
/// login.tag
<login>
    <label for="username">Name:</label>
    <input ref="username"></input>

    <virtual if={ requiresPass }>
        <label for="password">Pass:</label>
        <input ref="password"></input>
    </virtual>

    <button onclick={ login }>Submit</button>

    <script>
        this.requiresPass = true;

        login() {
            let user = this.refs.username
            let pass = this.refs.password

            fetch(`/login?user=${user}&pass=unsafe${pass}`)
                .then(() => {
                    // Do something
                })
        }
    </script>

    <style>
        :scope {
            display: flex;
            background: black;
            color: white;
            ...

            label, input {
                width: 50%;
            }

            input {
                color: lightgreen;
            }

            button {
                border: 0;
                border-radius: 5px;
                background: orange;
                color: white;
                ...
            }
        }
    </style>
</login>
{% endhighlight %}

There's a LOT going on there so let's break it down.

## The Basics

Riot components are `.tag` files that contain their markup, behavior, and style all in one. They always begin with their name tag
{% highlight javascript %}
    <foo>
    </foo>
{% endhighlight %}
is a valid component.

Their markup comes first.
{% highlight javascript %}
    <foo>
        <h1>Hello Der</h1>
    </foo>
{% endhighlight %}

Once the Riot parser stops finding html tags and finds a javascript or a style tag then it starts parsing that. Entire `.tag` definitions can be laid out in `<script>` tags in an html file if you'd like (in which case you **must** have `<script>` tags wrapping your custom component's behavior) but when they are in their own `.tag` files and imported then the `<script>` wrapping can be ommitted. However I think it's best practice to just always wrap the behavior section, which comes second.
{% highlight javascript %}
    <foo>
        <h1>Hello Der</h1>

        <script>
            this.onAction = () => console.log('did action')
        </script>
    </foo>
{% endhighlight %}

Last but not least comes any styles you want to include. By default the riot compiler expects CSS but it has built in preprocessors so long as you specify it when you compile them. Components may be compiles into bundles as a build task or at runtime.
{% highlight javascript %}
    <foo>
        <h1 onclick={ onAction }>Hello Der</h1>
        <h2 onclick={ myMethod }>Goodbye</h2>

        <script>
            this.onAction = () => console.log('did action')

            myMethod() { console.log('mine!') }
        </script>

        <style>
            :scope {
                background: black;
                display: block;
                color: white;
                font-size: 2em;
            }
        </style>
    </foo>
{% endhighlight %}

## Some key things to notice

Riot is ES6 friendly by default. Anything with a `ref` property is available on `this.refs`. The syntax `{ thing }` will reference `this.thing` from the script section. Anything in the script section that is defined as if it were an ES6 object method (like `myMethod` above) is also referenceable in the template. Using the `:scope` selection allows you to contain your styles to this component only. 

## So how do we actually use this dumb `tag` file?

Grab the riot compiler, `npm install riot -g`. Now you can run `riot foo.tag` and get `foo.js`. Now let's make a simple `index.html`
{% highlight html %}
    <html>
        <head>
            <script src="https://cdnjs.cloudflare.com/ajax/libs/riot/3.4.1/riot.min.js"></script>
            <script src="./foo.js"></script>
        </head>
        <body>
            <foo></foo>
            <script>
                riot.mount('foo');
            </script>
        </body>
    </html>
{% endhighlight %}

The `riot.mount` call is what instructs riot to bootstrap up the element, the `mount` method has a few useful permutations for actions like
- bootstrapping a particular component
- bootstrapping all riot components
- bootstrapping a component directly into a specific part of the DOM

and riot claims its library is ultra-fast, I have yet to push it to any insane limits but I've yet to encounter any slowdowns either.

## What about SCSS?

Start by installing sass to the local directory, `npm i node-sass`. Then execute the riot compiler with the `style` specified 
{% highlight console %}
riot foo.tag --style scss
{% endhighlight %}
voila, nest your styles and use Sass functions all day!

## What else does it do?

Riot has broken their router out into a separate module, you can find it from their homepage. The core library also contains an Observable implementation to setup intra-component listening if you need that.

## Other Resources

- <a href="http://riotjs.com">Riot Homepage</a>
- <a href="https://github.com/riot/tag-loader">Webpack laoder for riot</a>
- <a href="https://github.com/tompascall/riot-jest-transformer">Jest transformer for Riot components</a>

