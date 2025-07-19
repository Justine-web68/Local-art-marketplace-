<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Add New Product - Local Craft Marketplace</title>
    <style>
        /* General Body Styling */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; /* Modern font */
            margin: 0;
            padding: 20px; /* Add some padding around the content */
            background: linear-gradient(to right, #f8f9fa, #e9ecef); /* Subtle gradient background */
            color: #343a40; /* Darker text for readability */
            display: flex; /* Use flexbox to center the container */
            justify-content: center;
            align-items: center;
            min-height: 100vh; /* Ensure it takes full viewport height */
            box-sizing: border-box; /* Include padding in element's total width and height */
        }

        /* Main Container Styling */
        .container {
            max-width: 750px; /* Slightly wider */
            width: 100%; /* Ensure it's responsive */
            padding: 40px; /* More padding inside */
            background-color: #ffffff;
            border-radius: 12px; /* More rounded corners */
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.1); /* Softer, larger shadow */
            box-sizing: border-box;
        }

        /* Header Styling */
        h1 {
            text-align: center;
            color: #4a69bd; /* A calming blue */
            margin-bottom: 35px; /* More space below header */
            font-size: 2.2em; /* Larger heading */
            font-weight: 600; /* Semi-bold */
        }

        /* Form Group Styling */
        .form-group {
            margin-bottom: 25px; /* More space between form groups */
        }

        /* Label Styling */
        label {
            display: block;
            margin-bottom: 10px; /* Space below label */
            font-weight: 600; /* Semi-bold */
            color: #495057; /* Slightly darker label text */
            font-size: 1.1em; /* Slightly larger font */
        }

        /* Input, Textarea, Select Styling */
        input[type="text"],
        input[type="number"],
        textarea,
        select {
            width: 100%; /* Full width */
            padding: 12px 15px; /* More padding */
            border: 1px solid #ced4da; /* Lighter border */
            border-radius: 8px; /* More rounded inputs */
            font-size: 1em; /* Standard font size */
            color: #495057;
            box-sizing: border-box; /* Crucial for padding/border not adding to width */
            transition: border-color 0.3s ease, box-shadow 0.3s ease; /* Smooth transitions */
        }

        input[type="text"]:focus,
        input[type="number"]:focus,
        textarea:focus,
        select:focus {
            border-color: #6a89cc; /* Highlight border on focus */
            box-shadow: 0 0 0 0.2rem rgba(106, 137, 204, 0.25); /* Subtle glow on focus */
            outline: none; /* Remove default outline */
        }

        textarea {
            resize: vertical;
            min-height: 120px; /* Taller textarea */
        }

        input[type="file"] {
            padding: 10px 0; /* Align with other inputs */
            font-size: 1em;
            color: #495057;
        }

        /* Button Styling */
        button {
            display: block;
            width: 100%;
            padding: 15px 25px; /* Larger padding for button */
            background-color: #6a89cc; /* Primary action blue */
            color: white;
            border: none;
            border-radius: 8px; /* Match input rounding */
            font-size: 1.2em; /* Larger text for button */
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease; /* Smooth transitions */
            letter-spacing: 0.5px; /* Slightly spaced letters */
        }

        button:hover {
            background-color: #4a69bd; /* Darker blue on hover */
            transform: translateY(-2px); /* Slight lift effect */
        }

        button:active {
            transform: translateY(0); /* Press down effect */
            background-color: #3b5093;
        }

        /* Responsive Adjustments (Optional but good practice) */
        @media (max-width: 768px) {
            .container {
                margin: 15px;
                padding: 25px;
            }
            h1 {
                font-size: 1.8em;
            }
            button {
                font-size: 1.1em;
            }
        }

        @media (max-width: 480px) {
            body {
                padding: 10px;
            }
            .container {
                padding: 20px;
            }
            h1 {
                font-size: 1.5em;
                margin-bottom: 25px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Add New Craft Product</h1>
        <form id="productForm">
            <div class="form-group">
                <label for="productName">Product Name:</label>
                <input type="text" id="productName" name="productName" placeholder="e.g., Hand-carved Wooden Animal" required>
            </div>

            <div class="form-group">
                <label for="description">Description:</label>
                <textarea id="description" name="description" placeholder="Describe your craft, materials used, inspiration, etc." required></textarea>
            </div>

            <div class="form-group">
                <label for="price">Price (TZS):</label>
                <input type="number" id="price" name="price" step="0.01" min="0" placeholder="e.g., 50000.00" required>
            </div>

            <div class="form-group">
                <label for="category">Category:</label>
                <select id="category" name="category" required>
                    <option value="">Select a Category</option>
                    <option value="Pottery">Pottery & Ceramics</option>
                    <option value="Jewelry">Jewelry</option>
                    <option value="Textiles">Textiles & Fabric Art</option>
                    <option value="Woodcraft">Woodcraft</option>
                    <option value="Painting">Painting & Drawing</option>
                    <option value="Sculpture">Sculpture</option>
                    <option value="Leatherwork">Leatherwork</option>
                    <option value="Other">Other Crafts</option>
                </select>
            </div>

            <div class="form-group">
                <label for="productImages">Product Images (up to 5):</label>
                <input type="file" id="productImages" name="productImages" accept="image/*" multiple>
            </div>
            
            <button type="submit">List Product</button>
        </form>
    </div>

    <script>
        document.getElementById('productForm').addEventListener('submit', function(event) {
            event.preventDefault(); // Stop the form from refreshing the page

            // Get values from each input field
            const productName = document.getElementById('productName').value;
            const description = document.getElementById('description').value;
            const price = parseFloat(document.getElementById('price').value); // Convert price to a number
            const category = document.getElementById('category').value;
            const productImages = document.getElementById('productImages').files; // This will be a FileList object

            // Create an object to hold all the product data
            const productData = {
                name: productName,
                description: description,
                price: price,
                category: category,
                // For images, we typically don't send the entire file data directly in a simple form.
                // We'd upload them to storage (like Firebase Storage) and save their URLs.
                // For now, we'll just log the number of files selected.
                imageCount: productImages.length
            };

            // Log the collected data to the console
            console.log('Product Data Collected:', productData);

            // You can also show a temporary message to the user
            alert('Product data captured! Check your browser console for details. Next, we will save this data to a database.');

            // Clear the form after submission (optional)
            this.reset();
        });
    </script>
</body>
</html>
