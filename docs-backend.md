## 1. Overview

This API is part of a Flask-based web application that handles **user authentication**, **image uploads**, **image processing**, and **user interactions** such as favorites and feedback.
## 2. Page Navigation and Routing

These endpoints **solely** render pages without performing backend operations:
- `GET /` → Index Page
- `GET /signup` → Signup Page 
- `GET /upload` → Upload Page
- `GET /login` → Login Page
- `GET /userprofile` → User Profile Page (Requires login)
- `GET /whatwedo` → What We Do Page
- `GET /changepassword` → Change Password Page
- `GET /analysis` → Analysis Page
- `GET /logout` → Logout and redirect to Index Page
- `GET /imagedetail` → Image Detail Page
- `GET /feedback` → Feedback Page
- `GET /gallery` → Gallery Page
- `GET /getImage` → Get the image id from the user session
- `GET /images/sortBy< TimeDesc | TimeAsc | Tag >` → sort by different methods: times and tags.
- `GET /image/<int:image_id>` → get images by image id.
- `GET /getcurrentuserimages` → get images belongs to a user (uid is email), queried from database.

## 3. User Authentication & User Operations
This app uses email and password to authenticate.
The default email **`trustindicator@gmail.com`** and password **`vfiz hsgw ctke tdeu`**
- `POST /register` → Registers a new user. 
	- Response: "Email already exists.
- `POST /login_function` → Authenticate a user. 
	- Response: Invalid username or password
- `GET /logout` → Logs out the user and clears session.
    - Response: Redirects to the index page.

- `POST /change_profile_photo` → Changes the user's profile photo.
    - Response fail: "No image selected."
- `GET /get_current_user` → Retrieves current user details.
    - Response: JSON object with user details.
## 4. Image Management
To handle the image operations, the program uses Jsonify technique. 
- `POST /uploadImage` → Uploads an image.
    - Response: "Allowed file types are: png, jpg, jpeg, gif"
- `GET /getimagedetail/<int:image_id>` → Retrieves details for a specific image.
    - Response: JSON object with image details, or 
- `GET /getcurrentuserimages` → Retrieves images uploaded by the logged-in user.

## 5. Favorites and Feedback
Favorites and feedback involves database. 
- `POST /submit_feedback` → Submits user feedback.
    - Response fail: "Error, please try again."


- `POST /register` → Regist a user, format:
    ```json
    {
        "UserName": "john_doe",
        "Email": "johndoe@example.com",
        "LegalName": "John Doe",
        "Password": "SecurePass123"
    }
    ```
- `POST /reset-password` → Reset password for user, need email and newPassword (why need that?).
- `POST /change-password` → Reset password for user, need email, oldPassword and newPassword.

- `POST /send-code` → Send verification code to email. 
- `POST /verify-code` → Verrify user code. The JSON request format should contain: token: The JWT token provided to the user; code: The user-entered verification code.
    ```json
    {
        "token": "xxx",
        "code": "123456"
    }
    ```
# ^^ the backend program seems to registering the user by code sending and verification, but not tested.

- `POST /addToFavourite` → Adds an image to the user's favorites.
    - Response fail: "Please login to add favourite."
- `POST /checkFavourite` → Checks if an image is in the user's favorites.
    - Response: JSON object with favorite status.
- `POST /deleteFavourite` → Removes an image from the user's favorites.
    - Response success: "Favorite removed successfully"
- `POST /updateImageType` → Update the "type" of an image defined by imageId and imageType.

## 6. Error Code

| Status Code | Meaning               |
| ----------- | --------------------- |
| 400         | Bad Request           |
| 401         | Unauthorized          |
| 404         | Not Found             |
| 500         | Internal Server Error |
