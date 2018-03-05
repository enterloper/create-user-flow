# User Creation Flow

## Objectives

- To determine the flow for creating a user through the medium of my.scouting
- To determine the APIs needed to address the concerns raised from the legacy my.scouting 
application 
- To agree on the flow for creating a user before implementation
- To determine the best user experience for the user as this could be their first impression of 
the application and organization 


## Your Information

At the time of authoring, there are three routes to create a user presence on the 
respective databases associated with `my.scouting`. 
1. Navigating to the Create Account Page through **BeAScout**
2. Navigating to the Create Account Page by visiting **my.scouting.org**
3. Navigating to the Create Account Page via an invitation from a particular unit.

### Route One: Navigating through `beascout.scouting.org`

A user can visit the [BeaScout](https://beascout.scouting.org/BeAScoutMap.aspx) site and choose
a unit within their area (example shown below), if a unit is accepting applications and has 
properly modified it's settings, an **Apply Now** button will appear on it's flag 
on the map provided by Google maps. If a link is clicked to <em>Apply</em>, the user will be 
sent to **my.scouting.org** that will have a modified URL with a **Record 
Identifier** as query: 

`https://my.scouting.org/VES/OnlineReg/1.0.0/?tu=UF-MB-571paa2015`.

The **Record Identifier** being `UF-MB-571paa2015`. 
The Record Identifier is used to connect the account to be created with the specified unit 
selected from the map (example shown below). From this point, the flow will be similar to the
[Second Route](#route-two-visiting-myscoutingorg)

</br>
</br>

![beascout.scouting.org map view](./assets/beascoutmap.png "beascout.scouting.org preview")

</br>
</br>

###  Route Two: Visiting my.scouting.org

A user can visit the legacy version of [my.scouting.org](https://my.scouting.org)
and create a presence in the my.scouting databases without any interaction from the Boy Scouts of
America or it's affiliates. With the latest iteration of **my.scouting.org**, a user will also 
have the ability to create an account without interaction from BSA, and without a 
unit/organization specifically chosen.


![my.scouting.org login view](./assets/MYST_landing.png "my.scouting.org landing preview")

Upon clicking on the **Create Account** button, a user will be directed to the 
**Account Creation** page in **my.scouting.org** shown below.


#### Two possibilities:

1. ##### Does not have a Record Identifier

    If the user is arriving to this page <em>without</em> an invitation or 
    without going through `beascout.scouting.org`, then the full URL will be: 
    `my.scouting.org/online-registration/create-account/new`.



2. ##### Has a Record Identifier

    If the user is arriving to this page via an invitation (discussed in 
    [Route Three](#route-three-visiting-myscoutingorg-via-invitation-or-qr-or-email) or by going 
    through **beascout.scouting.org** or an invitation, then the full URL will be:

`my.scouting.org/online-registration/create-account/{RecordIdentifier}`

**Record Identifier** in the URL would be a unique identifier that will be 
used to link the to-be-made-account with the unit that provided the information. The
**Record Identifier** will be used to map the user's information to the 
respective unit/organization.

![my.scouting.org create account view](./assets/MYST_create_account.png "my.scouting.org 
create account preview")

### Route Three: Visiting my.scouting.org via Invitation or QR or email


If the user is provided with a URL via an invitation, QR code, email, they will be directed to the
above page with a route similar to: 
<br />
`my.scouting.org/online-registration/create-account/{RecordIdentifier}`
<br />
The flow will then be consistent for each of the previously described scenarios in regard to 
creating a user account.

    
## Creating a user account

Upon entry to the **Create Account Page**, the user will see the view above.
The fields that will be required to advance to the next grouping of questions will be 
**Date of Birth**, **First Name**, **Last Name**, 
**Zip Code**. Because a person without an account or presence within our database, 
the **Member ID** field will not be required. 

The general actions and responses should be taken as the user fills out the **YOUR 
INFORMATION** form for each field:
    
        
### Member ID and Date of Birth fields

If a user has a **Member ID** but is lacking an account, they can enter 
their **Member ID**. Entering a person's **Member ID** will
allow our systems to do a check for account presence in our databases. This action 
can be invoked with only the **Member ID** or with the coupling of 
the value of **Date of Birth**. At the time of authoring this, it is 
understood that both **Member ID** and **Date of Birth** 
will be used to match a person with their respective account.


This action will be fired **ONLY** when the user has fulfilled the 
following two requirements:

1. The **Member ID** field has been filled out and passed UI 
validation.

1. The **Date of Birth** field has been filled out and passed UI 
validation.

If the above requirements are met, when the user leaves the **Date of 
Birth** field, an API will be fired. If **Member ID** is 
missing, the API will not be called. Furthermore, if the actions are done in 
reverse order (meaning the user fills out the **Date of Birth** 
field first and then the **Member ID** field), the same action will 
fire on the blurring (action of losing focus on the field by the user) of the 
**Date of Birth** field.

    
If the API responds with a match, a modal will open stating the presence of the 
user's online account. In addition, a message should be provided informing the 
user of Member Care Services and the respective contact details. With an acknowledgement 
button that when clicked will send the user to the 
[Log In Page](#route-two-visiting-myscoutingorg) 
                
### First Name, Last Name, ZIP Code
**MFSR-122**
If the user's Member ID and Date of Birth values return no results, validation for the **First 
Name**, **Last Name**, and **ZIP Code** will be handled client-side on blur (loss of element 
focus). When the user click's next, validation will again check to ensure there are no errors 
present in the form for the fields **Date of Birth**, **First Name**, **Last Name**, and **ZIP 
Code**. **Member ID** will not be used or validated from this point because it is assumed that the 
value is irrelevant to the system. If validation is cleared, an API will be fired to search for 
potential matches in the BSA database.
 
#### Two Possibilities:

1. If one or more entries are found as a match, the user will be prompted to select the 
matching account and then go through the process of Retrieving their respective Username. If the 
username can not be retrieved, the user will be advised to contact Member Care Services.

1. If no matches are found, the second portion of the create account form will appear, as shown 
below.

![my.scouting.org create account view](./assets/MYST_create_account_2nd_half.png "my.scouting.org 
create account preview")

## Your Account Information

The following fields are used for the second portion of the form:
1. Email Address: The input of this field will be validated client side (in the UI) as well as 
server side (via the API), this value will be used to send instructions, confirmations, and be 
used for credential recovery. 

1. Username: The input of this field will be validated client side as well as via API. The 
following parameters must be followed for Username: 
    - Must be 6 to 20 characters
    - Must be alphanumeric
    - The period (.) and underscore (_) characters are allowed but can not be the last character 
    in a username
    - No other special characters are allowed
    - Spaces are **not** permitted (the UI will enforce this in the form, as well as in the 
    method that consumes the API by trimming/stripping whitespace)
    
    The Username needs to be unique. In order to insure uniqueness, an API must be consumed by 
    the UI to make the appropriate check. When the user leaves the field (on blur), the UI will 
    check to ensure the user followed the above rules. If all of the rules are not followed, the API
    will never be consumed. If the rules are followed and validation passes, the API wil be sent the 
    username to check for uniqueness.  In the event of finding the username is already taken by
    another account, The API should return possible suggestions for the username.

1. Password: The input of this field will be validated client side, and later when the form is 
submitted through the API. The following parameters must be followed for a Password:
    - Must be at least 8 characters but no longer than 12 characters
    - Must meet at least three of the following four criteria:
        - Must contain at least one uppercase letter (A-Z)
        - Must contain at least one lowercase letter (a-z)
        - Must contain at least one numeric character (0-9)
        - Must contain at least one non alphanumeric character (~!@#$%^&*(){}[]<>;:,.?/)

1. Confirm Password: The input of this field will be validated client side. The API does not need
 to check this field as the UI is simply checking for sameness.
 
1. Security Question 1: This field is a drop down/select box with choices populated from the 
backend/server. 
A selection is mandatory.

1. Answer Question 1: This field is an input field that will be the answer to the question 
chosen by the user from the drop down/select box from the previous field.

1. Security Question 2: This field is a drop down/select box with choices populated from an API. 
A selection is mandatory. The question selected from the group of questions delivered from the 
backend/server on Security Question 1 will be removed from the drop down/select options to 
eliminate redundancy. This is currently done client-side. 

1. Answer Question 2: This field is an input field that will be the answer to the question 
chosen by the user from the drop down/select box from the previous field.

1. Lastly, there will be a reCAPTCHA that will be used to minimize any potential automation from 
bots. At the time of authoring, it is unclear if the reCAPTCHA will be used in API validation as 
well.

Once the form is filled out and the user clicks the **NEXT** button, a final validation will 
check the fields on the UI end prior to consuming the "account creation" API. The "account 
creation" API will also do a check to ensure that those consuming the API are also following the 
same guidelines. The payload sent to the API will have the following **JSON** shape:
```
    DateOfBirth type = string, 
    FirstName type = string,    
    LastName type = string,
    ZipCode type = string,
    EmailAddress type = string,
    Password type = string,
    SecurityQuestion1 type = string,
    SecurityAnswer1 type = string,
    SecurityQuestion2 type = string,
    SecurityAnswer2 type = string
```
### With values in a JSON object for clarity.
```
{
    "DateOfBirth": "01/01/2001", 
    "FirstName": "Alexample",    
    "LastName": "McZample",
    "ZipCode": "75062",
    "EmailAddress": "example@gmail.com",
    "Password": "abracadabra",
    "SecurityQuestion1": "What was the name of your first pet?",
    "SecurityAnswer1": "Doggo",
    "SecurityQuestion2": "What was the color and Make of your first car?",
    "SecurityAnswer2": "Brown Chevy"
}
```
If the API returns a ResponseCode of '1', the user will then be taken to the login page for an 
initial login. If the API returns errors, the UI will proivde the appropriate instructions via a 
modal.

## Developer Questions
1. Do we need to send the successfully validated recaptcha value to the API as well?

1. Should we be saving invitation values on a user's created account instance? In other words, 
when a user is invited to scouting, should we be saving the value of that invitationGUID off the URL
to use as a reference later? I think it would be a good idea.

1. If a user does not have an invitationGUID what would that value be (`null`, `undefined`, `'new'`),
 and how are we going to discover where to place that user? The current mockups of the APIs to be
  consumed does not have a "Record Locator" with which the UI team can access or send that user to a
  specific instance of an application directed at a specific group. Basically, we need some way 
  to map a user to an application instance based on an invitation

1. What are we doing with user accounts that are created solely for Youth Protection Training. Is
 this information used at all beyond user access to YPT, and if so, how could we utilize this 
 information for profit for BSA within the scale of the app/website? To my understanding, that data 
 is dead once YPT is completed but still housed in our databases as bloat.