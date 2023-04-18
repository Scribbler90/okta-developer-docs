The following section outlines the main request required to implement the OTP flow using direct calls to the Okta OIDC & OAuth 2.0 API.

### Request for tokens

Before you can begin this flow, collect the username and the OTP from the user in a manner of your choosing. Then, make a single API call to the [authorization server's](/docs/concepts/auth-servers/) `/token` endpoint. If you are using the [default custom authorization server](/docs/concepts/auth-servers/#default-custom-authorization-server), then your request would look something like this:

```bash
curl --request POST \
  --url https://${yourOktaDomain}/oauth2/default/v1/token \
  --header 'accept: application/json' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data 'client_id=${client_id}&scope=openid profile&grant_type=urn:okta:params:oauth:grant-type:otp&otp=${123456}&login_hint=${testuser%40example.com}'
```

Note the parameters that are passed:

- `client_id` matches the client ID of the native application that you created in the [Set up your app](#set-up-your-app) section. You can find it at the top of your app's **General** tab.
- `scope` must be at least `openid`. See the **Create Scopes** section of the [Create an authorization server guide](/docs/guides/customize-authz-server/main/#create-scopes).
- `grant_type` is `urn:okta:params:oauth:grant-type:otp`, indicating that you are using the direct authentication OTP grant type. Use this grant type for OTP factors (such as Google Authenticator) that you want to use as a primary factor.
- `otp` is the one-time passcode that your app obtained from the user.
- `login_hint` is the username (email) of a user registered with Okta.

For more information on these parameters, see [Custom Authorization Servers](https://developer.okta.com/docs/api/openapi/okta-oauth/oauth/tag/CustomAS/#tag/CustomAS/operation/challengeCustomAS).

If the credentials are valid, your application receives back access and ID tokens:

```json
{
    "access_token": "eyJhb[...]56Rg",
    "expires_in": 3600,
    "id_token": "eyJhb[...]yosFQ",
    "scope": "openid profile",
    "token_type": "Bearer"
}
```

### Validate access token

When your application passes a request with an access token, the resource server needs to validate it. See [Validate access tokens](/docs/guides/validate-access-tokens/).