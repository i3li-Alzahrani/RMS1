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

