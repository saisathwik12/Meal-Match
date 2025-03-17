<!-- <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        
        input{
            width: 50%;
            padding: 10px;
            margin: 10px;
        }
        button{
            width: 20%;
            padding: 10px;
            margin: 10px;
            color: white;
            background-color: blue;
            font-size: large;
            &:focus{
                background-color: rgb(90, 90, 249);
            }
        }

    </style>
</head>
<body>
    <input id="ingredients" type="text" placeholder="Enter Ingredients"><br>
    <button id="search">Search</button>
    <h1 id="h1"></h1>
    <div id="cards">
        

    </div>

    <script>
        const input = document.getElementById("ingredients");
        const ser = document.getElementById("search")
        const h1 = document.getElementById('h1')
        const cards = document.getElementById('cards')
        console.dir(cards)
        ser.addEventListener("click",(e) => {
            let inp = input.value.toLowerCase().split(',');
            

            fetch('https://dummyjson.com/recipes?limit=0')
            .then(res => res.json())
            .then(res =>{ 
                recipe = res.recipes; 
                isFound = false;
                for(r of recipe){

                    for(l =0;l<r.ingredients.length;l++){
                        r.ingredients[l] = r.ingredients[l].toLowerCase()
                    }
                    
                    if(inp.every(val => r.ingredients.includes(val))){
                        // h1.textContent = r
                        const card = document.createElement('div')
                        card.setAttribute('id','card')

                        const img = document.createElement('img')
                        const name = document.createElement('h2')
                        const rating = document.createElement('span')
                        const review = document.createElement('span')
                        const cuisine = document.createElement('p')
                        const difficulty = document.createElement('p')
                        const preptime = document.createElement('p')
                        rating.textContent = 'Rating : ' + r.rating
                        review.textContent = 'Review Count : ' + r.reviewCount
                        cuisine.textContent = 'Cuisine : ' + r.cuisine
                        difficulty.textContent = 'Difficulty : ' + r.difficulty
                        preptime.textContent = 'Prepare Time Minutes : ' + r.prepTimeMinutes

                        name.textContent = r.name
                        img.setAttribute('src',r.image)
                        img.setAttribute('width','300px')
                        card.addEventListener('click',(e2) => {
                            location.href ='recipedetails.html'
                            
                        })
                    


                        isFound = true
                        cards.appendChild(card)
                        card.appendChild(img)
                        card.appendChild(name)
                        card.appendChild(cuisine)
                        card.appendChild(difficulty)
                        card.appendChild(preptime)
                        card.appendChild(rating)
                        card.appendChild(review)
                        card.style.border = '1px solid black'
                        card.style.padding = '50px'
                        card.style.margin = '10px'
                        card.style.cursor = 'pointer'

                        rating.style.marginRight = '50px'
                    }

                    
                }
                if(isFound){

                }
                else{
                    h1.textContent = 'Not found suitable Recipes'
                }
        
            })

            input.value = ""

        })

        cards.style.display = 'flex'
        cards.style.justifyContent = 'space-around'
        cards.style.flexWrap = 'wrap'


        
        
    </script>
</body>
</html> -->



<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Meal Match</title>
  <link rel="stylesheet" href="mealmatch.css">
</head>

<body>
  <header>
    <h1>Meal Match</h1>
    <p>Find recipes using ingredients you already have!</p>
  </header>

  <main>
    <section id="search">
      <input type="text" id="ingredient-input" placeholder="Enter ingredients (e.g., chicken, tomato)">
      <button id="search-button">Find Recipes</button>
    </section>

    <section id="meal-results" class="meal-grid">
      <!-- Meal cards will be dynamically injected here -->
    </section>
  </main>

  <template id="meal-card-template">
    <div class="meal-card">
      <img class="meal-image" alt="Meal Image">
      <h3 class="meal-name"></h3>
      <a class="meal-video-link" target="_blank">Watch Tutorial</a>
    </div>
  </template>

  <script>
    // JavaScript for Meal Match
    const searchButton = document.getElementById('search-button');
    const ingredientInput = document.getElementById('ingredient-input');
    const mealResults = document.getElementById('meal-results');
    const mealCardTemplate = document.getElementById('meal-card-template');

    searchButton.addEventListener('click', () => {
      const ingredients = ingredientInput.value.trim();
      if (ingredients) {
        fetchMeals(ingredients);
      } else {
        alert('Please enter at least one ingredient.');
      }
    });

    async function fetchMeals(ingredients) {
      const apiUrl = `https://www.themealdb.com/api/json/v1/1/filter.php?i=${ingredients}`;

      try {
        const response = await fetch(apiUrl);
        const data = await response.json();
        displayMeals(data.meals);
      } catch (error) {
        console.error('Error fetching meals:', error);
        mealResults.innerHTML = '<p>Failed to load meals. Please try again later.</p>';
      }
    }

    function displayMeals(meals) {
      mealResults.innerHTML = '';

      if (meals && meals.length > 0) {
        meals.forEach(meal => {
          const mealCard = mealCardTemplate.content.cloneNode(true);
          mealCard.querySelector('.meal-image').src = meal.strMealThumb;
          mealCard.querySelector('.meal-name').textContent = meal.strMeal;
          mealCard.querySelector('.meal-video-link').href = `https://www.youtube.com/results?search_query=${meal.strMeal}`;
          mealResults.appendChild(mealCard);
        });
      } else {
        mealResults.innerHTML = '<p>No meals found. Try different ingredients.</p>';
      }
    }
  </script>
</body>

</html>

body {
    font-family: Georgia, serif;
    margin: 0;
    padding: 0;
    /* background-image: url("4287688.jpg"); */
  }

  header {
    text-align: end;
    background-image: url("food_bg1.jpg");
    background-size: cover;
    background-repeat: no-repeat;
    color: #463f3a;
    text-shadow: 5px 2px 10px #33333335;
    height: 300px;
    padding-top: 100px;
    padding-right: 50px;
  }

  header h1 {
    margin: 0;
    animation: rise 3s ease;
    font-size: 100px;


  }

  @keyframes rise {
    from {
      translate: 0px 100px;

    }

    to {
      translate: 0 0;

    }
  }

  header p {
    font-family: Brush Script MT, cursive;
    animation: rise 3s ease;
    font-size: 40px;

  }


  #search {
    text-align: center;
    margin: 20px 0;
  }

  #ingredient-input {
    width: 80%;
    /* max-width: 400px; */
    font-size: larger;
    padding: 15px 10px;
    margin-right: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  #search-button {
    padding: 15px 30px;
    background-color: #e0dbd8;
    color: black;
    border: 1px solid #fff1e6;
    border-radius: 5px;
    cursor: pointer;
    font-size: larger;
  }

  #search-button:hover {
    background-color: #463f3a;
    color: white;
  }

  .meal-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
    padding: 20px;
  }

  .meal-card {
    background-color: whitesmoke;
    border: 1px solid #ddd;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    text-align: center;
    padding: 20px;
  }

  .meal-image {
    width: 100%;
    height: auto;
  }

  .meal-name {
    margin: 15px 0;
    font-size: 1.2rem;
    color: rgb(38, 38, 38);
  }

  .meal-video-link {
    display: inline-block;
    margin: 10px 0 20px;
    padding: 8px 15px;
    background-color: #e0dbd8;
    color: #463f3a;
    text-decoration: none;
    border: 1px solid #463f3a;
    border-radius: 5px;
  }

  .meal-video-link:hover {
    background-color: #463f3a;
    color: white;
  }

  @media (max-width: 768px) {
    header {
      background-color: #e6e5e5;
      background-image: url();
      color: #463f3a;
      text-shadow: 5px 2px 10px #33333335;
      min-height: 200px;
      padding-top: 100px;
      padding-right: 0px;
    }

    header h1 {
      text-align: center;
      margin: 0;
      animation: rise 3s ease;
      font-size: 4em;
      padding: 0;
    }

    header p {
      text-align: center;
      font-family: Brush Script MT, cursive;
      animation: rise 3s ease;
      font-size: 2em;
    }

    @keyframes rise {
      from {
        translate: 0px 50px;

      }

      to {
        translate: 0 0;
      }


    }

    #search-button {
      margin-top: 10px;
    }
  }
<!-- 
  index2.html -->

  <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Meal Match</title>
  <link rel="stylesheet" href="styles.css">
  <style>
    /* CSS for Meal Match */
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f4f4f4;
    }

    header {
      text-align: center;
      background-color: #ff6347;
      color: white;
      padding: 1rem 0;
    }

    #search {
      text-align: center;
      margin: 20px 0;
    }

    #ingredient-input {
      width: 80%;
      max-width: 400px;
      padding: 10px;
      margin-right: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    #search-button {
      padding: 10px 20px;
      background-color: #ff6347;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    #search-button:hover {
      background-color: #e5533f;
    }

    .meal-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      gap: 20px;
      padding: 20px;
    }

    .meal-card {
      background-color: white;
      border: 1px solid #ddd;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      text-align: center;
    }

    .meal-image {
      width: 100%;
      height: auto;
    }

    .meal-name {
      margin: 15px 0;
      font-size: 1.2rem;
      color: #333;
    }

    .meal-video-link {
      display: inline-block;
      margin: 10px 0 20px;
      padding: 8px 15px;
      background-color: #ff6347;
      color: white;
      text-decoration: none;
      border-radius: 5px;
    }

    .meal-video-link:hover {
      background-color: #e5533f;
    }
  </style>
</head>
<body>
  <header>
    <h1>Meal Match</h1>
    <p>Find recipes using ingredients you already have!</p>
  </header>
  
  <main>
    <section id="search">
      <input type="text" id="ingredient-input" placeholder="Enter ingredients (e.g., chicken, tomato)">
      <button id="search-button">Find Recipes</button>
    </section>

    <section id="meal-results" class="meal-grid">
      <!-- Meal cards will be dynamically injected here -->
    </section>
  </main>

  <template id="meal-card-template">
    <div class="meal-card">
      <img class="meal-image" alt="Meal Image">
      <h3 class="meal-name"></h3>
      <a class="meal-video-link" target="_blank">Watch Tutorial</a>
    </div>
  </template>

  <script>
    // JavaScript for Meal Match
    const searchButton = document.getElementById('search-button');
    const ingredientInput = document.getElementById('ingredient-input');
    const mealResults = document.getElementById('meal-results');
    const mealCardTemplate = document.getElementById('meal-card-template');

    searchButton.addEventListener('click', () => {
      const ingredients = ingredientInput.value.trim();
      if (ingredients) {
        fetchMeals(ingredients);
      } else {
        alert('Please enter at least one ingredient.');
      }
    });

    async function fetchMeals(ingredients) {
      const apiUrl = `https://www.themealdb.com/api/json/v1/1/filter.php?i=${ingredients}`;

      try {
        const response = await fetch(apiUrl);
        const data = await response.json();
        displayMeals(data.meals);
      } catch (error) {
        console.error('Error fetching meals:', error);
        mealResults.innerHTML = '<p>Failed to load meals. Please try again later.</p>';
      }
    }

    function displayMeals(meals) {
      mealResults.innerHTML = '';

      if (meals && meals.length > 0) {
        meals.forEach(meal => {
          const mealCard = mealCardTemplate.content.cloneNode(true);
          mealCard.querySelector('.meal-image').src = meal.strMealThumb;
          mealCard.querySelector('.meal-name').textContent = meal.strMeal;
          mealCard.querySelector('.meal-video-link').href = `https://www.youtube.com/results?search_query=${meal.strMeal}`;
          mealResults.appendChild(mealCard);
        });
      } else {
        mealResults.innerHTML = '<p>No meals found. Try different ingredients.</p>';
      }
    }
  </script>
</body>
</html>
