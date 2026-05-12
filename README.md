# Ex.04 Design a Website for Server Side Processing
## Date:12/5/26

## AIM:
To create a web page to calculate total bill amount with GST from price and GST percentage, using server-side scripts.

## FORMULA:
Bill = P + (P * GST / 100)
<br> P --> Price (in Rupees)
<br> GST --> GST (in Percentage)
<br> Bill --> Total Bill Amount (in Rupees)

## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Create python programs for views and urls to perform server side processing.

### Step 5:
Create a HTML file to implement form based input and output.

### Step 6:
Publish the website in the given URL.

## PROGRAM:
views.py
```
from django.shortcuts import render

def home(request):

    total = None
    gst_amount = None

    if request.method == 'POST':

        price = float(request.POST['price'])
        gst = float(request.POST['gst'])

        gst_amount = (price * gst) / 100
        total = price + gst_amount

    return render(request, 'home.html', {
        'total': total,
        'gst_amount': gst_amount
    })
```
home.html
```
<!DOCTYPE html>
<html>
<head>

    <title>GST Bill Calculator</title>

    <style>

        body{
            font-family: Arial;
            text-align:center;
            margin-top:50px;
        }

        h1{
            color:darkblue;
            font-size:45px;
        }

        form{
            font-size:25px;
        }

        input{
            font-size:22px;
            padding:8px;
            margin:10px;
        }

        button{
            font-size:22px;
            padding:10px 20px;
            background-color:green;
            color:white;
            border:none;
            border-radius:5px;
        }

        h2{
            color:red;
            font-size:30px;
        }

    </style>

</head>

<body>

    <h1>GST Bill Calculator</h1>

    <form method="POST">

        {% csrf_token %}

        <label>Enter Price:</label>

        <input type="number" name="price" required>

        <br><br>

        <label>Enter GST Percentage:</label>

        <input type="number" name="gst" required>

        <br><br>

        <button type="submit">Calculate Bill</button>

    </form>

    {% if total %}

        <h2>GST Amount = ₹ {{ gst_amount }}</h2>

        <h2>Total Bill Amount = ₹ {{ total }}</h2>

    {% endif %}

</body>
</html>
```


## OUTPUT - SERVER SIDE:
<img width="1918" height="1132" alt="image" src="https://github.com/user-attachments/assets/a2fb1447-bf65-4104-9320-79b4728108ba" />



## OUTPUT - WEBPAGE:
<img width="1914" height="1019" alt="image" src="https://github.com/user-attachments/assets/7dcb1cad-11a0-401e-96cb-9bbe33e2a390" />
<img width="1919" height="1033" alt="image" src="https://github.com/user-attachments/assets/ec0affea-cb53-41a2-b09f-61e64633e1b3" />




## RESULT:
The a web page to calculate vehicle mileage and fuel efficiency using server-side scripts is created successfully.
