# Azure Static Web Apps Authentication with GitHub

[Microsoft Learn Article](https://learn.microsoft.com/en-us/azure/static-web-apps/authentication-authorization)

## Start Here

Step 1: Add staticwebapp.config.json

```json
{
	"routes": [
		{
			"route": "/*",
			"allowedRoles": [
				"authenticated"
			]
		}
	],
	"responseOverrides": {
		"401": {
			"statusCode": 302,
			"redirect": "/.auth/login/github"
		}
	},
	"navigationFallback": {
		"rewrite": "/index.html"
	},
	"auth": {
		"identityProviders": {
			"github": {
				"registration": {
					"clientIdSettingName": "CLIENT_ID_GITHUB",
					"clientSecretSettingName": "CLIENT_SECRET_GITHUB"
				}
			}
		}
	}
}
``` 


## GitHub and Azure Setup Instructions

### GitHub Setup

1. Go to [Github.com](https://github.com).
2. Go to your profile and navigate to **Settings**.
3. Select **Developer Settings**.
4. Go to **OAuth Apps**.
5. Click on **New OAuth App** and fill in the details:
    1. **Application name**: *Name your app*
    2. **Homepage URL**: `https://sample.com/`
    3. **Authorization callback URL**: `https://sample.com/.auth/login/github/callback`
    4. Click **Register application**.
    5. Copy the **Client ID**.
    6. Click **Generate a new client secret** and copy the **Client Secret**.

### Azure Setup

1. Open the [Azure portal](https://portal.azure.com).
2. Go to your **Static Web App** resource.
3. Navigate to **Settings** > **Environment Variables**.
4. Add the following environment variables:
    - `CLIENT_ID_GITHUB` = *paste Client ID*
    - `CLIENT_SECRET_GITHUB` = *paste Client Secret*
5. Click **Apply Changes**.

### Endpoints

This setup gives access to the following endpoints:

- `/.auth/me` - Returns user info.
- `/.auth/logout` - Logs out the user.
- `/.auth/login/github` - Directs the user to GitHub login.
