## Flask Application Design

### HTML Files
- **index.html**: This will be the homepage of the website. It will have a description of the project and a link to a page where users can input their income level to view available schemes.
- **schemes.html**: This page will have a form where users can input their income level, and based on their input, it will display a list of schemes they are eligible for.

### Routes
- **\**: This route will render the `index.html` file, which will be the homepage of the website.
- **/schemes**: This route will handle the form submission from `schemes.html` and return the `schemes.html` file with the list of eligible schemes based on the user's input income level.

### Application Structure
```
├── app.py
├── templates
│   ├── index.html
│   └── schemes.html
```

### Implementation
#### app.py
```python
from flask import Flask, render_template, request
import schemes_data

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/schemes', methods=["GET", "POST"]
def schemes():
    if request.method == 'POST':
        income = request.form['income']
        schemes = schemes_data.get_schemes(income)
        return render_template('schemes.html', schemes=schemes)
    return render_template('schemes.html')

if __name__ == '__main__':
    app.run(debug=True)
```

#### schemes_data.py
```python
schemes_data = {
    "below_poverty_line": {
        "schemes": [
            "Scheme 1",
            "Scheme 2",
        ]
    },
    "low_income": {
        "schemes": [
            "Scheme 3",
            "Scheme 4",
        ]
    },
    "middle_income": {
        "schemes": [
            "Scheme 5",
            "Scheme 6",
        ]
    },
    "high_income": {
        "schemes": [
            "Scheme 7",
            "Scheme 8",
        ]
    },
}

def get_schemes(income):
    if income < 10000:
        return schemes_data["below_poverty_line"]["schemes"]
    elif income < 20000:
        return schemes_data["low_income"]["schemes"]
    elif income < 50000:
        return schemes_data["middle_income"]["schemes"]
    else:
        return schemes_data["high_income"]["schemes"]
```