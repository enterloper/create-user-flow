# User Creation Flow

### Objectives

To determine the flow for creating a user through the medium of my.scouting
To determine the APIs needed to address the concerns raised from the legacy my.scouting application 
To agree on the flow for creating a user before implementation
To determine the best user experience for the user as this could be their first impression of the application and organization 


## User Flow

At the time of authoring, there are three routes to create a user presence on the 
respective databases associated with `my.scouting`.

#### Route One: Navigating through `beascout.scouting.org`

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
[Second Route](#route-two-anonymously-visiting-myscoutingorg)

</br>
</br>

![beascout.scouting.org map view](./assets/beascoutmap.png "beascout.scouting.org preview")

</br>
</br>

####  Route Two: Visiting my.scouting.org

A user can visit the legacy version of [my.scouting.org](https://my.scouting.org)
and create a presence in the my.scouting databases without any interaction from the Boy Scouts of
America or it's affiliates. With the latest iteration of **my.scouting.org**, a user will also 
have the ability to create an account without interaction from BSA, and without a 
unit/organization specifically chosen.


![my.scouting.org login view](./assets/MYST_landing.png "my.scouting.org landing preview")

Upon clicking on the **Create Account** button, a user will be directed to the 
**Account Creation** page in **my.scouting.org** shown below.


#### Two possibilities:

##### Does not have a Record Identifier

If the user is arriving to this page <em>without</em> an invitation or 
without going through `beascout.scouting.org`, then the full URL will be: 
`my.scouting.org/online-registration/create-account/new`.



##### Has a Record Identifier

If the user is arriving to this page via an invitation (discussed in 
[Route Three](#route-three-visiting-myscoutingorg-via-invitation) or by going through 
**beascout.scouting.org**, then the full URL will be:

`my.scouting.org/online-registration/create-account/{RecordIdentifier}`

**Record Identifier** in the URL would be a unique identifier that will be 
used to link the to-be-made-account with the unit that provided the information. The
**Record Identifier** will be used to map the user's information to the 
respective unit/organization.

![my.scouting.org create account view](./assets/MYST_create_account.png "my.scouting.org 
create account preview")

#### Route Three: Visiting my.scouting.org via Invitation/QR code/email


If the user is provided with a URL via an invitation/QR code/email, they will be directed to the
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
    
        
#### Member ID and Date of Birth fields

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
user of Member Care Services and the respective contact details. with a 
button that when clicked will send the user to the 
[Log In Page](#route-two-anonymously-visiting-myscoutingorg) 
                
#### First Name, Last Name, ZIP CODE









