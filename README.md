# Flask Login App

This is a simple Flask application that demonstrates user login functionality using Flask-WTF for forms and Flask-Bootstrap for styling.

## Features
- Login form with email and password fields.
- Validation for email and password using Flask-WTF.
- Basic routing for home, login, success, and access denied pages.
- Bootstrap integration for styling.

---

## Installation

### Prerequisites
- Python 3.7+
- Pip (Python package manager)

### Clone the Repository
```bash
git clone <repository-url>
cd <repository-folder>
```

### Set Up a Virtual Environment (Optional but Recommended)
```bash
python -m venv venv
source venv/bin/activate  # On macOS/Linux
venv\Scripts\activate   # On Windows
```

### Install Dependencies
Run the following command to install required packages:
```bash
pip install -r requirements.txt
```

If you're using macOS, you may need to use:
```bash
pip3 install -r requirements.txt
```

---

## Application Structure

```
.
├── app.py              # Main application file
├── templates/          # HTML templates
│   ├── index.html
│   ├── login.html
│   ├── success.html
│   └── denied.html
├── requirements.txt    # Required Python packages
└── README.md           # Project documentation
```

---

## Running the Application
Start the Flask server by running:
```bash
python app.py
```

The application will be available at: [http://127.0.0.1:5001](http://127.0.0.1:5001)

---

## Functionality

### Routes
- `/`: Home page.
- `/login`: Login page with email and password form.
  - Valid credentials:
    - **Email**: `admin@email.com`
    - **Password**: `12345678`
  - Successful login redirects to `success.html`.
  - Failed login redirects to `denied.html`.

---

## Required Packages
The application uses the following Python packages:
- `Flask`
- `Flask-WTF`
- `WTForms`
- `Flask-Bootstrap`
- `email-validator`

These can be installed by running:
```bash
pip install -r requirements.txt
```

---

## Example Code
Below is a quick overview of the `LoginForm` and routing logic:

```python
from flask import Flask, render_template
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, SubmitField
from wtforms.validators import DataRequired
from flask_bootstrap import Bootstrap5

class LoginForm(FlaskForm):
    email = StringField("Email", validators=[DataRequired()])
    password = PasswordField("Password", validators=[DataRequired()])
    submit = SubmitField(label="Log In")

app = Flask(__name__)
app.secret_key = "YourSecretKey"
bootstrap = Bootstrap5(app)

@app.route("/login", methods=["GET", "POST"])
def login():
    form = LoginForm()
    if form.validate_on_submit():
        if form.email.data == "admin@email.com" and form.password.data == "12345678":
            return render_template("success.html")
        else:
            return render_template("denied.html")
    return render_template("login.html", form=form)

if __name__ == "__main__":
    app.run(debug=True, port=5001)
```

