# **AREA** ![](logo)
## Introduction:
- The following documentation allow you to access the informations needed to use our API named **AREA.** This informations will show you how to request our API. This API is used to allow users to configure actions and reactions (link) for a group of given **services** (link). To configure these actions and reactions you will need to **authenticate** (link) to our API and use differents types of request.<br/> Please, read the next documentation before you start.<br/><br/>**Use case :**
>Mr X  want to be informed when it s raining at his home. To do this, he will configure a reaction (cf). To configure this action / reaction, the user will need to be authenticated to our API and to the mail service(link) (to receive a mail on his account).

- In the following parts you will see how to use our API, and features that you have too implement.

## Important:
- All Requests **MUST BE** JSON formatted (only format supported).
- All requests that need an authentication **MUST** contain the JSONWebToken given at the authentication.(link) (See header authorization bearer token: [Bearer Token](https://swagger.io/docs/specification/authentication/bearer-authentication/)).

## Users:
- ### Creation:
This request allow you to create an account. Next to the creation, an activation mail will be sent to your mail address to activate it.<br/><br/>**Url**: https://toadsterubuntu.ddns.me:8080/users/create<br/>**Type**: **POST**<br/>**Request**: There is two way to create an account. With our API or with Facebook.
If you use our API, you will receive an activation mail after the creation of your account. Your account must be activated to use it.
Our creation need to contain the following informations:

		"type" : "classic"
		"firstname" : "YourName"
		"lastname" : "YourLastName"
		"email" : "YourEmail@email.com"
		"password" : "YourPassword"
To create an account with facebook, you only need to register with it. Your account will be created if it hasn t already.<br/>See Authentication (link).<br/><br/>**Response**: 

		"status" : "success" /* if the creation was successfull */ "warning" /* if the email is already taken */ "error" /* otherwise */
		"message" : "Description of the status"
		"data" : null
See response section for the format.(link)
- ### Activation:
To activate your account you need to click the link you received in the mail. If you didn t receive the mail or need another one, just sign up again with the same informations.
- ### Authentication:
Authentication token reminder: link.<br/>To authenticate tou our API with the classic method, you must send the followind request:<br/><br/>**Url**: https://toadsterubuntu.ddns.me:8080/users/auth<br/>**Type**: POST<br/>**Request**:
		- "email" : "YourEmail@email.com"
		- "password" : "YourPassword"
**Response**: 
                "status" : "success" if the authentication was successfull, "error" otherwise.
                "message" : Description of the status.
                "data" : {"token" : "azdsdqsdq.zadssdsqdqzdzq.dqsdsqdqzdz"}
See response section format.(link)<br/>You must keep this token to authenticate your request. (link)<br/><br/>To authenticate with facebook you must first authenticate to facebook: https://developers.facebook.com/docs/facebook-login/web,
            then send the following request:
            url: https://toadsterubuntu.ddns.me:8080/users/auth
            Type: POST
            Request:
                - "email" : "YourEmailGivedByFB"
                - "token" : "TokenGivenByFB"
                - "type" : "facebook"
                - "id" : "IDGivenByFB"
                - "username" : "UsernameGivenByFB"
            Response:
                See response section format.(link)
                You must keep this token to authenticate your request. (link)
                "status" : "success" if the authentication was successfull, "error" otherwise.
                "message" : Description of the status.
                "data" : {"token" : "azdsdqsdq.zadssdsqdqzdzq.dqsdsqdqzdz"}

- ### Suppression:

- ### Informations:

------------

## Services:
- ### Services availables:

- ### Service description:

------------


## Areas:
- ### Add an AREA:

- ### Update an AREA:

- ### Delete an AREA:

- ### AREAS informations for the user:

- ### AREA info by ID:

------------


## General:
- ### Reponse format:

- ### About.json:

------------


## Credits:
>This project has been made by Charles Descoust, Charles Aubert, Simon Gourlet and bastien Lécussan.
Feel free to contact us if you have feedback feedback at: area.epitech.toulouse@gmail.com

------------

