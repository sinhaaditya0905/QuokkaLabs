# QuokkaLabs - Net Core web Api 8 

#Database Integration:
#1. ApplicationDbContext.cs

This file represents the database context for the application. It's integrated into the application using Entity Framework Core.

#Purpose:

Manages the interaction with the database.
Methods:

OnModelCreating: Configures relationships and constraints between database tables.
Special Considerations:

Defines a Users table to store user information.
Configures a unique index on the UserName property to ensure uniqueness.
#2. User.cs

This class represents the User entity in the application.

Purpose:

Defines the structure of the User entity.
Properties:

Id: Unique user identifier.
UserName: User's username.
PasswordHash: Securely hashed password.
Special Considerations:

Passwords are securely hashed, ensuring they are not stored in plain text.
Relationships with other entities, such as articles, can be defined here.
#3. AuthController.cs

This controller handles user authentication and registration.

Registration (/api/v1/register):

Validates input.
Checks for duplicate usernames.
Hashes passwords securely.
Saves users to the database.
Login (/api/v1/login):

Accepts login requests.
Authenticates users.
Generates JWT tokens for successful logins.
Special Considerations:

Passwords are securely hashed.
Registration checks for duplicate usernames.
#JWT tokens are generated for secure communication.
#Session and Tokens (JWT):
#1. AuthController.cs

#Login (/api/v1/login):

Generates JWT tokens for successful logins.
#2. Startup.cs

#ConfigureServices:

Configures JWT authentication.
Special Considerations:

JWT authentication is added to secure APIs.
Authorization policies are set up to ensure proper access control.
#CRUD Operations:
#1. ArticleController.cs

This controller manages CRUD operations for articles.

#GetArticles (/api/v1/articles):

Retrieves a list of articles from the database.
CreateArticle (/api/v1/articles):

#Validates input.
Retrieves user information from the token.
Saves the article to the database.
UpdateArticle (/api/v1/articles/{id}):

#Validates input.
Retrieves the existing article.
Checks if the current user is the owner of the article.
Updates article properties and saves changes.
DeleteArticle (/api/v1/articles/{id}):

#Retrieves the article.
Checks if the current user is the owner of the article.
Deletes the article from the database.
Special Considerations:

#[Authorize] attribute secures CRUD operations (except GET) to authenticated users.
#[AllowAnonymous] attribute allows unrestricted access to the GetArticles method.
Running and Testing:
Run the Application:

Execute dotnet run in the terminal to start the application.
#Test with Postman:

Import the provided Postman collection.
Utilize /api/v1/register and /api/v1/login for registration and login.
Retrieve the JWT token and use it in the Authorization header for subsequent requests.
Test /api/v1/get-profile and CRUD operations on articles.
#Edge Cases and Considerations:
#User Registration Edge Cases:

Handle duplicate usernames.
Ensure secure password storage.
Login Edge Cases:

#Handle invalid credentials.
Generate and securely manage JWT tokens.
Get Profile Edge Cases:

Ensure only authenticated users access profiles.
Handle scenarios where the user is not found.
#Article CRUD Edge Cases:

Ensure only authorized users perform create, update, and delete operations.
Handle scenarios where articles do not exist.
