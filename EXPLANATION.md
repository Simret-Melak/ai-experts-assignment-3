
## What was the bug?
The client incorrectly handled dictionary-based tokens. When `self.oauth2_token` was a dictionary instead of an `OAuth2Token` object, the code:
1. Did not refresh the token 
2. Did not add an Authorization header to requests
3. Caused the test `test_api_request_refreshes_when_token_is_dict` to fail

## Why did it happen?
In `app/http_client.py`, the refresh condition only checked for:
- No token (`None`)
- Or an expired `OAuth2Token` object

Dictionary tokens were completely ignored. They didn't trigger a refresh (since they weren't `None` or an expired `OAuth2Token`), and they didn't add an Authorization header (since the header was only added for `OAuth2Token` objects).

## Why does your fix actually solve it?
The fix adds dictionary tokens to the refresh condition

if (not self.oauth2_token or 
    isinstance(self.oauth2_token, dict) or  # THIS LINE
    (isinstance(self.oauth2_token, OAuth2Token) and self.oauth2_token.expired)):
    self.refresh_oauth2()

Now when a dictionary token is present:

1. 'isinstance(self.oauth2_token, dict)' evaluates to 'True'
2. 'refresh_oauth2()' is called, replacing the dictionary with a fresh 'OAuth2Token'
3. The fresh token then adds the Authorization header with '"Bearer fresh-token"'

This ensures all token formats ('None', 'OAuth2Token', and 'dict') are properly handled.

## What’s one realistic case / edge case your tests still don’t cover?

A realistic edge case that still isn’t covered is when `oauth2_token` is a **dictionary containing a valid, non-expired token**. After the fix, all dictionary tokens automatically trigger a refresh, regardless of whether their `expires_at` value is still valid. This means even a correct, unexpired legacy token would be unnecessarily replaced. There is no test verifying that a valid dictionary-based token is preserved and used without refreshing, nor is there logic that checks expiration for dictionary tokens before deciding to refresh.




