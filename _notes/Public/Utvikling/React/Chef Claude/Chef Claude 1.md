
### `src/components/Main.jsx`
```jsx
import React from "react"

export default function Main() {

    const [ingredients, setIngredients] = React.useState([]);

    const ingredientListItems = ingredients.map(ingredient => (
        <li key={ingredient}>{ingredient}</li>
    ))

    function addIngredient(formData) {
        const newIngredient = formData.get("ingredient")
        console.log(newIngredient)
        setIngredients(prevIngredients => [...prevIngredients, newIngredient])
    }



    return (
        <main>
            <form action={addIngredient} className="add-ingredient-form">
                <input
                    type="text"
                    placeholder="e.g. oregano"
                    aria-label="Add ingredient"
                    name="ingredient"
                />
                <button>Add ingredient</button>
            </form>
            <ul>
                {ingredientListItems}
            </ul>
        </main>
    )
}
```

### `src/App.css`
```css
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Inter, sans-serif;
    background-color: #FAFAF8;
}

header {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 11px;
    height: 80px;
    background-color: white;
    box-shadow: 0px 1px 3px 0px rgba(0, 0, 0, 0.10), 0px 1px 2px 0px rgba(0, 0, 0, 0.06);
}

header > img {
    width: 50px;
}

header > h1 {
    font-weight: 400;
}

main {
    padding: 30px 30px 10px;
}

.add-ingredient-form {
    display: flex;
    justify-content: center;
    gap: 12px;
    height: 38px;
}

.add-ingredient-form > input {
    border-radius: 6px;
    border: 1px solid #D1D5DB;
    padding: 9px 13px;
    box-shadow: 0px 1px 2px 0px rgba(0, 0, 0, 0.05);
    flex-grow: 1;
    min-width: 150px;
    max-width: 400px;
}

.add-ingredient-form > button {
    font-family: Inter, sans-serif;
    border-radius: 6px;
    border: none;
    background-color: #141413;
    color: #FAFAF8;
    width: 150px;
    font-size: 0.875rem;
    font-weight: 500;
}

.add-ingredient-form > button::before {
    content: "+";
    margin-right: 5px;
}

ul.ingredients-list {
    margin-bottom: 48px;
}

ul.ingredients-list > li {
    color: #475467;
    line-height: 28px;
}

.get-recipe-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-radius: 8px;
    background: #F0EFEB;
    padding: 10px 28px;
}

.get-recipe-container h3 {
    font-size: 1.125rem;
    font-weight: 500;
    line-height: 24px;
}

.get-recipe-container p {
    color: #6B7280;
    font-size: 0.875rem;
    line-height: 20px;
}

.get-recipe-container button {
    border: none;
    border-radius: 6px;
    background: #D17557;
    box-shadow: 0px 1px 2px 0px rgba(0, 0, 0, 0.05);
    color: #FAFAF8;
    padding: 9px 17px;
    font-family: Inter, sans-serif;
    font-size: 0.875rem;
    cursor: pointer;
}

.suggested-recipe-container {
    color: #475467;
    line-height: 28px;
    font-size: 1.125rem;
    font-weight: 400;
}

.suggested-recipe-container ul li, .suggested-recipe-container ol li {
    margin-bottom: 8px;
}
```

### `recipeCode.md`
```md
<section>
    <h2>Chef Claude Recommends:</h2>
    <article className="suggested-recipe-container" aria-live="polite">
        <p>Based on the ingredients you have available, I would recommend making a simple a delicious <strong>Beef Bolognese Pasta</strong>. Here is the recipe:</p>
        <h3>Beef Bolognese Pasta</h3>
        <strong>Ingredients:</strong>
        <ul>
            <li>1 lb. ground beef</li>
            <li>1 onion, diced</li>
            <li>3 cloves garlic, minced</li>
            <li>2 tablespoons tomato paste</li>
            <li>1 (28 oz) can crushed tomatoes</li>
            <li>1 cup beef broth</li>
            <li>1 teaspoon dried oregano</li>
            <li>1 teaspoon dried basil</li>
            <li>Salt and pepper to taste</li>
            <li>8 oz pasta of your choice (e.g., spaghetti, penne, or linguine)</li>
        </ul>
        <strong>Instructions:</strong>
        <ol>
            <li>Bring a large pot of salted water to a boil for the pasta.</li>
            <li>In a large skillet or Dutch oven, cook the ground beef over medium-high heat, breaking it up with a wooden spoon, until browned and cooked through, about 5-7 minutes.</li>
            <li>Add the diced onion and minced garlic to the skillet and cook for 2-3 minutes, until the onion is translucent.</li>
            <li>Stir in the tomato paste and cook for 1 minute.</li>
            <li>Add the crushed tomatoes, beef broth, oregano, and basil. Season with salt and pepper to taste.</li>
            <li>Reduce the heat to low and let the sauce simmer for 15-20 minutes, stirring occasionally, to allow the flavors to meld.</li>
            <li>While the sauce is simmering, cook the pasta according to the package instructions. Drain the pasta and return it to the pot.</li>
            <li>Add the Bolognese sauce to the cooked pasta and toss to combine.</li>
            <li>Serve hot, garnished with additional fresh basil or grated Parmesan cheese if desired.</li>
        </ol>
    </article>
</section>
```