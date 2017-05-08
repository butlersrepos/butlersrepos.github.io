---
layout: post
title:  "Such Testable Much React"
image: ''
date:   2017-05-07 20:23:00
tags:
- react
- redux
- jest
- javascript
- web
- testing
description: ''
categories:
- Javascript
---

<img src="http://weknowmemes.com/wp-content/uploads/2013/11/doge-original-meme.jpg" />

## Testing Philosophy
I'm a big fan of the testing pyramid
<img src="https://cucumber.io/images/blog/testing-pyramid.png" width="350"/>
and as such I like to have fantastic solutions on hand for each level. The most important fact to keep in mind is that as test runs go up in time to execute they will diminish in developer willingness to run geometrically more. Tests need to be fast,provide solid feedback, and be easy to write in order to reap the benefits of TDD.

## Enter Jest?
I've spoke of Jest before but this article is more about the associated libraries with Jest, the "facebook family" if you will.
<img src="http://yycjs.com/real-world-react/img/react-logo.png" height="150"/>
<img src="http://blog.js-republic.com/wp-content/uploads/2016/11/logo-redux.png" height="150"/>
<img src="http://facebook.github.io/jest/img/opengraph.png" height="150"/>

## Enter React-Redux
The real benefit for testing driving while using these libraries comes from a design philosophy adopted by some of the community, described as Presentational vs Container components. I won't rehash the design itself here because I think the [article](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0) just it perfect justice but I will talk about the enjoyment of test driving it.

## Why's it so good?
In a few words - separation. Presentational components are stupid. They're effectively a template and can often be a pure function that destructures the props from a component (the attributes of a React component) and returns a template.
{% highlight javascript %}
const MyPresentationComponent = ({ attributeThatIsString, attributeEventFunction }) => (
	<div>
		<h1>{ attributeThatIsString }<h1>
		<button onClick={ attributeEventFunction }>Click?</button>
	</div>
)
{% endhighlight %}

How hard is this component to grok even if you aren't familiar with React?

_"Alright this thing appears to receive two things and I guess it renders one and attaches the other?"_

BOOM! You got it. (I hope it was that apparent)

How hard is this component to unit test? Two unit tests can basically cover this thing, and in Jest you could whip those up in a few minutes once you get used to it and if you're [snappy](/js-workflow) in your IDE of choice.

## How do I use this in a real app though?
So now you have a really dumb component and that's really testable but now ultra useful yet. That's where a library like `react-redux` comes in.

Firstly the result of our efforts here is gonna be an entirely new component that exists alongside `MyPresentationComponent`, we're gonna make the container component. We're going to get that `attributeThatIsString` from a `redux` store. To integrate all nicely and such we're gonna use a `connect` method. The `react-redux` library uses a convenience method called `connect` that takes two functions as parameters.

- One is a function that maps the state object to any props you want to inject.
- The second is a function that maps the dispatch for the store to any functions you want to inject.

The culmination for our presentation component would be something like this...
{% highlight javascript %}
import { connect } from 'react-redux'

const mapStateToProps = state => ({ attributeThatIsString: state.myString })
const mapStateToDispatch = dispatch => {
	return {
		attributeEventFunction: () => {
			dispatch({
				type: "EVENT_FUNCTION"
			})
		}
	}
}

const MyContainerComponent = connect(mapStateToProps, mapStateToDispatch)(MyPresentationalComponent)
{% endhighlight %}

`mapStateToProps` does just as it says, it maps something on the state object to the props that will be injected. The glory of this is that you have no divorced your Presentational component from having to know 1) how to get into the state object and 2) that the store even exists. Ensuring that your Presentational component stays very dumb... and even reusable. `mapDispatchToProps` is given the `dispatch` method from your store and told how to invoke it, then hands back the reference (in our case `attributeEventFunction`) for your Presentational component to be injected with and use. Again - ensuring that it stays ignorant not only of the store as a whole but also of `dispatch`ing and how to build the appropriate action. You could even re-wrap the same Presentational component with different container components - swapping out the action created/dispatched and reuse those!

How easy do you think that last code chunk is to unit test? If you said "really damned easy" you're right.

## I'm reading this but how's it work IRL?
Checkout the repository I made around this example, along with its tests, and see how minimal it is. I hope you find it as great as I did.
- [React Redux Jest et al](https://github.com/butlersrepos/react-redux-testing-presentation-and-containers)