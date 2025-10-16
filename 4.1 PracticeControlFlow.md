```R
# ================================================
# RetailTech Solutions - Basic Order Processing
# Module 2 - Graded Lab
# ================================================

# This starter code provides the structure for your
# order processing functions. Complete each section
# marked with "YOUR CODE HERE"

# ================================================
# Activity 1: Check Order Amount
# ================================================

### GRADED CHALLENGE 1 ###
# Create the check_order_amount function
# Parameters: order_amount (numeric)
# Returns: Character string indicating order level
check_order_amount <- function(order_amount) {
    # YOUR CODE HERE
    # Remember to check:
    # - Negative or zero amounts, return "Invalid"
    # - If order is under 50 return "Low"
    # - If order is between 50-100 return "Regular"
    # - Else return "High"
     if (order_amount <= 0) {
        return("Invalid")
    } else if (order_amount < 50) {
        return("Low")
    } else if (order_amount >= 50 && order_amount <= 100) {
        return("Regular")
    } else {
        return("High")
    }
}

# Test cases provided
test_amount <- -1
print(check_order_amount(test_amount))
test_amount <- 20
print(check_order_amount(test_amount))
test_amount <- 120
print(check_order_amount(test_amount))

# ================================================
# Activity 2: Calculate Order Total 
# ================================================

### GRADED CHALLENGE 2 ###
# Create the calculate_total function
# Parameters: 
# - amount (numeric)
# - is_member (logical)
calculate_total <- function(amount, is_member) {
    # YOUR CODE HERE
    # Remember:
    # - Check for valid amount
    # - Apply 10% member discount if applicable
    # - Do not apply a 10% member discount if is_member is FALSE 
    # - Return final total
        if (amount <= 0) {
        return("Error: Invalid amount")
    }
    if (is_member) {
        return(amount * 0.90)
    } else {
        return(amount)
    }
}

# Test cases provided
test_amount <- 100
test_member <- TRUE
print(calculate_total(test_amount, test_member)) # returns 90

test_amount <- 100
test_member <- FALSE
print(calculate_total(test_amount, test_member)) # returns 100


# ================================================
# Activity 3: Process Multiple Orders 
# ================================================

### GRADED CHALLENGE 3 ###
# Create the process_orders function
# Parameters: order_amounts (numeric vector)
# Returns: List with count of 'large orders' and 'average'
process_orders <- function(order_amounts) {
    # YOUR CODE HERE
    # Remember to:
    # - Count orders above 100 and store in 'large_orders'
    # - Calculate the average amount of all orders submitted to process_orders and store in 'average'
    # - Return both 'large_orders' and 'average' in a list
    if (any(is.na(order_amounts))) {
        return("Error: Contains NA values")
    }
    
    # Check for non-numeric input
    if (!is.numeric(order_amounts)) {
        return("Error: Non-numeric input")
    }
    
    # Filter out orders that are not numeric
    clean_amounts <- as.numeric(order_amounts[!is.na(order_amounts)])
    
    # Count orders over 100
    large_orders <- sum(clean_amounts > 100)
    
    # Calculate the average amount
    average <- mean(clean_amounts)
    
    # Return results in a list
    return(list(large_orders = large_orders, average = average))
}

# Test cases provided
test_orders <- c(75, 120, 45, 200, 85)
process_orders(test_orders)

# ================================================
# Activity 4: Basic Error Checking (24 points)
# ================================================

### GRADED CHALLENGE 4 ###
# Modify process_orders to include error checking
# Add checks for:
# - NA values
# - Non-numeric input
# - Return error messages for the following:
# - For NA Values inputs, return the exact error: "Error: Contains NA values"\
# - For Non-numeric inputs, return the exact error: "Error: Non-numeric input"

# YOUR CODE HERE

# Test cases for error checking
test_na <- c(100, NA, 75)
test_invalid <- c(100, "invalid", 75)

test_valid <- c(120, 80, 50, 200)
test_amounts <- c(75, 120, 45, 200, 85)
test_member <- TRUE
print(process_orders(test_na))# Expected: "Error: Contains NA values"
print(process_orders(test_invalid))# Expected: "Error: Non-numeric input"


# ================================================
# Testing Section
# ================================================
# Use these commands to test your functions

# Activity 1 Test
print("Testing check_order_amount:")
for(amount in test_amounts) {
    print(paste("Amount:", amount, "Result:", check_order_amount(amount)))
}

# Activity 2 Test
print("Testing calculate_total:")
print(paste("Regular total:", calculate_total(test_amount, FALSE)))
print(paste("Member total:", calculate_total(test_amount, TRUE)))

# Activity 3 Test
print("Testing process_orders:")
result <- process_orders(test_orders)
print(result)

# Activity 4 Test
print("Testing error handling:")
tryCatch({
    process_orders(test_na)
}, error = function(e) {
    print(paste("Error handled:", e$message))
})
```
