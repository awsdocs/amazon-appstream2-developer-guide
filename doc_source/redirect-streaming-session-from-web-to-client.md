# Redirect a Streaming Session from the Web Browser to the AppStream 2\.0 Client<a name="redirect-streaming-session-from-web-to-client"></a>

You can configure AppStream 2\.0 to redirect a streaming session from a web browser to the AppStream 2\.0 client\. That way, when your users sign in to AppStream 2\.0 and start a streaming session in their web browser, their session is redirected to the AppStream 2\.0 client\. To do so, perform these steps\.

1. Use the AppStream 2\.0 CreateStreamingURL API action to generate a streaming URL\.

1. Add the following prefix for the custom AppStream 2\.0 client handler to the streaming URL: **amazonappstream:**

   Together, the prefix and streaming URL are formatted as follows:

   **amazonappstream:***base64encoded\(streamingURL\)*

1. When users are redirected to the streaming URL, their browser detects that the link must be opened by the AppStream 2\.0 client\.

1. Users are prompted to choose whether they want to start the streaming session by using the AppStream 2\.0 client\. 

1. After the prompt, either of the following occurs:
   + If the AppStream 2\.0 client is installed by the user, they can choose to continue the streaming session by using the AppStream 2\.0 client\. 
   + If the AppStream 2\.0 client is not installed, the browser returns a callback to indicate that the client application is not installed\. In this case, you can configure a prompt that displays a link to the AppStream 2\.0 client\. Users can download the AppStream 2\.0 client, install it, and refresh their browser to start the streaming session by using the AppStream 2\.0 client\.