<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            margin: 0;
            padding: 0;
            background-color: #111;
            color: white;
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        .neon-glow {
            font-size: 2em;
            text-align: center;
            color: #0ff;
            text-shadow: 0 0 10px #0ff, 0 0 20px #0ff, 0 0 30px #0ff;
            margin-bottom: 20px;
        }

        .instruction-box {
            background-color: rgba(0, 0, 0, 0.8);
            padding: 20px;
            border-radius: 10px;
            max-width: 400px;
        }

        input, select, button {
            margin-bottom: 10px;
            width: 100%;
            padding: 10px;
            box-sizing: border-box;
        }

        button {
            background-color: #0ff;
            color: #111;
            cursor: pointer;
            border: none;
            border-radius: 5px;
        }

        #price {
            font-size: 1.2em;
            text-align: center;
            margin-top: 10px;
        }
    </style>
    <title>HM SMM SERVICES</title>
</head>
<body>
    <div class="neon-glow">HM SMM SERVICES</div>
    <div class="instruction-box">
        <p>Please enter your name:</p>
        <input type="text" id="userName" placeholder="Your Name" required>
        <br>
        <p>Select a category:</p>
        <select id="category" onchange="showSubcategories(); calculatePrice();">
            <option value="" selected disabled>Select Category</option>
            <option value="Facebook">Facebook</option>
            <option value="Instagram">Instagram</option>
            <option value="YouTube">YouTube</option>
        </select>
        <br>
        <div id="subcategoryBox" style="display: none;">
            <p>Select a subcategory:</p>
            <select id="subcategory" onchange="calculatePrice();">
                <option value="" selected disabled>Select Subcategory</option>
            </select>
        </div>
        <br>
        <p>Enter quantity:</p>
        <input type="number" id="quantity" placeholder="Quantity" required onchange="calculatePrice();">
        <br>
        <p>Paste the link:</p>
        <input type="text" id="link" placeholder="Paste Link">
        <br>
        <div id="price" class="neon-glow"></div>
        <button onclick="calculatePrice()">Refresh Price</button>
        <button onclick="submitForm()">Submit</button>
    </div>

    <script>
        function showSubcategories() {
            var category = document.getElementById("category").value;
            var subcategoryBox = document.getElementById("subcategoryBox");
            var subcategorySelect = document.getElementById("subcategory");

            // Clear existing options
            subcategorySelect.innerHTML = '<option value="" selected disabled>Select Subcategory</option>';

            if (category === "Facebook" || category === "Instagram" || category === "YouTube") {
                subcategoryBox.style.display = "block";

                // Add subcategories based on the selected category
                switch (category) {
                    case "Facebook":
                    case "Instagram":
                    case "YouTube":
                        addOption(subcategorySelect, "Followers");
                        addOption(subcategorySelect, "Likes");
                        addOption(subcategorySelect, "Views");
                        if (category === "YouTube") {
                            // Replace "Followers" with "Subscribers" for YouTube
                            subcategorySelect.options[0].text = "Subscribers";
                        }
                        break;
                    default:
                        break;
                }
            } else {
                subcategoryBox.style.display = "none";
            }
        }

        function calculatePrice() {
            var category = document.getElementById("category").value;
            var subcategory = document.getElementById("subcategory").value;
            var quantity = document.getElementById("quantity").value;
            var price = 0;

            switch (subcategory) {
                case "Followers":
                    switch (category) {
                        case "Facebook":
                            price = 300 * quantity / 1000;
                            break;
                        case "Instagram":
                            price = 150 * quantity / 1000;
                            break;
                        case "YouTube":
                            price = 2000 * quantity / 1000;
                            break;
                        default:
                            break;
                    }
                    break;
                case "Likes":
                    switch (category) {
                        case "Facebook":
                            price = 250 * quantity / 1000;
                            break;
                        case "Instagram":
                            price = 50 * quantity / 1000;
                            break;
                        case "YouTube":
                            price = 2000 * quantity / 1000;  // Assuming same price for YouTube likes
                            break;
                        default:
                            break;
                    }
                    break;
                case "Views":
                    switch (category) {
                        case "Facebook":
                            price = 200 * quantity / 1000;
                            break;
                        case "Instagram":
                            price = 20 * quantity / 1000;
                            break;
                        case "YouTube":
                            price = 2000 * quantity / 1000;  // Assuming same price for YouTube views
                            break;
                        default:
                            break;
                    }
                    break;
                case "Subscribers":
                    if (category === "YouTube") {
                        price = 2000 * quantity / 1000;  // Assuming same price for YouTube subscribers
                    }
                    break;
                default:
                    break;
            }

            document.getElementById("price").innerText = `Estimated Price: Rs ${price.toFixed(2)}`;
        }

        function submitForm() {
            var userName = document.getElementById("userName").value;
            var category = document.getElementById("category").value;
            var subcategory = document.getElementById("subcategory").value;
            var quantity = document.getElementById("quantity").value;
            var link = document.getElementById("link").value;

            var phoneNumber = '7982631298';  // Replace with the actual phone number

            var message = `Name: ${userName}\nCategory: ${category}\nSubcategory: ${subcategory}\nQuantity: ${quantity}\nLink: ${link}\nEstimated Price: Rs ${document.getElementById("price").innerText.split(":")[1].trim()}`;
            var whatsappLink = `https://wa.me/${phoneNumber}?text=${encodeURIComponent(message)}`;

            window.location.href = whatsappLink;
        }

        function addOption(selectElement, optionText) {
            var option = document.createElement("option");
            option.text = optionText;
            option.value = optionText;
            selectElement.add(option);
        }
    </script>
</body>
</html>
