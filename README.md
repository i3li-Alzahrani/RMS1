# Resutaurant Management System (RMS)
## Execute

website :- https://projectworlds.in

Youtube :- https://youtu.be/6iB4-3c0cxc
Double click RMS_GUI.jar
## Login
You can use test data for the first time. You can add new staff when you log in as manager.
### Manager
- ID:1000 Password:Java
- ID:5555 Password:kazukazu

### Staff
* ID:1111 Password:password
* ID:3333 Password:david  
(Modifing the data file directoly may make problem.)  

## Show menu
You can see all menu items by clicking ALL button, and items in particular categories by clicking Drink, Alcohol, Main, or Dessert button.  
## Taking order
### Create new order
1. Click "Show menu" button on the left
2. Click "New" button to create new order
![](readme_images/order.jpg)
3. Select adding items by clicking from the menu list on the right side.
4. Enter quantity and click "Add" button on the left side.(If quantity is emputy, one item will be added)
5. You can delete ordered item from the order detail by clicking "Delete" button  

### Edit order
1. Click "Show menu" button on the left
2. Select the order from the order list to edit
3. Click "Edit" button
4. You can add, delete ordered items

### Close or Cancel order
1. Select the order from the order list
2. Click "Close" button or "Cancel" button
3. The order closed or canceled can not edit

## Manage Employees (Manager only)
### Add new staff
1. Click "Manage Employees" Button on the left
2. Click "New" button
3. Fill in all information and click OK

###Edit staff
1. Click "Manage Employees" Button on the left
2. Select a staff from the employees list
3. Click "Edit" button
4. Fill in all information and click OK

###Delete staff
1. Click "Manage Employees" Button on the left
2. Select a staff from the employees list
3. Click "Delete" button

##Manage Menu Items (Manager only)
###Add new item
1. Click "Manage menu items" Button on the left
2. Click "Add new menu item" button
3. Fill in all information and click OK

###Edit menu item
1. Click "Manage menu items" Button on the left
2. Select a menu item from the menu list
3. Click "Edit menu item" button
4. Fill in all information and click OK

###Delete menu item
1. Click "Manage menu items" Button on the left
2. Select a menu item from the menu list
3. Click "Delete menu item" button

##About payments
* When you log in, the system automaticaly set start working time.
* Clock out button will set finish working time of the person currently logged in.
* Manager can make staff clocked out via manage employees, by selecting staff and clicking Clock out button.
* You can see a payment details for a day by clicking "Show payment" button on the left





### Functions
code example in Delete an item in Order.
This project includes functions for managing orders, including deleting items from an order.

## How to Use the Function

To remove an item from an order, you can use the following method:

```java
// Delete item from order
public boolean deleteOrderItem(int orderID, int index) {
    Order rOrder = findOrderByID(orderID); // Find order by ID  
    if (rOrder == null) return false; // Check if order exists
    return rOrder.deleteItem(index); // Delete item from order
// Ahmed sultan
}
```

## API Documentation for `deleteOrderItem`

### Overview
The `deleteOrderItem` method is part of the Order Management System and allows users to remove an item from a specific order based on the order ID and the index of the item.

### Endpoint
- **Method**: DELETE
- **URL**: `/orders/{orderID}/items/{index}`

### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `orderID` | int  | The unique identifier of the order. |
| `index`   | int  | The index of the item in the order to be deleted. |

### Request Example
To delete an item from an order, you would make a request like this:

This request attempts to delete the item at index 0 from the order with ID 123.

### Response

#### Success Response
- **Code**: 200 OK
- **Content**:
```json
{
    "success": true,
    "message": "Item deleted successfully."
}
```
#### Erorr Response
- **Code**: 404 Not Found
- **Content**:
```json
{
    "success": false,
    "message": "Order not found."
}
```

# Menu Item Initialization API

## Overview
The `init` method is responsible for initializing a menu item in the application. It sets up the fields for a new menu item when the `menuItemID` is `0`. This method ensures that all relevant fields are cleared and set to default values.

## Method Signature
```java

public void init(int menuItemID) {
// ali
    // Check if the menuItemID is 0, indicating a new menu item creation
    if (menuItemID == 0) {
        // Reset the menu ID to an empty string
        setMenuID("");
        
        // Enable editing for the menu item ID textbox
        tbMenuItemID.setEditable(true);
        
        // Clear the item name field
        setItemName("");
        
        // Clear the price field
        setPrice("");
        
        // Set the default type of the menu item to "Main"
        setType("Main");
        
        // Indicate that this is not an update operation
        isUpdate = false;
        
        // Exit the method as the initialization is complete
        return;
    }
    // Additional logic for handling existing menu items would go here
}
```

### Endpoint
- **Method**: ADD
- **POST**: /menu/items/init

### Description
This endpoint initializes the parameters for a menu item. If the menuItemID is 0, it sets up a new menu item. Otherwise, it prepares an existing menu item for editing.

### Parameters

- *Query Parameters:*
  - menuItemID (int): The unique identifier for the menu item. A value of 0 indicates the creation of a new menu item.

### Request Example
```http
POST /menu/items/init?menuItemID=0

  "message": "Menu item initialized successfully."
  "menuItem": {
    "menuID": "",
    "itemName": "",
    "price": "",
    "type": "Main",
    "isUpdate": false
  }
```
Here's the API documentation for the userLogin method:

### Method: userLogin
The userLogin method handles the login process for both managers and employees. It displays the login view, prompts for user input to determine the login type, and proceeds to validate credentials based on the selection.

#### Parameters:
- This method does not take any parameters.

#### Process:
1. *Display Login View*:
   - Calls cView.loginView() to display the login interface to the user.
   - Prompts the user with: "Login as manager? (Y/N)" to determine whether they want to log in as a manager or an employee.

2. *Handle User Input*:
   - Receives user input through cView.userInput().
   - If the user enters "Q", the method sets the scene to SCENE_MAIN_MENU and exits, returning the user to the main menu.
   - If the user input is not "Y" or "N", it prompts them again until a valid input is provided.

3. *Login Verification*:
   - If the user chooses "Y", the method calls loginCheck(true) to verify manager login credentials.
   - If the user chooses "N", it calls loginCheck(false) to verify employee login credentials.

4. *Return to Main Menu*:
   - After the login check (successful or not), the method sets the scene to SCENE_MAIN_MENU, returning the user to the main menu.

#### Returns:
- This method does not return any value.

#### Example:
When a user attempts to log in, they are prompted to select whether they are logging in as a manager or employee. Based on their selection, the appropriate login verification is executed. If the user enters "Q" at any time, they are returned to the main menu without logging in.

``` java
private void userLogin() {
// ahmed abad
    // Display the login interface 
    cView.loginView();
    // Ask the user if they want to login as a manager
    printMessageToView("Login as manager? (Y/N)");

    // Get user input for login type
    String key = cView.userInput();
    // If the user enters "Q", return to the main menu
    if (key.equalsIgnoreCase("Q")) {
        scene = SCENE_MAIN_MENU;
        return;
    }

    // Loop until the user enters a valid response ("Y" or "N")
    while (!key.equalsIgnoreCase("Y") && !key.equalsIgnoreCase("N")) {
        printMessageToView("Please enter 'Y' or 'N'\nLogin as manager? (Y/N)");
        key = cView.userInput();
    }

    // If the user chooses "Y", proceed with manager login check
    if (key.equalsIgnoreCase("Y")) {
        loginCheck(true); // Search for manager data
    } else if (key.equalsIgnoreCase("N")) {
        loginCheck(false); // Search for employee data
    }

    // After login attempt, return to the main menu
    scene = SCENE_MAIN_MENU;
}
```
## Method: userLogin

### Description:
Handles the user login process for both managers and employees. Displays a login view, prompts the user to select whether they are logging in as a manager or employee, and processes their input accordingly.

### Parameters:
- *None*

### Returns:
- *void*: This method does not return a value. It performs actions based on user input, such as verifying login credentials and navigating back to the main menu.

### Usage:
The userLogin method is intended to be called when a user needs to log in to the system. It prompts the user to specify if they are logging in as a manager or employee and performs the login verification based on the user's selection.

### Workflow:
1. *Display Login View*: 
   - The method calls cView.loginView() to display the login interface.
   - Prompts the user with: "Login as manager? (Y/N)".

2. *Handle User Input*:
   - Receives the user's input using cView.userInput().
   - If the user enters "Q", the login process is canceled, and the system returns to the main menu (scene = SCENE_MAIN_MENU).

3. *Validate Input*:
   - If the input is not "Y" or "N", the user is prompted to enter a valid option repeatedly until they do so.

4. *Process Login Type*:
   - If the user enters "Y", loginCheck(true) is called to perform a login as a manager.
   - If the user enters "N", loginCheck(false) is called to perform a login as an employee.

5. *Return to Main Menu*:
   - After attempting the login (successful or unsuccessful), the method returns the user to the main menu by setting scene to SCENE_MAIN_MENU.

### Example:
java
// Initiate the user login process
userLogin();


In this example, the userLogin() method will:
- Display the login interface.
- Prompt the user to log in as a manager or employee.
- Perform the corresponding login verification based on user input.
- Return to the main menu after the login process is complete or if the user chooses to cancel.

---
# API Documentation for createPaymentList()

## Overview

The createPaymentList() method generates a formatted string that lists the payment details of staff members from a database. It calculates wages for finished work states and provides a summary of total payments and the number of staff members processed.

## Method Signature

java
public String createPaymentList()


## Returns

- *String*: A formatted string containing:
  - Staff ID
  - Staff Name
  - Work Time
  - Payment Amount
  - Total Payments and Count of Staff
```
public String createPaymentList()
{
// muath
    double totalPayment = 0;
    int staffNum = 0;
    String output = "";

    Iterator<Staff> it = cDatabase.getStaffList().iterator();
    while (it.hasNext())
    {
        Staff re = it.next();

        if (re.getWorkState() == Staff.WORKSTATE_FINISH)
        {
            double pay = re.culculateWages();
            output += String.format("Staff ID:%4d  StaffName:%-20s  Work time:%5.2f Pay:%5.2f\n",
                                    re.getID(), re.getFullName(), re.culculateWorkTime(), pay);
            staffNum++;
            totalPayment += pay;
        }
        else if (re.getWorkState() == Staff.WORKSTATE_ACTIVE)
        {
            output += String.format("Staff ID:%4d  StaffName:%-20s  * On work *\n",
                                    re.getID(), re.getFullName());
            staffNum++;
        }
    }
    output += "-------------------------------------------------------\n";
    output += String.format("Total payment:$%.2f (%d)", totalPayment, staffNum);
    return output;
}
```
## Description

The createPaymentList() method performs the following actions:

1. *Initialization*:
   - Initializes totalPayment to 0, staffNum to 0, and output as an empty string.

2. *Iterating through Staff Members*:
   - Uses an iterator to traverse the list of staff members retrieved from cDatabase.
   - For each staff member:
     - *Finished Work State*:
       - If the staff member's work state is WORKSTATE_FINISH, it calculates their wages and work time, appending this information to the output string.
       - Updates totalPayment and increments the staffNum.
     - *Active Work State*:
       - If the staff member's work state is WORKSTATE_ACTIVE, it appends a message indicating that the staff member is currently on work.
       - Increments the staffNum.

3. *Final Summary*:
   - Appends a separator line and a summary of the total payment and the number of staff members to the output string.

4. *Return Value*:
   - Returns the formatted output string.

## Example Usage

java
String paymentList = createPaymentList();
System.out.println(paymentList);


## Notes

- Ensure that the cDatabase object is properly initialized and contains valid staff data before calling this method.
- The method assumes that the Staff class has methods getWorkState(), culculateWages(), getID(), getFullName(), and culculateWorkTime() implemented.

## Dependencies

- Requires the Staff class and cDatabase instance to be defined in the same context.
- Assumes constants WORKSTATE_FINISH and WORKSTATE_ACTIVE are defined within the Staff class.

## Formatting

The output will be formatted as follows:


Staff ID: 1234  StaffName: John Doe           Work time: 40.00 Pay: 100
Staff ID: 5678  StaffName: Jane Smith         * On work *
-------------------------------------------------------
Total payment:$100 (2)


This provides a clear and organized view of the payment details for each staff member, along with a summary of total payments.
