![img](./image.png) # functional https://fr.umio.us/the-philosophy-of-ramda

# Open Close
#### "Open for extension, closed for modification"
![](https://i.imgur.com/tpE9rSE.png)
#### It is only natural to think that given that proposition, to be able adding code as a plugin would be handy.
![](https://i.imgflip.com/2gbykl.jpg)
#### There is already a term for this idea. In the following architecture, you could avoid modifying the core  system when adding new functionalities, by adding them _as plugins_.
![](https://i.imgur.com/6GyouoS.png)
## Here is one implementation I would suggest.

![](https://i.imgur.com/2Zs4ygR.jpg)

# let's screenwrite the implementation as it was a scene for a theatrical play
![](https://i.imgur.com/m9NdWzP.png)
# #showMeTheCode
Here is the folder Core System designated for new functionalities to be placed.

![](https://i.imgur.com/4oWtwnH.png)

Here is where Core Project will import all of the files. This is called the Module Pattern, in JS.

This will avoid the common pitfall of just _having_ to add a _little_ bit of code to inform what plugin to import.

Next, we go inside _each_ plugin, and we see this:

![](https://i.imgur.com/jczueAa.png)

In short, every plugin knows how to present itself in a way that will not require further presentation by the developer. Each plugin knows how to present itself.

And after presenting themselves, providing the _unmodifiable_ Core of a function that answers the question, _should I let this transformer transform the data?_, it provides another function, the one in charge of _actually transforming the data._

# and then?
Well, in JS what you would do at conditionalActions/index.js is just make a list of exports, that exports all of the files in the module.

Then you would import it using
```js
import * as conditionalActions
from 'conditionalActions/index.js'
```

Then you would map-reduce the object `conditionalActions` onto a new constant. The input would be the not_transformed_ data, and the output would evaluate to the sum of all transformations performed if the _should_ function did in fact return `true`.

Here I am not taking into account the order of the transformations. In my case they did not overlap, but if they did the order should be provided by `'conditionalActions/index.js'.`
