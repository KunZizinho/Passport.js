     REVERSE ENGINEERING PASSPORT.JS


# Server
    Setting up server by importing/requiring necessary dependencies.
        Express to set up aur server.
        Express-session as middleware so that every user gets assigned a unique session and this allows us to store user state maintained by express.
        Passport.js from config folder, where we import/require passport module.
        We use passport module as an authentication middlerware in wich we use strategies to authenticate requests.

                ## passport.js
                    In passport file we use the local strategy to athenticate if user has valid credentials as well as a code that takes care of new sign ups.
                    In order to help keeping authentication state across HTTP requests, sequelize needs to serialize and deserialize the user.
                    by requiring models folder we are ensuring that tru sequelize we are gonna define our db table and its endpoints for user data.
                    We also import/reqire bcryptjs to hash our password.
                    Then we are creating a custom method that will checked if an unhashed password entered by user can be compared to the hashed password stored in our database.
                    By creating hooks  we are automatically running thru various phases of the User model lifecycle,
                    in our case, before a User is created, we will automatically hash their password.
        We are setting up a port for our server and requiring/importing models folder for syncing

                ## models folder index.js/user.js
                    Using Sequelize we are creating our table dynamically using users input as endpoints for the table
                    Using  bcryptjs to hash our password.
        Then we are creating express app and configuring middleware needed for authentication.
        app.use(express.urlencoded({ extended: true }));  ---> Returns middleware that only parses urlencoded bodies and only looks at requests where the Content-Type header matches the type option.
        app.use(express.json()); --> Returns middleware that only parses json and only looks at requests where the Content-Type header matches the type option.
        app.use(express.static("public")); --> Create a new middleware function to serve files from within a given root directory. The file to serve will be determined by combining req.url with the provided root directory. When a file is not found, instead of sending a 404 response, this module will instead call next() to move on to the next middleware, allowing for stacking and fall-backs.
        app.use(session({ secret: "keyboard cat", resave: true, saveUninitialized: true }));
        app.use(passport.initialize());
        app.use(passport.session()); --> We also need to initialize passport and pasport session to keep track of our user's log in we are 
        In my case i ignored html files because i used handlebars in this activity.
        As import/require express-handlebars module and set it up  we are also importing/requiring isAuthenticated file from our config/middleware folder.

                ## handlebars 
                    We are rendering our front end thru decided routes.
                    Requiring/importign isAuthenticated file gives an option to check if user is sign in before accesing the members pages of our application.

                ## api-routes
                    We are importing/requiring models folder as well as passport file from our config folder for authentication/creation of user profile.
                    Here is where we are gonna have all our GET and POST methods for our database.

        we are routing all our front end and using the isAuthenticated as a methot to deny or allow premission to certain pages of the app depending on user having valid account or not.
        We also have to import/require api-routes file to manipulate our database.
        And last is 
        db.sequelize.sync().then(function() {
        app.listen(PORT, function() {
        console.log("==> 🌎  Listening on port %s. Visit http://localhost:%s/ in your browser.", PORT, PORT);
            });
        });   -->  Which is syncing our database and loging message to the user upon success.
