Checklist
✅ Install Heroku CLI and Go.
✅ Create and test a Go app.
✅ Add Procfile and configure the port.
✅ Deploy to Heroku with Git.
✅ Verify and update your app.






Step 1: Install Required Tools

Install Go
  Ensure Go is installed on your Mac. If not, install it via Homebrew:
    brew install go

Install the Heroku CLI
  Download and install the Heroku CLI:
    brew tap heroku/brew && brew install heroku

Verify Installations
  Check if both tools are installed correctly:
    go version
    heroku --version





Step 2: Prepare Your Go App

Create a New Go Project
  If you don’t already have a Go app, create one:
    mkdir go-heroku && cd go-heroku
    go mod init go-heroku

Write Sample Code
  Create a main.go file:
    package main

    import (
        "fmt"
        "log"
        "net/http"
        "os"
    )

    func main() {
        port := os.Getenv("PORT")
        if port == "" {
            port = "8080" // Default port
        }
        http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
            fmt.Fprintln(w, "Hello, Heroku!")
        })
        log.Printf("Server starting on port %s\n", port)
        log.Fatal(http.ListenAndServe(":"+port, nil))
    }

Test Locally
  Run your app to ensure it works:
    go run main.go
    Visit http://localhost:8080 in your browser.





Step 3: Prepare for Heroku Deployment

Create a Procfile
  Add a file named Procfile (no extension) to specify how to run your app:
    echo "web: ./go-heroku" > Procfile

Build the Go App
  Compile the app into a binary that Heroku can execute:
    go build -o go-heroku

Add a .gitignore
  Create a .gitignore file to exclude unnecessary files:
    echo "go-heroku" > .gitignore
    echo "*.log" >> .gitignore
    echo "*.tmp" >> .gitignore





Step 4: Set Up Heroku

Log in to Heroku
  Authenticate with Heroku CLI:
    heroku login

Create a New Heroku App
  In your project directory, create a new Heroku app:
    heroku create io-go-heroku
    Replace go-heroku with a unique name. If omitted, Heroku assigns a random name.


Set the Buildpack
  Tell Heroku to use the Go buildpack:
    heroku buildpacks:set heroku/go --app io-go-heroku





Step 5: Deploy Your App

Initialize Git Repository
  If your project isn’t already a Git repository:
    git init
    git add .
    git commit -m "Initial commit"

Deploy to Heroku
  Push your code to Heroku:
    git push heroku main





Step 6: Verify Deployment

Open Your App
  Once deployed, Heroku provides a URL for your app. Open it in your browser:
    heroku open

Check Logs
  To debug or check the status of your app:
    heroku logs --tail





Step 7: Make Updates

Edit Your Code
  Modify your main.go or other files as needed.


Redeploy
  After changes:
    git add .
    git commit -m "Updated app"
    git push heroku main
    Step 8: Clean Up (Optional)

Remove the App
  If you no longer need the app
    heroku apps:destroy --app go-heroku --confirm go-heroku