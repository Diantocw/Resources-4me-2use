# Resources-4me-2use

Task 1 
Functional Requirements:

Users need to be able to register a unique account through username, email, password and optionally phone number.
Logins need secure authentification mechanisms, like password hashes or 2FA
Password reset functions must be available in case a password is forgotten
Clients must be able to add, update and store product data, with fields for name, description, quantity and price.
Input data must be validated, changes must be logged and audited, and updated product info should be displayed in an orderly and searchable format.
users must be able to select items, bring them into a cart and provide payment details to purchase those items, with support for multiple payment methods. 
Payment Processing must be secure and done through encrypted and secure gateways, updating inventory on a valid purchase. 
Users should recieve confirmation of payment through email or SMS.

Non-Functional Requirements:
Systems must be compatible with screen readers and text to speech software for visually impaired users, Including ARIA (Accessible Rich Internet Applications) landmarks and roles if possible.
Systems colour scheme should be primarily high contrast colours, with the option to customise those colours or change them over to a dark mode theme.

System must be navigatable using Keyboard Shortcuts to ensure that motor impaired users can utilise the system.
The System Interface must be user friendly and intuitive through clear points of navigation and interactive elements. Consistency in design alongside tooltips and guides will help enforce this.
The System must be compatible across a variety of devices, screen sizes and system specifications, for example: Tablets, PCs, Phones, Laptops, Macbooks, ios, Android, Linux, Windows, Mac os etc.
The system should have minimal load times and be robust enough to handle a variety of stressful conditions, this can be achieved through code and resource optimisation.

Data stored and transmitted by the system must be stored utilising strong encryption principles. This includes the used of SSL/TLS for secure communications. 
Sensitive Information must be encrypted and authenticated through hashes and MFA (Multi Factor Authentication) Regular Security Audits  should be conducted to identify and Address vulnerabilities.
These measures to keep user information safe from breaches and unauthorized access/Misuse must comply with lawful standards, and these measures must be inspected regularly to ensure effectiveness.

The system must tolerate large volumes of traffic, transactions efficiently, and with as minimal error as is possible even at peaks in capacity, utilising scalable infrastructures and load balancing to achieve this.

The system should provide real time update and response times, to keep users in sync with feedback and information that is added. Appropriate usage of Asyncronus Caching will allow us to achieve that goal.

The system must continually be capable of meeting or exceeding user demands through scalable infrastructure and design, to allow changes to resource flow and capacities.

KPIs outlined, explain why

Solution effectiveness, Break down each page's purpose and why you chose to design it that way.
Data Dictionary + Key: 


Entity Relationship Diagrams:

All data here should be annotated in a data dictionary + give it a description

Staff Registration
  Staff ID (Primary Key)
  Password
  Email
  Phone Number
  Registry Date
  Last Login
  Role
  
User Registration
User ID (Primary Key)
Password
Email
Phone Number
Registry Date
Role

Product Information
Product ID
Purchase Information
Order Tracking

Add a Task flow to show how pages would be navigated

Test plan, covering all the features on each page, prerequisites to adding them and dependancies
Usability testing, 
A/B testing
Accessibility testing 
All forms of User Experience Tests, require defined user testing groups, and one group with very diverse needs.

Page Load Times
Response Times
Scalability
All performance tests, Requires performance testing tools and a deployed website.

Wireframes/Sketches Benefits *elaborate on each point's importance* :
Early Visualisations

Important Legal and Regulatory Requirements:
WCAG compliance for accessibility
GDPR for data privacy
Consumer Rights act 2015
Copyright, Designs and patents act 1988
Online Safety bill compliance
National Cyber Security Centre.

Effectiveness of the solution:
Explain what each page's purpose is, and how the designs added will contribute to that.
Explain how your designs contributes to solution effectiveness (Consistency, Simplicity, Responsiveness, Accesspibility)
Explain how your functionality is effective, (Login/Signup, Purchase Processing, Product Management, Community, Contact & Support

Algorithms for each page


Compatibility of the solution with users:
Who is most likely to use the solution?
Accessibility users (people who struggle to, or cannot go to grocery stores)
Families & General Users
Environmental Advocates and Community Leaders

Functional user compatibility (Ai Driven Insights to predict shopper wants or costs compared to competitors. Efficient ordering system customisable user experience, intuitive dashboards.) 

Accessibility Considerations and tools: 
WCAG Compliance 
Color Palette & contrast considerations
High contrast mode for visually impaired
Typography & Readability Elements
Layouts & Navigation





Task 1 END



Task 2
Make products table for shop page

CREATE TABLE products (
     id INT NOT NULL ,
     name TEXT NOT NULL,
     price INT NOT NULL,
     PRIMARY KEY (id)
);

Cart page: Alter to fit with website schema from template, add bootstrap and navbar functionality etc.

<!DOCTYPE html>
<html>

<head>
    <title>Shopping Cart</title>

</head>
<style>
    body {
        background-color: green;
    }
    header, nav, main, footer {
        background-color: white;
    } 
    table {
        border-collapse: collapse;
        width: 100%;
    }
    th, td {
        text-align: left;
        padding: 8px;
    }
    th {
        background-color: #dddddd;
    }
    tr:nth-child(even) {
        background-color: #f2f2f2;
    }
    footer {
        background-color: green;
        margin-top: 348px;
        color: black;
        max-width: 264px;
    
    }
    
    
</style>

<body>
    <header>
        <h1><?php session_start();
$user = $_SESSION['user'];
echo $user['name']; ?> Shopping Cart</h1>
    </header>

    <nav>
        <ul>
            <li>
                <a href="shop.html">Home</a>
            </li>
            <li>
                <a href="shop.html">Products</a>
            </li>
            <li>
                <a href=
"#">Contact Us</a>
            </li>
            <li>
                <a href="cart.php">Cart</a>
            </li>
        </ul>
    </nav>

    <main>
        <section>
            <table>
                <tr>
                    <th>Product Name </th>
                    <th>Quantity </th>
                    <th>Price </th>
                    <th>Total </th>
                </tr>
                <?php
                $servername = "localhost";
                $username = "root";
                $password = "";
                $dbname = "shp";

                // Create connection
                $conn = 
                    new mysqli($servername, $username, $password, $dbname);

                // Check connection
                if ($conn->connect_error) {
                    die("Connection failed: " . $conn->connect_error);
                }

                $total = 0;

                // Loop through items in cart and display in table
                foreach ($_SESSION['cart'] as $product_id => $quantity) {
                    $sql = "SELECT * FROM products WHERE id = $product_id";
                    $result = $conn->query($sql);

                    if ($result->num_rows > 0) {
                        $row = $result->fetch_assoc();
                        $name = $row['name'];
                        $price = $row['price'];
                        $item_total = $quantity * $price;
                        $total += $item_total;

                        echo "<tr>";
                        echo "<td>$name</td>";
                        echo "<td>$quantity</td>";
                        echo "<td>$price $</td>";
                        echo "<td>$item_total $</td>";
                        echo "</tr>";
                    }
                }
                // Display total
                echo "<tr>";
                echo "<td colspan='3'>Total:</td>";
                echo "<td>$total $</td>";
                echo "</tr>";
                ?>
            </table>
            <form action="checkout.php" method="post">
                <input type="submit" 
                       value="Checkout" 
                       class="button" />
            </form>
        </section>
    </main>

    <footer>
        <p>&COPY;2023 GFG Shopping Web Application</p>
    </footer>
</body>

</html>

Similar scenario as above.
<!DOCTYPE html>
<html>

<head>
    <title>Checkout Page</title>
    <link rel="stylesheet" 
          type="text/css" 
          href="checkout.css">
</head>
<style>
    body {
        background-color: #ffffff;
        font-family: Arial, sans-serif;
    }
    
    header {
        background-color: green;
        color: #ffffff;
        padding: 20px;
    }
    
    nav ul {
        margin: 0;
        padding: 0;
        list-style: none;
    }
    
    nav li {
        display: inline-block;
        margin-right: 20px;
    }
    
    nav a {
        color: #ffffff;
        text-decoration: none;
    }
    
    nav a:hover {
        text-decoration: underline;
    }
    
    section {
        max-width: 600px;
        margin: 0 auto;
        padding: 20px;
    }
    
    h1 {
        color: green;
        font-size: 32px;
        margin-bottom: 20px;
    }
    
    h2 {
        color: green;
        font-size: 24px;
        margin-bottom: 10px;
    }
    
    label {
        display: block;
        margin-bottom: 5px;
        color: #666666;
    }
    
    input[type="text"],
    input[type="email"] {
        width: 100%;
        padding: 10px;
        border: 1px solid #cccccc;
        border-radius: 5px;
        margin-bottom: 10px;
        font-size: 16px;
    }
    
    input[type="submit"] {
        background-color: green;
        color: #ffffff;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        font-size: 16px;
        cursor: pointer;
    }
    
    input[type="submit"]:hover {
        background-color: #228B22;
    }
    
    footer {
        background-color: green;
        color: #ffffff;
        padding: 20px;
        text-align: center;
    }
    
</style>

<body>
    <header>
        <nav>
            <ul>
                <li>
                    <a href="shop.php">Home</a>
                </li>
                <li>
                    <a href="shop.php">Shop</a>
                </li>
                <li>
                    <a href="cart.php">Cart</a>
                </li>
                <li>
                    <a href=
"#">Contact</a>
                
                       </li>
            </ul>
        </nav>
    </header>

    <section>
        <h1>Checkout</h1>
        <form action="thanks.php" method="post">
            <h2>Billing Information</h2>
            <label for="name">Name:</label>
            <input type="text" 
                   id="name"
                   name="name" required>

            <label for="email">Email:</label>
            <input type="email" 
                   id="email" 
                   name="email" required>

            <label for="address">Address:</label>
            <input type="text" 
                   id="address" 
                   name="address" required>

            <label for="city">City:</label>
            <input type="text" 
                   id="city" 
                   name="city" required>

            <label for="state">State:</label>
            <input type="text" 
                   id="state" 
                   name="state" required>

            <label for="zip">Zip Code:</label>
            <input type="text" 
                   id="zip"
                   name="zip" required>

            <h2>Payment Information</h2>
            <label for="cardholder">Name on Card:</label>
            <input type="text" id="cardholder" 
                   name="cardholder" required>

            <label for="cardnumber">Card Number:</label>
            <input type="text" 
                   id="cardnumber" 
                   name="cardnumber" required 
                   pattern="\d{4}-?\d{4}-?\d{4}-?\d{4}" required=>


            <label for="expmonth">Expiration Month:</label>
            <input type="text" 
                   id="expmonth" 
                   name="expmonth" required>

            <label for="expyear">Expiration Year:</label>
            <input type="text" 
                   id="expyear" 
                   name="expyear" required>

            <label for="cvv">CVV:</label>
            <input type="text" 
                   id="cvv"
                   name="cvv" required>

            <input type="submit" 
                   value="Place Order">
        </form>
    </section>

    <footer>
        <p>&copy; 2023 GFG Shopping Web Application</p>
    </footer>
</body>

</html>



page to be placed after purchase.

<html>

<head>
    <style>
        body {
            background-color: #f2f2f2;
            font-family: Arial, sans-serif;
        }
        
        h1 {
            color: #008000;
            font-size: 2.5em;
            text-align: center;
            margin-top: 50px;
        }
        
        p {
            color: #333;
            font-size: 1.2em;
            text-align: center;
            margin-top: 20px;
        }
        
        
    </style>
</head>


<?php
   // Start the session
    session_start();

 // Retrieve the customer name from the session variable
    if (isset($_SESSION['user'])) {
        $user = $_SESSION['user'];
        $customerName = $user['name'];
    } else {
        $customerName = "Valued Customer";
    }

 // Display the thank you message
    echo "<h1>Thank You, $customerName!</h1>";
    echo 
"<p>Your order has been received and will be delivered soon.</p>";
    ?>
</html>

Breakdown the development process you go through implementing these pages and features, do not forget to add in any errors and how you fix them. Be as transparent as possible, if you change something in any way it probably should be added.

Comment, Comment, Comment. Add comments to blocks of code to explain what they do, and any additional information that would help someone who hasn't touched your code.

ABC! ALWAYS! BE! COMMENTING!





