# 🛒 Amazon Website Automation using Selenium

## 📌 Project Overview

This project automates the **Amazon India website** using **Python and Selenium WebDriver**.

The automation performs a complete shopping flow:

1. Opens Amazon India
2. Searches for a laptop
3. Retrieves the search results
4. Displays the first 5 products
5. Opens the first product
6. Verifies the product page
7. Clicks **Add to Cart**
8. Checks the cart count
9. Verifies whether the product was successfully added to the cart

This project demonstrates basic **Web UI Automation Testing** using Selenium.

---

## 🛠️ Technologies Used

* **Python**
* **Selenium WebDriver**
* **Google Chrome**
* **ChromeDriver**
* **Amazon India**

### Python Libraries

```python
selenium
time
```

---


---

## ⚙️ Prerequisites

Before running the project, make sure you have:

* Python installed
* Google Chrome installed
* Selenium installed
* Internet connection

---

## 📥 Installation

### 1. Install Selenium

Open Command Prompt or Terminal and run:

```bash
pip install selenium
```

### 2. Verify Python

```bash
python --version
```

### 3. Verify Selenium

```bash
pip show selenium
```

---

## ▶️ How to Run

Run the Python file using:

```bash
python amazon_automation.py
```

The Chrome browser will automatically open and perform the automation steps.

---

## 🔄 Automation Flow

```text
Open Amazon
      ↓
Search for "laptop"
      ↓
Wait for search results
      ↓
Get product list
      ↓
Display first 5 products
      ↓
Click first product
      ↓
Open product page
      ↓
Find "Add to Cart"
      ↓
Click Add to Cart
      ↓
Check cart count
      ↓
Verify result
```

---

## 🔍 Selenium Concepts Used

### 1. WebDriver

```python
driver = webdriver.Chrome()
```

Creates a Chrome browser session using Selenium.

### 2. Navigate to Website

```python
driver.get("https://www.amazon.in/")
```

Opens Amazon India.

### 3. Locate Elements

The project uses different Selenium locators:

```python
By.ID
By.CSS_SELECTOR
```

Example:

```python
(By.ID, "twotabsearchtextbox")
```

### 4. Explicit Wait

```python
wait = WebDriverWait(driver, 20)
```

Explicit waits are used to wait until elements become available or clickable.

Example:

```python
wait.until(
    EC.element_to_be_clickable(
        (By.ID, "twotabsearchtextbox")
    )
)
```

### 5. Keyboard Action

```python
search_box.send_keys(Keys.ENTER)
```

Presses the Enter key after entering the search term.

### 6. Finding Multiple Elements

```python
products = driver.find_elements(
    By.CSS_SELECTOR,
    "div[data-component-type='s-search-result']"
)
```

Gets the available product search results.

### 7. JavaScript Click

```python
driver.execute_script(
    "arguments[0].click();",
    product_link
)
```

Uses JavaScript to click an element.

### 8. Verification

The cart count is checked after adding the product:

```python
if int(cart_count.text) > 0:
    print("ADD TO CART: PASS")
else:
    print("ADD TO CART: FAIL")
```

---

## Code 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Chrome()
driver.maximize_window()

wait = WebDriverWait(driver, 20)

try:
    # 1. Open Amazon
    driver.get("https://www.amazon.in/")
    print("Amazon opened")

    # 2. Search
    search_box = wait.until(
        EC.element_to_be_clickable(
            (By.ID, "twotabsearchtextbox")
        )
    )

    search_box.send_keys("laptop")
    search_box.send_keys(Keys.ENTER)

    print("Search completed")

    # 3. Wait for products
    wait.until(
        EC.presence_of_element_located(
            (By.CSS_SELECTOR, "div[data-component-type='s-search-result']")
        )
    )

    # 4. Get product list
    products = driver.find_elements(
        By.CSS_SELECTOR,
        "div[data-component-type='s-search-result']"
    )

    print("Products found:", len(products))

    # 5. Print first 5 products
    for i, product in enumerate(products[:5], start=1):
        try:
            name = product.find_element(
                By.CSS_SELECTOR,
                "h2"
            ).text

            print(i, name)

        except:
            pass

    # 6. Click first product
    first_product = products[0]

    product_link = first_product.find_element(
        By.CSS_SELECTOR,
        "h2 a"
    )

    driver.execute_script(
        "arguments[0].click();",
        product_link
    )

    print("First product clicked")

    # 7. Wait for product page
    wait.until(
        EC.presence_of_element_located(
            (By.ID, "productTitle")
        )
    )

    print("Product page opened")

    # 8. Find Add to Cart button
    add_to_cart = wait.until(
        EC.element_to_be_clickable(
            (By.ID, "add-to-cart-button")
        )
    )

    # 9. Click Add to Cart
    driver.execute_script(
        "arguments[0].click();",
        add_to_cart
    )

    print("Add to Cart clicked")

    # 10. Wait
    time.sleep(30)

    # 11. Verify cart
    cart_count = wait.until(
        EC.presence_of_element_located(
            (By.ID, "nav-cart-count")
        )
    )

    print("Cart count:", cart_count.text)

    if int(cart_count.text) > 0:
        print("ADD TO CART: PASS")
    else:
        print("ADD TO CART: FAIL")

    time.sleep(50)

except Exception as e:
    print("ERROR:", e)

finally:
    time.sleep(50)
    driver.quit()
```
## 🧪 Test Scenario

| Test Step | Test Action            | Expected Result                              |
| --------- | ---------------------- | -------------------------------------------- |
| 1         | Open Amazon            | Amazon homepage should open                  |
| 2         | Search for laptop      | Laptop search results should appear          |
| 3         | Get products           | Product list should be displayed             |
| 4         | Print first 5 products | First five product names should be displayed |
| 5         | Click first product    | Product details page should open             |
| 6         | Find Add to Cart       | Add to Cart button should be available       |
| 7         | Click Add to Cart      | Product should be added to cart              |
| 8         | Check cart count       | Cart count should be greater than 0          |
| 9         | Verify result          | Test should display PASS or FAIL             |

---

## Output
<img width="1916" height="1057" alt="image" src="https://github.com/user-attachments/assets/db3899b4-8cac-4ea2-b1d5-128789abc754" />


#### github link
https://github.com/Sarishatheiveegan/hcl-amazon-testing.git

## ⭐ Conclusion

This project demonstrates a simple end-to-end **Selenium Web Automation Test** for an e-commerce website.

It automates the process of searching for a product, opening the product, adding it to the cart, and verifying the cart count.
