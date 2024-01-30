# Lab Report 2  

## Part 1  
ChatServer.java code:  
(also uses Server.java with the URLHandler interface given to us in class)
```
import java.io.IOException;
import java.net.URI;
import java.util.List;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String messages = "";

    public String handleRequest(URI url){
        String query = url.getQuery();
        if (url.getPath().equals("/add-message")) {
            if(query.startsWith("s=")) {
                String[] splitInput = url.getQuery().split("=");
                String[] messageStrSplit = splitInput[1].split("&");
                String messageRough = messageStrSplit[0]; //there are + in between the words
                String messageFinal = messageRough.replace("+", " "); //replace with a space
                String userStr = splitInput[2];
                String messageToAdd = String.format("%s: %s \n", userStr, messageFinal);
                messages = messages + messageToAdd;
                return messages;
            }
            else {
                return "/add-message requires a query parameter s\n";
            }
        }
        else {
        return String.format("add a message using: /add-message?s=<string>&user=<string>");
        }

    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }
        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
    }
}
```
**First Add Message**  
