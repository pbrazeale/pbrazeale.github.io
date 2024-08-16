[The 3 Laws of Writing Readable Code](https://www.youtube.com/watch?v=-AzSRHiV9Cc)

## Law 1: Avoid Deeply Nested Logic
- logic is harder to understand

{% highlight Go linenos %}
func main(){
	if !isMaintenancePeriod {
		if isAuthenticatedUser {
			if isAuthorizedUser {
				for _. product := range cart {
					// Core Logic
					switch product.Type() {
						case "alcohol":
							total += alcoholTax
						case "electronics":
							total += electronicsTax
						default:
							total += generalTax
					}
				}
			}else {
				log.Fatalf("user not authorized")
			}
		}else {
			log.Fatalf("invalid user credentials")
		}
	}else {
		log.Fatalf("feature unabailable")
	}
}
{% endhighlight %}
### Solutions
#### Inversion
*Catch the error conditions earlier and only allow the core logic code to execute if all else is good*
{% highlight Go linenos %}
func main(){
	if isMaintenancePeriod {
		log.Fatalf("feature unabailable")
	}
	
	if !isAuthenticatedUser {
		log.Fatalf("invalid user credentials")
	}
	
	if !isAuthorizedUser {
		log.Fatalf("user not authorized")
	}
	
	for _. product := range cart {
		// Core Logic
		switch product.Type() {
			case "alcohol":
				total += alcoholTax
			case "electronics":
				total += electronicsTax
			default:
				total += generalTax
		}
	}
}
{% endhighlight %}

#### Merge Related If Statements
{% highlight Go linenos %}
func main(){
	if isMaintenancePeriod {
		log.Fatalf("feature unabailable")
	}

	// Easier to read, but at the cost of only one log message. Weigh the tradeoff.
	if !isAuthenticatedUser || !isAuthorizedUser {
		log.Fatalf("user not authorized")
	}
	
	for _. product := range cart {
		// Core Logic
		switch product.Type() {
			case "alcohol":
				total += alcoholTax
			case "electronics":
				total += electronicsTax
			default:
				total += generalTax
		}
	}
}
{% endhighlight %}

#### Extraction

{% highlight Go linenos %}
func main(){
	if isMaintenancePeriod {
		log.Fatalf("feature unabailable")
	}

	if !isValidUser() {
		log.Fatalf("user not authorized")
	}
	
	for _. product := range cart {
		calculateTaxes(product)
	}
}

//seperating out the code makes it easier to understnad.
func isValidUser() bool {
	return isAuthenticatedUser && isAuthorizedUser
}

func calculateTaxes(product product) {
	// Core Logic
	switch product.Type() {
		case "alcohol":
			total += alcoholTax
		case "electronics":
			total += electronicsTax
		default:
			total += generalTax
	}
}
{% endhighlight %}


## Law 2: Avoid Duplication

{% highlight Go linenos %}
func getUser(w http.REsponseWriter, r *http.Request) {
	userID := r.URL.Path[len("/user/"):]

	cacheMux.Lock()
	user, found := cache[userID]
	cacheMux.Unlock()

	if !found {
		query := "SELECT user_name, email FROM useres WHERE user_id = ?"
		stmt, _ := db.Prepare(query)

		var u User
		_ = stmt.QueryRow(userID).Scan(&u.Username, &u.Email)

		cacheMux.Lock()
		cache[userID] = u
		cacheMux.Unlock()
		
		user = u
	}
	
	w.Header().Set("Content-Type", "application/json")
	json.NewEncoder(w).Encode(user)
}

func getUsers(w http.REsponseWriter, r *http.Request){
	var requestBody RequestBody
	json.NewDecoder(r.Body).Decode(&requestBody)
	userIDs := requestBody.UserIDs
	var users []User
	
	for _, userID := range userIDs {
		cacheMux.Lock()
		user, found := cache[userID]
		cacheMux.Unlock()
		
		if !found {
			query := "SELECT user_name, email FROM useres WHERE user_id = ?"
			stmt, _ := db.Prepare(query)
	
			var u User
			_ = stmt.QueryRow(userID).Scan(&u.Username, &u.Email)
	
			cacheMux.Lock()
			cache[userID] = u
			cacheMux.Unlock()
			
			user = u
		}
		
		users = append(users, user)
	}
	
	writeResponse(w, user)
}
{% endhighlight %}

Create a function for both parent functions to use.
{% highlight Go linenos %}
func getUser(w http.REsponseWriter, r *http.Request) {
	userID := r.URL.Path[len("/user/"):]
	user := getSingleUser(userIDs)
		
	w.Header().Set("Content-Type", "application/json")
	json.NewEncoder(w).Encode(user)
}

func getUsers(w http.REsponseWriter, r *http.Request){
	var requestBody RequestBody
	json.NewDecoder(r.Body).Decode(&requestBody)
	userIDs := requestBody.UserIDs
	var users []User
	
	for _, userID := range userIDs {
		
		user := getSingleUser(userIDs)
		users = append(users, user)
	}
	
	writeResponse(w, user)
}

// Function to replace gettign User
func getSingleUser(userID string) User {
	cacheMux.Lock()
	user, found := cache[userID]
	cacheMux.Unlock()
	
	if !found {
		query := "SELECT user_name, email FROM useres WHERE user_id = ?"
		stmt, _ := db.Prepare(query)

		var u User
		_ = stmt.QueryRow(userID).Scan(&u.Username, &u.Email)

		cacheMux.Lock()
		cache[userID] = u
		cacheMux.Unlock()
		
		user = u
	}
	
	return user
}

//Function to replace Writing Response
func writeResponse(w http.ResponseWriter, response interface{}) {
	w.Header().Set("Content-Type", "application/json")
	json.NewEncoder(w).Encode(users)
}
{% endhighlight %}

### Takeaways
- Code is easier to read through
- easier to maintain as it only needs to be touched in place
- modular and able to be moved around if needed

## Law 3: Don't User Cryptic Naming
{% highlight Go linenos %}
type P struct {
	N string
	P float64
}

func main() {
	ps := []P{
		{"Apple", 0.50},
		{"Banana", 0.25},
		{"Orange", 0.75},
		{"Pear", 0.30},
	}
	
	t := 0.08
	var tc float64 = 0
	
	for _, P := range ps {
		tc += p.P + (p.P * t)
	}
	
	sc := tc / flaot64(len(ps))
	
	fmt.Println(tc)
	fmt.Println(ac)
}
{% endhighlight %}
**Pick any naming convention and use it!**

{% highlight Go linenos %}
type Product struct {
	Name string
	Price float64
}

func main() {
	proudcuts := []Product{
		{"Apple", 0.50},
		{"Banana", 0.25},
		{"Orange", 0.75},
		{"Pear", 0.30},
	}
	
	tax := 0.08
	var totalCost float64 = 0
	
	for _, product := range products {
		totalCost += product.Price + (product.Price * tax)
	}
	
	averageCost := totalCost / flaot64(len(ps))
	
	fmt.Println(totalCost)
	fmt.Println(averageCost)
}
{% endhighlight %}

