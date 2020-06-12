## Url Unfurl

When a user posts a GitHub url on the channel, we show an unfurled card to the user with the important information of the resource.

## Flow:

1. When a user posts github url in Teams channel, we get a request and we handle it in the function - handleTeamsAppBasedLinkQuery.
2. We fetch the user information and the github client. We use user's auth token in the github client in case user is signed in, otherwise auth token is taken as empty string.
3. We check if the url provided is public or private.
4. In case the url is public, we unfurl the url for the user. In case the url is private, we unfurl it if the user is signed in, otherwise we prompt the user to signin.
5. We get the attachment for the response using the function - getUnfurlAttachment.
6. In this function, We first get the url type using regex matching and fetch the required parameters corresponding to that url type.
7. Then we pass the parameters to the constructCardJson to create the card using the template for the url type.
8. We then return the final attachment for the url to the main function.
9. The main function then contructs a compose extension response with the attachment and the unfurl card is posted to the Teams channel.

## Status

Accepted

## Context

We need to support unfurling of github urls in Teams channel.

## Decision

Private/Public urls (Sign in) :	Allow unfurling of public urls and prompt user to sign in for unfurling private urls.
Non – GitHub domains : Teams GitHub app will support urls from GitHub domain only & other domains can be handled by Teams itself. 
Caching : Teams has in-built caching which lasts for 30 minutes where they automatically unfurl the url without sending the request to the app. We will go ahead with this.
Supporting 2 Urls : We will support unfurling of only 1 url as of now and will extend later based on telemetry.
Supporting user prompts : We will not show user prompts as of now.
Command remembering : We will support command remembering for all commands in Teams GitHub app in later phases.

## Consequences

None
