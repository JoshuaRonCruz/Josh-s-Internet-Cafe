<h1>Josh's Internet Cafe</h1>

<script>
	let drinks = [
		{id: 1, name: "Water", image: "https://www.clipartkey.com/mpngs/m/79-798309_water-bottle-bottle-water-maza-turkish-mediterranean-unbranded.png", price: 1.00, quantity: 1, description1: "Regular, good old fashion, crystal clear, and refreshing water.", description2: "No addons for an already perfect beverage."},
		{id: 2, name: "Coffee", image: "https://www.healio.com/~/media/slack-news/stock-images/fm_im/c/coffee_shutterstock.jpg", price: 3.00, quantity: 1, description1: "Standard dark roast.", description2: "Brewed for you, so you don't have to at home."},
		{id: 3, name: "Latte", image: "https://static.vecteezy.com/system/resources/previews/001/740/365/large_2x/close-up-of-a-latte-on-a-white-background-free-photo.jpg", price: 4.75, quantity: 1, description1: "Espresso with steamed milk.", description2: ""},
		{id: 4, name: "Mocha", image: "https://previews.123rf.com/images/punsayaporn/punsayaporn1307/punsayaporn130700121/20841305-cup-of-hot-cafe-mocha-isolated-on-white-background.jpg", price: 5.20, quantity: 1, description1: "Espresso with steamed milk and chocolate.", description2:""},
		{id: 5, name: "Cappuccino", image: "https://previews.123rf.com/images/fanfo/fanfo1010/fanfo101000011/7969657-cappuccino-cup-coffee-isolated-on-a-white-background-.jpg", price: 4.60, quantity: 1, description1: "Two Espresso shots with steamed milk foam.", description2:""},
		{id: 6, name: "Caramel Macchiato", image: "https://previews.123rf.com/images/belchonock/belchonock1903/belchonock190302477/118089179-glass-cup-of-tasty-caramel-macchiato-on-white-background.jpg", price: 5.50, quantity: 1, description1: "Espresso with steamed milk, vanilla, and caramel sauce.", description2:""},
		{id: 7, name: "Espresso", image: "https://media.istockphoto.com/photos/coffee-espresso-in-white-background-picture-id545335342?k=6&m=545335342&s=170667a&w=0&h=YQU0SvpObLGQNAyz720FH1RbYfgqYui1kbpD1_1eqRo=", price: 2.50, quantity: 1, description1: "Standard shot, except with caffine instead of alcohol.", description2:""},
		{id: 8, name: "Americano", image: "https://image.freepik.com/free-photo/white-cup-black-coffee-isolated-white-background_252965-15.jpg", price: 4.40, quantity: 1, description1: "Espresso with hot water.", description2:""}
	]

	let addons = [
		{id: 9, name: "Extra Shot", price: 0.50, quantity: 1},
		{id: 10, name: "Decaf", price: 0, quantity: 1},
		{id: 11, name: "Extra Shot", price: 0.50, quantity: 1},
		{id: 12, name: "Whipped Cream", price: 0.25, quantity: 1},
		{id: 13, name: "Soy Milk", price: 0.35, quantity: 1}
	]

	let cart = [];
	let cart2 = [];

	const addToCart = (drink) => {
		for(let item of cart){
			if(item.id === drink.id){
				drink.quantity += 1
				cart = cart;
				return
			}
		}
		cart = [...cart, drink]
	}

	const addonToCart = (addon) => {
		for(let item2 of cart2){
			if(item2.id === addon.id){
				addon.quantity += 1
				cart2 = cart2;
				return
			}
		}
		cart2 = [...cart2, addon]
	}

	const plusQuantity = (drink) => {
		for(let item of cart) {
			if(item.id === drink.id) {
				drink.quantity += 1
				cart = cart;
				return
			}
		}
		cart = [...cart, drink]
	}

	const plusQuantityAddon = (addon) => {
		for(let item2 of cart2) {
			if(item2.id === drink.id) {
				drink.quantity += 1
				cart2 = cart2;
				return
			}
		cart2 = [...cart, addon]
		}
	}
	const minusQuantity = (drink) => {
		for(let item of cart) {
			if(item.id === drink.id) {
				drink.quantity -= 1
				cart = cart;
				return
			}
		cart = [...cart, drink]
		}
	}

	const minusQuantityAddon = (addon) => {
		for(let item2 of cart2) {
			if(item2.id === drink.id) {
				drink.quantity += 1
				cart2 = cart2;
				return
			}
		cart2 = [...cart2, addon]
		}
	}

	total1 = cart.reduce((sum, item) => sum + item.price * item.quantity, 0)
	total2 = cart2.reduce((sum, item2) => sum + item2.price * item2.quantity, 0)
$: total = total1 + total2
</script>

<div class ="drink-list">
	{#each drinks as drink}
		<div>
			<div class="img" style="background-image: url({drink.image})"></div>
			<img src={drink.image} alt={drink.name}/>
			<h2>{drink.name}</h2>
			<h4>{drink.description1}</h4>
			<h4>{drink.description2}</h4>
			<p>${drink.price}</p>
			<button on:click={() => addToCart(drink)}>Add Drink to Cart</button>
			<div class="addon-list">
				{#each addons as addon}
				<h2>{addon.name}</h2>
				<p>${addon.price}</p>
				<button on: click={() => addonToCart(addon)}>Add Addon to Cart</button>
				{/each}
			</div>
		</div>
	{/each}
</div>

<div class="cart-list">
	{#each cart as drink}
		{#if drink.quantity > 0}
		<div class="cart-item-drink">
			<img id= "cartdrink" src={drink.image} alt={drink.name}/>
			<h6>{drink.name}</h6>
			<div>{drink.quantity}
				<button on:click={() => minusQuantity(drink)}>-</button>
				<button on:click={() => plusQuantity(drink)}>+</button>
			</div>
			<p>${drink.price * drink.quantity}</p>
		</div>
		{/if}
	{/each}
	{#each cart as addon}
		{#if addon.quantity > 0}
		<div class="cart-item-addon">
			<h6>{addon.name}</h6>
			<div>{addon.quantity}
				<button on:click={() => minusQuantityAddon(addon)}>-</button>
				<button on:click={() => plusQuantityAddon(addon)}>+</button>
			</div>
			<p>${addon.price * addon.quantity}</p>
		</div>
		{/if}
	{/each}
	<div class= "total">
		<h4>Total: $ {total}</h4>
		</div>
</div>

<style>
	img {
		width: 300px;
		height: 300px;
		display: inline-block;
	}

	img[id = "cartdrink"] {
		width: 50px;
		height: 50px;
		display: inline-block;
	}

	.addon-list {
		display: grid;
		grid-template-columns: (5, 5fr)
		
	}

	.drink-list {
		display: grid;
		grid-template:
		"item item item"
		"item item item"
		"item item item"
		"item item item"
		minmax(40px, 40px)
	}

	.drink-list{
		display: grid;
		grid-template:
		"item item item"
		"item item item"
		"item item item"
		"item item item"
		minmax(40px, 40px)
	}

	h1{
		text-align: center;
		color: grey;
		border-bottom-width: 1px;
		border-bottom-color: black;
		border-bottom-style: solid;
		grid-area: heading;
		font-weight: normal;
	}

	.cart-list {
		border: 2px solid;
		padding: 10px;
	}
	
	.cart-item-addon {
		grid-template-columns: repeat(9, 1fr);
	}

	.cart-item-drink {
		grid-template-columns: repeat(9, 1fr);
	}
</style>



