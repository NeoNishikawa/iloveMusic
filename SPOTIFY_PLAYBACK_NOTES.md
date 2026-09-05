Official Spotify playback implementation notes collected Sep 4, 2026:

Spotify recommends Authorization Code with PKCE for single-page web apps. The Web Playback SDK requires a valid access token for a Spotify Premium user. The Transfer Playback Web API endpoint also only works for Premium users. The Web Playback SDK documentation states that developer tools must not be used in commercial projects without Spotify's prior written approval.

Sources:
- https://developer.spotify.com/documentation/web-api/tutorials/code-pkce-flow
- https://developer.spotify.com/documentation/web-playback-sdk/reference
- https://developer.spotify.com/documentation/web-api/reference/transfer-a-users-playback
- https://developer.spotify.com/documentation/web-playback-sdk
The production site uses a client-side PKCE redirect URI of `https://ilovemusic-production.up.railway.app/`. Spotify Developer Dashboard was opened for the LoveMusic app, and this URI is currently entered in the Add Redirect URI field. It still needs to be added and the app settings saved before OAuth can be tested.
Spotify Developer Dashboard now lists the production redirect URI `https://ilovemusic-production.up.railway.app/` alongside the existing URIs in edit mode. The app is still in unsaved edit state; the Save action is below the API/SDK selection area.
The production redirect URI has been added to the Spotify app's redirect URI list. The dashboard is still in edit mode and requires clicking Save to persist the change. The page layout is horizontally offset, so the Save control may require returning to the form's visible left area.
The production redirect URI remains present in the Spotify app edit form. The dashboard viewport places the Save control below the SDK selection and above the footer; the content currently renders with a wide horizontal offset, so the save action still needs to be targeted before OAuth testing.
Live OAuth test reached Spotify authorization for LoveMusic using PKCE and redirect URI `https://ilovemusic-production.up.railway.app/`. Spotify consent shows account data, playback activity, and permission to control and stream on Spotify devices. The account shown is `RIS S`. The flow is waiting at the consent page; no access token has been exposed.
The server-side OAuth implementation is deployed on Railway. The latest active deployment includes root callback handling, so Spotify can redirect to the already-registered production URI `https://ilovemusic-production.up.railway.app/` and the server exchanges the code before redirecting back to `/`. Latest active code commit: `78242e7`.
