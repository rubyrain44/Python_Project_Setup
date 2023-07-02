+Create Project Folder
    pipenv install PyMySQL flask
    pipenv shell
    pip list (to see whats installed)
    exit (cancels the environment)

    *To run the file* - python server.py
    *Localhost:5000*


+Modularization
    PROJECT FOLDER
        -flask_app
            __init__.py (double underlines)
                from flask import Flask
                app = Flask(__name__)
                app.secret_key = "shhhhhh"
        -config
            mysqlconnection.py
        -controllers (all of the routes)
            plural.py
                from flask_app import app
                from flask import render_template, redirect, request, session, flash
                from singular import Singular
                from flask_app.models.singular import Singular
                
                Routes
        -models
            singular.py
                from flask_app.config.mysqlconnection import connectToMySQL
                import re	# the regex module
                EMAIL_REGEX = re.compile(r'^[a-zA-Z0-9.+_-]+@[a-zA-Z0-9._-]+\.[a-zA-Z]+$') 
                Class 
                Class Functions/Queries
        -static
            -css
                styles.css
        -templates
            html files
        -server.py
            from flask_app.controllers import plural
