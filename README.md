# **AREA** ![](https://github.com/Charliebegood/FileStorage/blob/master/images/area.png)
## Introduction:
- The following documentation allow you to access the informations needed to use our API named **AREA.** This informations will show you how to request our API. This API is used to allow users to configure actions and reactions (link) for a group of given **services** (link). To configure these actions and reactions you will need to **authenticate** (link) to our API and use differents types of request.<br/> Please, read the next documentation before you start.<br/><br/>**Use case :**
>Mr X  want to be informed when it s raining at his home. To do this, he will configure a reaction (cf). To configure this action / reaction, the user will need to be authenticated to our API and to the mail service(link) (to receive a mail on his account).

- In the following parts you will see how to use our API, and features that you have too implement.

## Important:
- All Requests **MUST BE** JSON formatted (only format supported).
- All requests that need an authentication **MUST** contain the JSONWebToken given at the [authentication](#Authentication). (See header authorization bearer token: [Bearer Token](https://swagger.io/docs/specification/authentication/bearer-authentication/)).

## Users:
- ## Creation:
This request allow you to create an account. Next to the creation, an activation mail will be sent to your mail address to activate it.<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/users/create<br/>**Type**: **POST**<br/>**Request**: There is two way to create an account. With our API or with Facebook.
If you use our API, you will receive an activation mail after the creation of your account. Your account must be activated to use it.
Our creation need to contain the following informations:

		{
		"type" : "classic",
		"firstname" : "YourName",
		"lastname" : "YourLastName",
		"email" : "YourEmail@email.com",
		"password" : "YourPassword"
		}
To create an account with facebook, you only need to register with it. Your account will be created if it hasn t already.<br/>See Authentication (link).<br/><br/>**Response**: 

		{
		"status" : "success" /* if the creation was successfull */ "warning" /* if the email is already taken */ "error" /* otherwise */,
		"message" : "Description of the status",
		"data" : null
		}
See response section for the format.(link)
- ## Activation:
To activate your account you need to click the link you received in the mail. If you didn t receive the mail or need another one, just sign up again with the same informations.
- ## <a name="Authentication"></a>Authentication:
Authentication token reminder: (link).<br/>To authenticate to our API with the classic method, you must send the followind request:<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/users/auth<br/>**Type**: POST<br/>**Request**:

		{
		"email" : "YourEmail@email.com",
		"password" : "YourPassword"
		}
**Response**:

		{
		"status" : "success" /* if the authentication was successfull */ "error" /* otherwise. */,
		"message" : "Description of the status.",
		"data" : {"token" : "azdsdqsdq.zadssdsqdqzdzq.dqsdsqdqzdz"}
		}
See response section format.(link)<br/>You must keep this token to authenticate your request. (link)<br/><br/>To authenticate with facebook you must first authenticate to facebook: https://developers.facebook.com/docs/facebook-login/web, then send the following request:<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/users/auth<br/>**Type**: POST<br/>**Request**:

		{
		"email" : "YourEmailGivedByFB",
		"token" : "TokenGivenByFB",
		"type" : "facebook",
		"id" : "IDGivenByFB",
		"username" : "UsernameGivenByFB"
		}
**Response**:

		{
		"status" : "success" /* if the authentication was successfull */ "error" /* otherwise. */,
		"message" : "Description of the status.",
		"data" : {"token" : "azdsdqsdq.zadssdsqdqzdzq.dqsdsqdqzdz"}
		}
See response section format.(link)<br/>You must keep this token to authenticate your request. (link)
- ## Suppression:
Request send to delete an user. Must be auth.(link)<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/users/delete<br/>**Type**: DEL<br/>**Request**:

		null
**Response**:

		{
		"status" : "success" /* if the supression was successfull */ "error" /* otherwise. */,
		"message" : "Description of the status.",
		"data" : null
		}
See response section format.(link)
- ## Informations:
Request send to get information about an user. Must be auth.(link)<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/users/<br/>**Type**: GET<br/>**Request**:

		null
**Response**:

		{
		"status" : "success" /* if the request was successfull */ "error" /* otherwise. */,
		"message" : "Description of the status.",
		- Classic: "data" : {"email" : "YourEmail", "lastname" : "YourLastName", "firstname" : "YourFirstname", "accountType" : "classic"},
		- Facebook: "data" : {"email" : "YourFBEmail", "username" : "FBUsername", "accountType" : "facebook"}
		}
See response section format.(link)<br/>Users informations.

------------

## Services:
- ## Services availables:
Request send to get informations about all the services.<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/services/<br/>**Type**: GET<br/>**Request**:

		null
**Response**:

		{
		"status" : "success" /* if the request was successfull */ "error" /* otherwise. */,
		"message" : "Description of the status.",
		"data" : {"name" : "ServiceName",
				"description" : "Service description",
				"_id" : "Id of the service",
				"icon_url" : "Url of the service icon",
				"configured" : "true" | "false" /* if the parameter is true, the service doesn't need connection */,
				"auth_url" : "Authentication url for the service if needed, none otherwise"}
		}
See response section format.(link)<br/>Services informations.
- ## Service description:
Request send to get informations about one specific service.<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/services/idOfTheService<br/>**Type**: GET<br/>**Request**:

		null
**Response**:

		{
		"status" : "success" if the request was successfull, "error" otherwise.
		"message" : Description of the status.
		"data" : {"name" : "ServiceName",
				"description" : "Service description",
				"_id" : "Id of the service",
				"icon_url" : "Url of the service icon",
				"configured" : "true" | "false" (If the parameter is true, the service doesn't need connection),
				"auth_url" : "Authentication url for the service if needed, none otherwise"
				TODOAREA
		}
See response section format.(link)<br/>Service informations.

------------


## Areas:
- ## Add an AREA:
Request send to add an area. You may assign one or further reactions for only one action. Must be auth (link)<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/areas<br/>**Type**: POST<br/>**Request**:

		{
		"action" : { "service_id" : "The service id",
				"_id" : "Id of the action",
				"data" : [ "Data needed by the action described in the service request (link)" ] }
		"reactions" : [{ "service_id" : "The service Id",
				"_id" : "Id of the reaction",
				"data" : [ "Data needed by the reaction described in the service request (link)" ] }, ...]
		}
**Response**:

		{
		"status" : "success" /* if the Area was added successfully */ "error" /* otherwise. */
		"message" : "Description of the status."
		"data" : null
		}
See response section format.(link)

- ## Update an AREA:
Request send to update an area. Must be auth. (link)<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/areas<br/>**Type**: PUT<br/>**Request**:

		{
		"_id" : "Id of the area to update"
		"action" : { "service_id" : "The service id",
				"_id" : "Id of the action",
				"data" : [ "Data needed by the action described in the service request (link)" ] }
		"reactions" : [{ "service_id" : "The service Id",
				"_id" : "Id of the reaction",
				"data" : [ "Data needed by the reaction described in the service request (link)" ] }, ...]
		}
**Response**:

		{
		"status" : "success" /* if the Area was updated successfully */ "error" /* otherwise. */
		"message" : "Description of the status."
		"data" : null
		}
See response section format.(link)

- ## Delete an AREA:
Request send to delete an area. Must be auth. (link)<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/areas<br/>**Type**: DEL<br/>**Request**:

		{
		"_id" : "Id of the area to delete"
		}
**Response**:

		{
		"status" : "success" /* if the Area was deleted successfully */ "error" /* otherwise. */
		"message" : "Description of the status."
		"data" : null
		}
See response section format.(link)

- ## AREAS informations for the user:
Request send to get informations on areas of the user. Must be auth. (link)<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/areas<br/>**Type**: GET<br/>**Request**:

		null
**Response**:

		{
		"status" : "success" /* if the request was successfull */ "error" /* otherwise. */
		"message" : "Description of the status."
		"data" : { TODOAREA }
		}
See response section format.(link)

- ## AREA info by ID:
Request send to get informations of an area of the user. Must be auth. (link)<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/areas/IdOfTheArea<br/>**Type**: GET<br/>**Request**:

		null
**Response**:

		{
		"status" : "success" /* if the request was successfull */ "error" /* otherwise. */
		"message" : "Description of the status."
		"data" : { TODOAREA }
		}
See response section format.(link)

------------


## General:
- ## Reponse format:
A request will have only one format of response. This response will always be in JSON.<br/>A response always contains three elements:

		{
		"status" : "success" | "error" | "warning".
		"message" : "A description of the request result".
		"data" : "Contains additional data in result of the request."
		}

- ## About.json:
The API answer a request about.json which allow an application to access general informations about our API.<br/><br/>**URL**: https://toadsterubuntu.ddns.me:8080/about.json<br/>**Type**: GET<br/>**Request**:

		null
**Response**:

		TODOAREA
		{
		"status" : "success" /* if the request was successfull */ "error" /* otherwise. */
		"message" : "Description of the status."
		"data" : {
			"client ": 
				{"host":  "10.101.53.35"},
			"server ": {
				"current_time ":  1531680780 ,
				"services ":  [{
					"name": "facebook",
					"actions ": [{
						"name": "new_message_in_group",
						"description ": "A new  message  is  posted  in the  group"},
						{"name": "new_message_inbox",
						"description ": "A new  private  message  is  received  by the  user"},
						{"name": "new_like",
						"description ": "The  user  gains a like  from  one of their  messages"}],
					"reactions ": [{
						"name": "like_message",
						"description ": "The  user  likes a message"}]},
					{"name": "intra",
					"actions ": [{
						"name": "new_project_subscription",
						"description ": "The  user  signs  up for a project"}],
					"reactions ": [{
						"name": "activity_subscribe",
						"description ": "The  user  signs  up for an  activity"},
						{"name": "module_subscribe",
						"description ": "The  user  signs  up for a unit"}]
				}]
			}
		}
		}
See response section format.(link)

------------


## Credits:
>This project has been made by Charles Descoust, Charles Aubert, Simon Gourlet and bastien Lécussan.
Feel free to contact us if you have feedback feedback at: area.epitech.toulouse@gmail.com

------------
