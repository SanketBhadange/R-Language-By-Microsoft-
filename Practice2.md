# ================================================
# ShopSmart Order Processing System
# Module 2 - Lab 3: Control Flow and Functions
# ================================================

# Welcome to ShopSmart's order processing system development!
# In this lab, you'll implement order validation, price calculations,
# and inventory management using control flow and functions.

# ================================================
# Activity 1: Order Validation with Conditional Statements
# ================================================

###### Provided Example: ######
# Simple order validation
check_quantity <- function(quantity) {
    if (quantity <= 0) {
        return("Invalid quantity")
    }
return("Valid quantity")
}
# Try this example:
print(check_quantity(5))
print(check_quantity(0))

###### TRY IT OUT ######

# Practice 1.1: Create validate_order function
# TODO: Create a function that validates orders based on:
# - Price cannot be negative
# - Price cannot exceed 1000
# Return appropriate message for each case
validate_order <- function(price) {
    # Your code here - implement the validation logic
    #< YOUR CODE HERE >
        if (price < 0) {
        return("Error: Price cannot be negative.")
    } else if (price > 1000) {
        return("Error: Price exceeds the maximum allowable limit of $1000.")
    } else {
        return("Success: Order price is valid.")
    }
}

# Test your function
test_price <- 100
print(validate_order(test_price))
print(validate_order(-50))        
print(validate_order(1001))

# ================================================
# Activity 2: Processing Multiple Orders with Loops
# ================================================

###### Provided Example: ######
# Processing a list of orders
sample_orders <- c(100, 150, 200)
for (order in sample_orders) {
    print(paste("Processing:", order))
}

###### TRY IT OUT ######
# Practice 2.1: Create calculate_total function
# TODO: Create a function that:
# - Takes a vector of order amounts
# - Applies discounts: 10% for orders over 100, 20% for orders over 200
# - Returns total after discounts
calculate_total <- function(orders) {
    # Your code here - implement the discount logic
   # < YOUR CODE HERE >
    total_after_discount <- 0
    
    for (order_amount in orders) {
        discounted_amount <- order_amount
        
        if (order_amount > 200) {
            # 20% discount for orders over $200
            discounted_amount <- order_amount * 0.80
        } else if (order_amount > 100) {
            # 10% discount for orders over $100 (but not over $200)
            discounted_amount <- order_amount * 0.90
        }
        
        total_after_discount <- total_after_discount + discounted_amount
    }
    
    # Round the total to two decimal places for currency
    return(round(total_after_discount, 2))
}
# Test your function
test_orders <- c(50, 150, 250)
# Expected calculation: 50 + (150 * 0.90) + (250 * 0.80) = 50 + 135 + 200 = 385
print(paste("Total after discounts:", calculate_total(test_orders)))

# Practice 2.2: Process orders until limit
# TODO: Create a function that:
# - Takes a vector of order amounts
# - Adds total of orders before reaching $1000 total
# - Returns total amount
process_until_limit <- function(order_amounts) {
    # Your code here - implement the processing logic
   # < YOUR CODE HERE >
   current_total <- 0
    limit <- 1000
    
    for (amount in order_amounts) {
        # Check if adding the current amount would exceed the limit
        if (current_total + amount > limit) {
            print(paste("Stopping: Adding order of $", amount, " would exceed the $", limit, " limit.", sep=""))
            # Stop the loop
            break 
        }
        
        # Add the order amount to the running total
        current_total <- current_total + amount
    }
    
    return(round(current_total, 2))
}
test_amounts_1 <- c(300, 400, 200, 500)
# Expected: 300 + 400 + 200 = 900. Stops before 500.
print(paste("Total processed (Test 1):", process_until_limit(test_amounts_1))) 

test_amounts_2 <- c(250, 250, 250, 250, 10)
# Expected: 250 + 250 + 250 + 250 = 1000. Stops before 10.
print(paste("Total processed (Test 2):", process_until_limit(test_amounts_2)))
# ================================================
# Activity 3: Building Complex Functions
# ================================================

###### Provided Example: ######
# Function with multiple parameters
calculate_shipping <- function(distance, weight) {
    base_rate <- 10
    if (distance > 100) {
        base_rate <- base_rate + 5
    }
    if (weight > 10) {
        base_rate <- base_rate + (weight - 10) * 0.5
    }
    summary <- list(
        shipping_cost = base_rate,
        distance = distance,
        weight = weight
    )
    return(summary)
}
# Try this example:
print(calculate_shipping(50, 4)) # Should return list with cost = 10 
print(calculate_shipping(120, 30))  # Should return list with cost = 25

###### TRY IT OUT ######
# Practice 3.1: Create order_summary function
# TODO: Create a function that:
# - Accepts distance and weight as parameters
# - Calculates a base rate using the same rules
# - Returns a list with:
#     - Final shipping cost
#     - Distance and weight
#     - Message: "Shipping calculated successfully"

order_summary <- function(distance, weight) {
    # Your code here - implement the shipping summary logic
    #< YOUR CODE HERE >
    base_rate <- 10
    
    if (distance > 100) {
        base_rate <- base_rate + 5
    }
    
    if (weight > 10) {
        # Apply additional charge for weight over 10kg
        base_rate <- base_rate + (weight - 10) * 0.5
    }
    
    # Create the summary list
    summary <- list(
        shipping_cost = base_rate,
        distance = distance,
        weight = weight,
        message = "Shipping calculated successfully"
    )
    
    return(summary)
}

# Test your function
print(order_summary(80, 5))
print(order_summary(150, 25))

# ================================================
# Activity 4: Debugging Practice
# ================================================

###### Provided Example: ######
# Debug this function
process_order <- function(items, prices) {
    total <- 0
    for (i in 1:length(item)) {  # Bug: wrong variable name
        if (prices[i] <= 0) {
            continue  # Bug: 'continue' doesn't exist in R
        }
        total <- total + price[i]  # Bug: wrong variable name
    }
    return(total)
}

###### TRY IT OUT ######
# Your task: Fix the bugs in the process_order function
# TODO: Identify and fix:
# 1. Variable name mismatches
# 2. Incorrect loop control
# 3. Any other bugs you find

# Test your fixed function here
test_items <- c("Book", "Pen", "Notebook")
test_prices <- c(20, 5, 10)
