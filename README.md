# Ex.05 Design a Website for Server Side Processing
## Date:18/12/25

## AIM:
 To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side. 


## FORMULA:
P = I<sup>2</sup>R
<br> P --> Power (in watts)
<br> I --> Intensity
<br> R --> Resistance

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

## PROGRAM :
math.html:
```
<!DOCTYPE html>
<html>
<head>
    <title>Power Calculator</title>
    <style>
        body {
            background-color: red;
            font-family: Arial, sans-serif;
            text-align: center;
        }
        .container {
            background-color: blue;
            border: 5px dashed green;
            width: 400px;
            padding: 30px;
            margin: 100px auto;
            color: white;
            border-radius: 10px;
        }
        h1 {
            color: pink;
        }
        input[type="text"] {
            width: 100px;
            padding: 5px;
            margin-left: 10px;
        }
        input[type="submit"] {
            padding: 5px 15px;
            background-color: white;
            border: none;
            cursor: pointer;
            font-weight: bold;
        }
        input[type="submit"]:hover {
            background-color: lightgray;
        }
    </style>
</head>

<body>
<div class="container">
    <h1>Incandescent Bulb Power Calculator</h1>

    <form method="post">
        {% csrf_token %}
        <label>Current (I):</label>
        <input type="text" name="current" required><br><br>

        <label>Resistance (R):</label>
        <input type="text" name="resistance" required><br><br>

        <input type="submit" value="Calculate Power">
    </form>

    {% if result is not None %}
        <h2>Power (P) = {{ result }} Watts</h2>
    {% endif %}

    {% if error %}
        <p style="color:red">{{ error }}</p>
    {% endif %}
</div>
</body>
</html>

```
mathapp/views.py:
```
from django.shortcuts import render

def calculate_power(request):
    result = None
    error = None

    if request.method == 'POST':
        try:
            current = float(request.POST.get('current'))
            resistance = float(request.POST.get('resistance'))
            result = round((current ** 2) * resistance, 2)
        except:
            error = "Invalid input. Enter numbers only."

    return render(request, 'mathapp/math.html',
                  {'result': result, 'error': error})

```
mathapp/urls.py:
```
from django.urls import path
from . import views

urlpatterns = [
    path('', views.calculate_power, name='calculate_power'),
]

```
mathproject/urls.py:
```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('mathapp.urls')),
]

```
## SERVER SIDE PROCESSING:
![alt text](<server side processing.png>)
## HOMEPAGE:
![alt text](<Home page.png>)

## RESULT:
The program for performing server side processing is completed successfully.
