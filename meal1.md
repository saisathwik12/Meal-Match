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