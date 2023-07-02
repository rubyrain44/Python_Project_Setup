BASIC VALIDATIONS=====================================================================================

+MODELS

Class Burger:

    @staticmethod
    def validate_burger(burger):
        is_valid = True # we assume this is true
        if len(burger['name']) < 3:
            flash("Name must be at least 3 characters.")
            is_valid = False
        if len(burger['bun']) < 3:
            flash("Bun must be at least 3 characters.")
            is_valid = False
        if int(burger['calories']) < 200:
            flash("Calories must be 200 or greater.")
            is_valid = False
        if len(burger['meat']) < 3:
            flash("Bun must be at least 3 characters.")
            is_valid = False
        return is_valid


+CONTROLLERS

from flask_app.models.burger import Burger

@app.route('/create', methods=['POST'])
def create_burger():
    # if there are errors:
    # We call the staticmethod on Burger model to validate
    if not Burger.validate_burger(request.form):
        # redirect to the route where the burger form is rendered.
        return redirect('/')
    # else no errors:
    Burger.save(request.form)
    return redirect("/burgers")


+INDEX.HTML

{% with messages = get_flashed_messages() %}     <!-- declare a variable called messages -->
    {% if messages %}                            <!-- check if there are any messages -->
        {% for message in messages %}            <!-- loop through the messages -->
            <p>{{message}}</p>                   <!-- display each message in a paragraph tag -->
        {% endfor %}
    {% endif %}
{% endwith %}

===================================================================================================================================

PATTERN VALIDATIONS=====================================================================================

+MODELS

import re	# the regex module
# create a regular expression object that we'll use later   
EMAIL_REGEX = re.compile(r'^[a-zA-Z0-9.+_-]+@[a-zA-Z0-9._-]+\.[a-zA-Z]+$') 
class User:
    @staticmethod
    def validate_user(user):
        is_valid = True
        # test whether a field matches the pattern
        if not EMAIL_REGEX.match(user['email']): 
            flash("Invalid email address!")
            is_valid = False
        return is_valid


+CONTROLLERS

from flask_app.models.user import User
@app.route('/register', methods=['POST'])
def register():
    if not User.validate_user(request.form):
        # we redirect to the template with the form.
        return redirect('/')
    # ... do other things
    return redirect('/dashboard')


*Say we want to categorize flash messages into different labels or buckets. We can utilize categories by passing a second argument in the flash function:*
    flash("Email cannot be blank!", 'email')