## Christopher Schrader
### Lab Report 2 (Lab 3)
---

#Code for `StringServer.java`:

```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;

    String wholeString = "";
    int numStrings = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            //return the list of our strings
            return String.format("%s", wholeString);
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    numStrings++;
                    wholeString += numStrings + ". " + parameters[1] + "\n";
                    return String.format("Successfully added %s to our list of strings/entire string.", parameters[1]);
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
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

#Screenshot 1, using `/add-message`:
![First](lab3_1.png)

