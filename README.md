# Burrito.JS

## Introdution
Burrito JS is a web scrapper that can be easily extended with middleware extensions called "Ingredients".
Burrito fetchs the page, checks the headers of the response and then decides what type of page it is. If it is a HTML page the data retured are the HTML, headers, title, main content, Phantom instance and meta data. If it is RSS data...

## How to use it
Ingredients are individual packages that can be used within combineIngredients fuction. To combine the ingridents the module "Async" is used. http://caolan.github.io/async/

```javascript
import { createBurrito, combineIngredients } from 'burrito';
import { socialMediaIngredient } from 'burrito-social-ingredient';
import { youtubeIngredient } from 'burrito-yt-ingredient';

// Create a burrito instance, config function for burrito, combineIngredient function contains all the Ingredients you need.
const basicScraper = createBurrito(
	config,
	combineIngredients(
		socialMediaIngredient,
		youtubeIngredient
	)
);

// Async module.
function combineIngredients(...ingredients) {
	return (data) => {
		const run = async.compose.apply(this , ingredients);
		run(data);
	}
}

basicScraper(url)


function socialMediaIngredient(data, next) {
	const { meta, mime }  = data;

	if (mime !== 'html') {
		return next();
	}

	// processing the ingrident
	...

	next(O)
}
```
