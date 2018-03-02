<h1>User Creation Flow</h1>

<h3>Objectives</h3>

<ul>
    <li> To determine the flow for creating a user through the medium of my.scouting</li>
    <li> To determine the APIs needed to address the concerns raised from the legacy my.scouting application</li> 
    <li> To agree on the flow for creating a user before implementation</li>
    <li> To determine the best user experience for the user as this could be their first impression of the application and organization</li> 
</ul>

<h2>User Flow</h2>

<p>
    At the time of authoring, there are three routes to create a user presence on the 
    respective databases associated with <code>my.scouting</code>.
</p>

<h4>
    Route One: Navigating through <code>beascout.scouting.org</code>
</h4>

<p>
    A user can visit the <a href="https://beascout.scouting.org/BeAScoutMap.aspx">BeaScout</a> site 
    and choose
    a unit within their area (example shown below), if a unit is accepting applications and has 
    properly modified it's settings, an <strong>Apply Now</strong> button will appear on it's flag on the 
    map provided by Google maps. If a link is clicked to <em>Apply</em>, the user will be sent to
    <strong>my.scouting.org</strong> that will have a modified URL with a <strong>Record Locator</strong> as query: 
</p>
<code>https://my.scouting.org/VES/OnlineReg/1.0.0/?tu=UF-MB-571paa2015</code>.
</p>

<p>
    The <strong>Record Locator</strong> being <code>UF-MB-571paa2015</code>. 
    The Record Locator is used to connect the account to be created with the specified unit selected from the map (example shown below).
    From this point, the flow will be similar to the <a href='#route-two-anonymously-visiting-myscoutingorg'>Second Route</a>
</p>

</br>
</br>

![beascout.scouting.org map view](./assets/beascoutmap.png "beascout.scouting.org preview")

</br>
</br>

<h4> Route Two: Anonymously visiting my.scouting.org</h4>
<p>
    A user can visit the legacy version of <a href="https://my.scouting.org">my.scouting.org</a> and 
    create a presence in the my.scouting databases without any interaction from the Boy Scouts of America or it's affiliates.
    With the latest iteration of <strong>my.scouting.org</strong>, a user will also have the ability to 
    create an account without interaction from BSA, and without a unit/organization specifically chosen.
</p>

![my.scouting.org login view](./assets/MYST_landing.png "my.scouting.org landing preview")

<p>
    Upon clicking on the `Create Account` button, a user will be directed to the Account Creation 
    page in `my.scouting.org`. 
</p>

<h4>Two possibilities:</h4>

<ul>
    <li> 
        </p>
            If the user is arriving to this page without an invitation (discussed in 
            <a href="#route-three-visiting-myscoutingorg-via-invitation">Route Three</a> or 
            without going through <code>beascout.scouting.org</code>, then the full URL will be: 
            <code>my.scouting.org/online-registration/create-account/new</code>.
        </p>
    </li>
    <li>
        </p>
            If the user is arriving to this page via an invitation (discussed in 
            <a href="#route-three-visiting-myscoutingorg-via-invitation">Route Three</a> or by going through 
            <strong>beascout.scouting.org</strong>, then the full URL will be:
        </p>
        <code>my.scouting.org/online-registration/create-account/{RecordIdentifier}</code>
        <p>
            <strong>Record Identifier</strong> in the URL would be a unique identifier that will be 
            used to link the to-be-made-account with the unit that provided the information.
        </p>
    </li>
</ul>

![my.scouting.org create account view](./assets/MYST_create_account.png "my.scouting.org 
create account preview")

#### Route Three: Visiting my.scouting.org via Invitation










