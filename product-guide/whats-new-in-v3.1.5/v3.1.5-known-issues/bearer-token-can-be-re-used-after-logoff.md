# RC1-010: Bearer token can be re-used after logoff

{% tabs %}
{% tab title="Description" %}
This was the result of Veracode testing.  This happens on all logouts \(Maana Portal and Knowledge app\).  While we logoff as Auth0 recommends, this is just on the client - the bearer token stays valid until token expiration time.

Auth0 responses below. Veracode report attached \(See page \#8\)

Auth0:

_The logout endpoint clears the session in Auth0 so they can't retrieve a new token. It does not invalidate an issued token._

_Rather than invalidating the token \(this can't be done, at best you can only blacklist it\), you should keep the token expiration window as short as possible and renew it via_ [_silent authentication_](https://auth0.com/docs/api-auth/tutorials/silent-authentication)_. Silent authentication uses the session the logout endpoint clears, so if the user visits the logout_ endpoint, _when you next perform silent authentication they will be required to input their credentials again._

Auth0:

_Due to the way token based authentication works, the tokens will be valid until they expire. One way which this can be mitigated is to shorten the token lifetime, which will_ in turn _shorten the window in which the token can be used after logout. Logout will clear the Auth0 session,_ however _the token will still be valid until expiration._

_The following documentation might be useful:_  
[\_https://auth0.com/docs/api-auth/blacklists-vs-grants\#blacklists\_](https://jira.corp.maana.io/browse/ENG-16565#blacklists_)
{% endtab %}

{% tab title="Repro Steps" %}
1. Copy bearer token
2. Logoff
3. Use saved bearer token to make requests
{% endtab %}

{% tab title="Expected Result" %}
Bearer token can't be used.
{% endtab %}

{% tab title="Actual Result" %}
Bearer token can be used.
{% endtab %}
{% endtabs %}

