# GoogleSheetIntegration

To get the read_all authorization in order to retieve all the activities you have to make all the below steps
  
1) Get authorization code from authorization page. This is a one time, manual step. 
Paste the below code in a browser, hit enter then grab the "code" part from the resulting url. 

ID_client 49591
Client Secret	4ab2be93e692650356cc4287ec6e2b1cd137aea7

https://www.strava.com/oauth/authorize?client_id=49591&redirect_uri=http://localhost&response_type=code&scope=activity:read_all

code=982206c354ddfc34d3f109a7fcf2625b051f2ea0

2) Exchange authorization code for access token & refresh token(post)

https://www.strava.com/oauth/token?client_id=49591&client_secret=your_client_secret&code=your_code_from_previous_step&grant_type=authorization_code

access_token=7c5e3031a96f7f2a132ba6b3122bf9eb94b4af65
refresh_token=cfedcb9b7e79842fb9eea4b864b9535fd6106418

3) View your activities using the access token just received

https://www.strava.com/api/v3/athlete/activities?access_token=access_token_from_previous_step

3) Use refresh token to get new access tokens

https://www.strava.com/oauth/token?client_id=your_client_id&client_secret=your_client_secret&refresh_token=your_refresh_token_from_previous_step&grant_type=refresh_token

-----

acess token efb237a707fc227b0a91dba88f3dfcd6efbe79b8




This token has scope:read that maybe is not enough to do what you want (i.e. are your activities public or private?).

If you need a new token with different scopes you have to follow these steps.

STEP 1: redirect the user to Strava's authorization page:

https://www.strava.com/oauth/authorize?
    client_id=YOUR_CLIENT_ID&
    redirect_uri=YOUR_CALLBACK_DOMAIN&
    response_type=code&
    scope=YOUR_SCOPE
STEP 2: read code parameter from response:

http://YOUR_CALLBACK_DOMAIN/?
    state=&
    code=AUTHORIZATION_CODE_FROM_STRAVA&
    scope=YOUR_SCOPE
STEP 3: ask for a new access token using a POST containing the authorization code; you'll find the new access_token in the JSON response.

https://www.strava.com/oauth/token?
    client_id=YOUR_CLIENT_ID&
    client_secret=YOUR_CLIENT_SECRET&
    code=AUTHORIZATION_CODE_FROM_STRAVA&
    grant_type=authorization_code
You can find client ID, client secret and callback domain in your application page.

You can find the list of new scopes in this documentation.

If you are the only person that use your application you can manually do the first 2 steps using a browser and http://localhost as callback domain.